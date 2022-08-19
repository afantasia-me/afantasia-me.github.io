---
layout: default
title: Home
---

# Atelier Fantasia

> Unabashadly infrequent work in progress.

My usual pseudonym is A. Fantasia (stylised: aFantasia), while my online handle is babel.
- A. Fantasia is a self-reference. Not hard to figure out.
- babel is after Jorge Luis Borges, sadly not Douglas Adams. Simply not confident as a translator, I'm afraid!

I read books 📚 and drink tea 🍵.

You can sometimes find me:

- Writing: [aFantasia](https://archiveofourown.org/users/aFantasia)
  + Writing bird app: [@aFantasia__](https://twitter.com/aFantasia__)
- Public bird app: babel [@StoryStratos](https://twitter.com/StoryStratos)
- On discord: babel#0001

I thank [Sangled](https://twitter.com/sangled) for their wonderful picrew (now sadly 404'd), used for pfp.

---

## Recent Posts

<ul class="posts">
  {% for post in site.posts :5 %}
  <li><span>{{ post.date | date_to_string }}</span> >> <a href="{{ post.url }}" title="{{ post.title }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>
