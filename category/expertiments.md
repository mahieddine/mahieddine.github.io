---
layout: posts_by_category
categories: experiments
title: Experiments
permalink: /category/experiments
---

<p>Posts in category "experiments" are:</p>

<ul>
  {% for post in site.categories.experiments %}
    {% if post.url %}
        <li><a href="{{ post.url }}">{{ post.title }}</a></li>
    {% endif %}
  {% endfor %}
</ul>