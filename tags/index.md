---
title: 标签
layout: page
---

<div id='tag_cloud'>
  {% for tag in site.tags %}
    <a href="#{{ tag[0] }}" title="{{ tag[0] }}" rel="{{ tag[1].size }}">{{ tag[0] }}</a>
  {% endfor %}
</div>

<div class="listing">
  <ul>
    {% for tag in site.tags %}
    <div class="listing-classify">
      <li class="listing-classify-tag" id="{{ tag[0] }}">{{ tag[0] }}</li>
      <div class="listing-classify-post">
      {% for post in tag[1] %}
        <li>
          <time datetime="{{ post.date | date:"%Y-%m-%d" }}">{{ post.date | date:"%Y-%m-%d" }}</time>
          <a href="{{ post.url }}" title="{{ post.title }}">{{ post.title }}</a>
        </li>
      {% endfor %}
      </div>
    </div>
    {% endfor %}
  </ul>
</div>

<script src="/media/js/jquery.tagcloud.js" type="text/javascript" charset="utf-8"></script> 
<script language="javascript">
$.fn.tagcloud.defaults = {
    size: {start: 1, end: 1, unit: 'em'},
      color: {start: '#f8e0e6', end: '#980000'}
};

$(function () {
    $('#tag_cloud a').tagcloud();
});
</script>
