---
layout: post
title: Fixing Python's insecure platform warning
tags: [python, linux]
---

Here’s how to fix that nagging InsecurePlatformWarning warning in Python.

<!--more-->

### The issue

> InsecurePlatformWarning: A true SSLContext object is not available. This prevents urllib3 from configuring SSL appropriately and may cause certain SSL connections to fail. For more information, see [https://urllib3.readthedocs.org/en/latest/security.html#insecureplatformwarning](https://urllib3.readthedocs.org/en/latest/security.html#insecureplatformwarning).

Assuming you have pip for python installed, read on...

### Ubuntu 14.04 fix

{% highlight bash %}
sudo apt-get install libffi-dev libssl-dev
sudo pip install -U requests[security]
{% endhighlight %}
