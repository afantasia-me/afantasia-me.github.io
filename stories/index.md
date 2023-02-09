---
layout: default
title: Stories
---

<ul class="posts">
  {% for post in site.stories %}
  <li><span>{{ post.date | date_to_string }}</span>: <a href="{{ post.url }}" title="{{ post.title }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>
