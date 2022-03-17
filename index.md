---
layout: default
title: "Sam Ettinger"
---

## Sam Ettinger

This is where my small one-off projects will go, I suppose.

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.permalink }}">{{ post.title }}</a>
      <p>{{ content }}</p>
    </li>
  {% endfor %}
</ul>