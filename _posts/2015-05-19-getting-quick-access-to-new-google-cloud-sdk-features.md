---
layout: post
title: Getting quick access to new Google Cloud SDK features
tags: [linux, bash]
---

There is a two-week delay before gsutil gets updated with the latest and greatest. If you want to try the new stuff out, pip install the SDK!

<!--more-->

{% highlight bash %}
sudo yum install gcc openssl-devel python-devel python-setuptools libffi-devel
sudo yum install python-pip
sudo pip install -U gsutil
{% endhighlight %}

Then execute gsutil like this:

{% highlight bash %}
/usr/bin/gsutil
{% endhighlight %}

To access beta (or even alpha) features of gcloud, execute gcloud like this:

{% highlight bash %}
gcloud beta compute instances ...
{% endhighlight %}
