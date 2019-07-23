---
layout: page
---

<h1 class="page-heading">Guides</h1>

<p>A collection of technical guides</p>

<ul class="post-list">
    {% for item in site.guides %}
    <a href="{{ item.url | prepend: item.baseurl }}">{{ item.title }}</a>
    {% endfor %}
</ul>