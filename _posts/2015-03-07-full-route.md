---
layout: post
title: SRX100 に full route を食わせる
tags: [routing, juniper]
---

# Motivation
検証などでフルルートを食わせてみましょうってのがあるけれども、結局どうやるんだろうと。

# Install Python
Mac なので入ってた
{% highlight bash %}
$ python
Python 2.7.5 (default, Mar  9 2014, 22:15:05) 
[GCC 4.2.1 Compatible Apple LLVM 5.0 (clang-500.0.68)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
{% endhighlight %}

# Insatall PyPy
入れるといいらしい

[PyPy - Download and install](http://pypy.org/download.html)

真ん中あたりの Mac OS/X binary (64bit) を持ってくる。

# Configure SRX
Factory setting から BGP に関するものとかを入れただけ。

{% gist shakemi/56e8939447eef375b729 %}

# Advertise full route
1 時間以上かかってる...
{% highlight bash %}
$ ./sbin/exabgp ~/mrtparse/examples/full.conf
{% endhighlight %}

# Reference
* [Exa-Networks/exabgp](https://github.com/Exa-Networks/exabgp/)
	* Python で書かれた BGP をおしゃべりするプログラム
* [ExaBGPを使ってBGPフル経路を注入](http://okuranagaimo.blogspot.co.uk/2014/11/exabgpbgp.html)
	* の使い方とか（ExaBGP のサイトからもリンク貼られてる）
* [Index of /bgpdata](http://archive.routeviews.org/bgpdata/)
	* full route 置き場（Route Views Project から）
* [YoshiyukiYamauchi/mrtparse](https://github.com/YoshiyukiYamauchi/mrtparse)
	* Route Views のファイルを ExaBGP が食える形に変換
