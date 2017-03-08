---
title: Course Notes
layout: default

---

<h1>Here are the notes</h1>
<ul>
{% for course in site.courses %}
    <li><a href="{{ site.baseurl }}{{ course.url }}">{{ course.title }}</a></li>
{% endfor %}
</ul>