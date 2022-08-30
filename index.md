---
layout: default
title: Home
---

# Welcome to the Atelier Fantasia

> Unabashadly infrequent work in progress.

---

## Recent Posts

<ul class="posts">
  {% for post in site.posts :5 %}
  <li><span>{{ post.date | date_to_string }}</span>: <a href="{{ post.url }}" title="{{ post.title }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>
