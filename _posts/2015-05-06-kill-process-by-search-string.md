---
layout: post
title: Kill process by search string
tags: [linux, bash]
---

In Linux, you can kill all processes by name (or by username etc) using something like this:

{% highlight bash %}
kill -9 $(ps aux | grep 'some_process_name' | awk '{print $2}')
{% endhighlight %}
