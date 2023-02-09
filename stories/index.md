---
layout: default
title: Stories
---

<ul class="posts">
  {% assign stories = site.posts | where: "story" %}
  {% for post in stories %}
  <li><span>{{ post.date | date_to_string }}</span>: <a href="{{ post.url }}" title="{{ post.title }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>