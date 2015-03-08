---
layout: post
title: Jekyll で URL の構造を変える
tags: [jekyll]
---

{% include google_analytics.html %}

# Motivation
/:year/:month/:day/:title.html っていう構造が気にくわないので変える

/:year/:month/:day/ の階層に上がれないしね、結局

# Modily _config.yml
permalink に好みの URL structure を書く
{% highlight bash %}
$ git diff 59550d3d6a24e987bb408d8d5d188376c3ca833d a5a73e5882af3fd946e0b215f9a90f1087e7c74b
diff --git a/_config.yml b/_config.yml
index 971a181..838920a 100644
--- a/_config.yml
+++ b/_config.yml
@@ -12,3 +12,4 @@ github_username:  shakemi
 
 # Build settings
 markdown: kramdown
+permalink: /:year-:month-:day-:title.html
{% endhighlight %}

# Reference
* [Permalinks](http://jekyllrb.com/docs/permalinks/)
	* permalink の修正のしかたが書いてある

# Feedback
カスタマイズ性って大事だなぁと
