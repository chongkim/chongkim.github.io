---
layout: post
title: Health Check on a Django Server
date: 2018-04-05 16:58:44
categories: programming
---


When you have a load balancer on AWS, there is a tab called "Health Check".  By
default it is set to ping each ec2 instance on port 80 every few seconds.  The
problem with this is that it doesn't work well when the site is up but
misbehaving.  For example, if your ec2 instance starts throwing 500 errors on
all its requests, the loadbalancer thinks that it is still healthy because the
pings are going through.

To fix this, you need to set up to request an actual page and verify the
response status is 200.  You do this by

* Clicking the Edit Health Button.
* Choosing the Ping Protocol to HTTP
* Enter the URI path to check (say `/health_check`).

On your server, you can write a code to handle the `/health_check` request.  For
example, in Django, you do something like this:

{% highlight python %}
# mysite/urls.py
    ...
    url(r'^health_check/?$', views.HealthCheckView.as_view()),
    ...

# myapp/views.py
from django.db import connection
from django.http import HttpResponse

class HealthCheckView(View):
    """
    Checks to see if the site is healthy.
    """
    def get(self, request, *args, **kwargs):
        with connection.cursor() as cursor:
            cursor.execute("select 1")
            one = cursor.fetchone()[0]
            if one != 1:
                raise Exception('The site did not pass the health check')
        return HttpResponse("ok")
{% endhighlight %}

If you have a very simple setup, this is all you need to do.

Let's make this more complicated.  Let's say your nginx server has a rewrite
rule to redirect http requests to https and your loadbalancer.  This will fail
the Health Check because it expects a 200 response, not a 301 redirect response.
In this case, you need to modify the rule to look like this:

{% highlight conf %}
server {
    listen 80
    if ($http_x_forwarded_proto != "https") {
        set $redirect_to_https 1;
    }
    if ($request_uri = '/health_check') {
        set $redirect_to_https 0;
    }
    if ($redirect_to_https = 1) {
        rewrite ^(.*)$ https://$http_host$REQUEST_URI permanent;
    }
}
{% endhighlight %}

You can test it on the command line:

{% highlight bash %}
$ curl -I http://127.0.0.1/health_check
HTTP/1.1 200 OK
Server: nginx
Date: Thu, 05 Apr 2018 21:11:13 GMT
Content-Type: text/html; charset=utf-8
Content-Length: 2
Connection: keep-alive
X-Frame-Options: SAMEORIGIN
Vary: Cookie

{% endhighlight %}

Make sure it says `200 OK`.

Now this should work.... but with your django app, it probably won't.  So far
you've updated the Health Check to HTTP.  You added the code in your django app
to handle `/health_check`.  You updated the nginx config file. But it's still
failing.  Let's see what's going on.

Using `nc` (nc is netcat, which is like `cat` but for sockets).  We're going to
set up a dummy server and listen some port, let's say 8080.  We run this:

{% highlight bash %}
$ nc -l 8080
{% endhighlight %}


It'll wait there listening on the port until it gets something.

We go to AWS's Health Check tab again and enter `8080` for the port and
`/health_check` for the ping path.  When we go back to the bash prompt, we see

{% highlight bash %}
$ nc -l 8080
GET /health_check HTTP/1.1
host: 123.45.67.8:8080
User-Agent: ELB-HealthChecker/1.0
Accept: */*
Connection: keep-alive

{% endhighlight %}

(You can ctrl-c out of that).  You can see the actual request that is being sent
from the load balancer.  We notice something interesting with the `host`.  It is
using the private IP of the ec2 instance running our django app.  Normally when
somone enters a url into the browser (ie. `http://mysite.com`), it would be
`host: mysite.com`, but the load balancer doesn't know that and just uses the
private IP of the instance.

How does this help us?  Well, if you look at your `mysite/settings.py`, you
should see a `ALLOWED_HOSTS` being set to a list of domain names and IP
addresses:

{% highlight python %}
# mysite/settings.py

ALLOWED_HOSTS = [
    'mysite.com',
    'www.mysite.com',
    'localhost',
    '127.0.0.1',
]
{% endhighlight %}

We need to add our private IP into this list.  The problem with hard-coding it
into this file is that the private IP may change (when this instance get reboot
for example) and imagine maintaining a list of IP address if you have a bunch of
machines.  The solution is to dynamically find out the private IP of this ec2
instance:

{% highlight python %}
# mysite/settings.py

import requests

ALLOWED_HOSTS = [...]

try:
    EC2_IP = requests.get('http://169.254.169.254/latest/meta-data/local-ipv4').text
    ALLOWED_HOSTS.append(EC2_IP)
except requests.exceptions.RequestException:
    pass

{% endhighlight %}

The hard-coded URL comes from the [AWS EC2 User
Guide](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-instance-metadata.html#instancedata-data-retrieval).

Now everything is set up.  You're good to go!  And the Health Check should be
passing.
