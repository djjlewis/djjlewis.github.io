---
layout: page
---

<h1 class="page-heading">Conference Talks</h1>

<p>This area contains a list of notes I have taken for various technical conference talks. I find the act of writing
    helps solidify the content in my own mind and also helps as a handy personal repostiory of key ideas I can look back
    on. Hopefully others will find it of some use!</p>

<p>Special thanks of course goes to all the speakers for their knowledgeable contributions in the first place.</p>

<ul class="post-list">
    {% for item in site.conference-talks %}
    <a href="{{ item.url | prepend: item.baseurl }}">{{ item.title }}</a>
    {% endfor %}
</ul>