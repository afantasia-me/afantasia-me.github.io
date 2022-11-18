---
layout: default
title: Home
---

# Welcome to the Atelier Fantasia

> Unabashadly infrequent work in progress.

For updates on writing, see my <a rel="me" href="https://masto.ai/@afantasia">writing mastodon</a>.
For socialising or the odd gamedev update, see <a rel="me" href="https://mastodon.gamedev.place/@babel">@babel</a>.

---

## Recent Posts

<ul class="posts">
  {% for post in site.posts :5 %}
  <li><span>{{ post.date | date_to_string }}</span>: <a href="{{ post.url }}" title="{{ post.title }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>

