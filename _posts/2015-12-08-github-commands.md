---
layout: post
title: Github commands
tags: [github]
---

Common commands I'm using all the time, but keep forgetting the syntax for.

<!--more-->

## Pull and overwrite any local changes

{% highlight bash %}
git fetch --all
git reset --hard origin/master
{% endhighlight %}

Or if you're on a different branch:

{% highlight bash %}
git reset --hard origin/your_branch
{% endhighlight %}

## Revert repository to previously pushed commit

{% highlight bash %}
git reset 306410193e675ac9486fea07a1de04971f51e1a4
git push --force
{% endhighlight %}
