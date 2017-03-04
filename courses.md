---
title: Courses I have taken so far
layout: default
permalink: /courses/
---
<h1>Test  Notes from the courses I have taken so far </h1>
<ul>
{% for page in site.courses %}
    <li><a href="{{ site.baseurl }}{{ page.url }}">{{ page.title }}</a></li>
{% endfor %}
</ul>