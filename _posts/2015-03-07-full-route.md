---
layout: post
title: SRX100 に full route を食わせる
tags: [routing, juniper]
---

# motivation
検証などでフルルートを食わせてみましょうってのがあるけれども、結局どうやるんだろうと。

# install Python
Mac なので入ってた
{% highlight bash %}
$ python
Python 2.7.5 (default, Mar  9 2014, 22:15:05) 
[GCC 4.2.1 Compatible Apple LLVM 5.0 (clang-500.0.68)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
{% endhighlight %}

# insatall PyPy
入れるといいらしい

[PyPy - Download and install](http://pypy.org/download.html)

真ん中あたりの Mac OS/X binary (64bit) を持ってくる。

# configure SRX
Factory setting から BGP に関するものとかを入れただけ。

{% gist shakemi/56e8939447eef375b729 %}

# advertise full route
1 時間以上かかってる...
{% highlight bash %}
$ ./sbin/exabgp ~/mrtparse/examples/full.conf
{% endhighlight %}

# Reference
* Python で書かれた BGP をおしゃべりするプログラム
	* [Exa-Networks/exabgp](https://github.com/Exa-Networks/exabgp/)
* の使い方とか（ExaBGP のサイトからもリンク貼られてる）
	* [ExaBGPを使ってBGPフル経路を注入](http://okuranagaimo.blogspot.co.uk/2014/11/exabgpbgp.html)
* full route 置き場（Route Views Project から）
	* [Index of /bgpdata](http://archive.routeviews.org/bgpdata/)
* Route Views のファイルを ExaBGP が食える形に変換
	* [YoshiyukiYamauchi/mrtparse](https://github.com/YoshiyukiYamauchi/mrtparse)
