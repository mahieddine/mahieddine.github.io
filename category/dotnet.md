---
layout: posts_by_category
categories: dotnet
title: .NET
permalink: /category/dotnet
---

<p>Posts in category "dotnet" are:</p>

<ul>
  {% for post in site.categories.dotnet %}
    {% if post.url %}
        <li><a href="{{ post.url }}">{{ post.title }}</a></li>
    {% endif %}
  {% endfor %}
</ul>