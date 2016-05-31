---
layout: page
title: Archive
permalink: /archive/
---

<h1>Archive: {{ page.title }}</h1>
<ul>
  {% if page.month %}
    {% capture pagemonth %} {{ page.year | append: '-' | append: page.month }} {% endcapture %}
    {% for post in site.posts %}
      {% capture postmonth %} {{ post.date | date: '%Y-%m' }} {% endcapture %}
      {% if postmonth == pagemonth %}
        <li class="post">
          <p class="meta">
            by <a href="{{ post.author-link }}">{{ post.author }}</a>
            on <a href="{{ post.date | date: '/%Y/%m/' }}">{{ post.date | date: "%b %-d, %Y" }}</a>
          </p>
          <h3><a href="{{ post.url }}">{{ post.title }}</a></h3>
          <p class="tags">
            {% for tag in post.tags %}
              <a href="{{ tag | downcase | replace: ' ', '-' | prepend:'/tags/' }}">{{ tag }}</a>
            {% endfor %}
          </p>
        </li>
      {% endif %}
    {% endfor %}
  {% elsif page.year %}
    