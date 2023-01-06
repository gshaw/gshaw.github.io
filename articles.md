---
title: Articles
permalink: /articles/
---

# {{ page.title }}

<ul>
  {% for post in site.posts %}
    <li>
      <small>{{ post.date | date: "%b %-d  %Y" }}</small>
      <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>
