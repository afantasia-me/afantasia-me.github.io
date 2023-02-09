---
layout: default
title: Stories
---

<ul class="posts">
  {% comment %}
  {% for post in site.posts %}
  {% if post.story %}
  <li><span>{{ post.date | date_to_string }}</span>: <a href="{{ post.url }}" title="{{ post.title }}">{{ post.title }}</a></li>
  {% endif %}
  {% endfor %}
  {% endcomment %}
</ul>
