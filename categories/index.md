---
title: 分类
layout: page
---

<div id='tag_cloud'>
{% for cat in site.categories %}
<a href="#{{ cat[0] }}" title="{{ cat[0] }}" rel="{{ cat[1].size }}">{{ cat[0] }} ({{ cat[1].size }})</a>
{% endfor %}
</div>

<div class="listing">
  <ul>
  {% for cat in site.categories %}
  <div class="listing-classify">
    <li class="listing-classify-tag" id="{{ cat[0] }}">{{ cat[0] }}</li>
    <div class="listing-classify-post">
    {% for post in cat[1] %}
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
