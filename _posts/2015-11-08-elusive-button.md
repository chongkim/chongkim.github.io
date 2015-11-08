---
layout: post
title: Elusive Button
date: 2015-11-08 14:44:10
categories: programming
---

<style>
#btn {
  position: relative;
  top: 0px;
  left: 0px;
}
</style>

<form onsubmit="return false">
  Click submit
  <input id="btn" type="button" value="submit" onclick="$('#msg').html('you got me');"><br/>
  <div id="msg"></div>
</form>

<script>
$(document).ready(function() {
  $('#btn').hover(function(e) {
    var $el = $('#btn'),
        offset = $el.offset(),
        newtop = offset.top + 25 - Math.random()*50,
        newleft = offset.left + 25 - Math.random()*50;
    $el.offset({top: newtop, left: newleft});
  });
});
</script>
