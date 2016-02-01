---
layout: post
title: How to create large temp files quickly (for testing purposes)
tags: [bash]
---

Quick and dirty way to just create a 10GB temp file for testing e.g. network transfer speeds.

<!--more-->

### Linux

{% highlight bash %}
fallocate -l 10G temp_10GB_file
{% endhighlight %}

### Windows

The file size is defined in bytes. Use Google to do the conversion if you’re unsure.

{% highlight bat %}
fsutil file createnew temp_10GB_file 10000000000
{% endhighlight %}


### Mac OS X

{% highlight bash %}
mkfile -n 10g temp_10GB_file
{% endhighlight %}
