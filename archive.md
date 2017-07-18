---
layout: page
title: Archive
---

{% include filter_by_tag.html %}

<style class="mono">{% for post in site.posts %}{{ post.date | date_to_string }}</style> &raquo; [ {{ post.title }} ]({{ post.url }})  
{% endfor %}
