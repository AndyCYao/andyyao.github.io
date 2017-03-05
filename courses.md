---
title: Courses I have taken so far
layout: default
permalink: /courses/
---

<h1>Here are the notes</h1>
<ul>
{% for course in site.courses %}
    <li><a href="{{ site.baseurl }}{{ course.url }}">{{ course.title }}</a></li>
{% endfor %}
</ul>