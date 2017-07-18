---
layout: page
title: Archive
---

{% include filter_by_tag.html %}

{% for post in site.posts %}{<style class="mono">{ post.date | date_to_string }</style>} &raquo; [ {{ post.title }} ]({{ post.url }})  
{% endfor %}
