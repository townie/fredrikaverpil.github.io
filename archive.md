---
layout: page
title: Archive
---

{% include filter_by_tag.html %}

{% for post in site.posts %}<em class="mono">{{ post.date | date_to_string }}</em> &raquo; [ {{ post.title }} ]({{ post.url }})  
{% endfor %}
