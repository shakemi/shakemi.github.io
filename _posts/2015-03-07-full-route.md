---
layout: post
title: SRX100 に full route を食わせる
tags: [routing, juniper]
---

# Reference
* Python で書かれた BGP をおしゃべりするプログラム
	* [Exa-Networks/exabgp](https://github.com/Exa-Networks/exabgp/)
* の使い方とか（ExaBGP のサイトからもリンク貼られてる）
	* [ExaBGPを使ってBGPフル経路を注入](http://okuranagaimo.blogspot.co.uk/2014/11/exabgpbgp.html)
* full route 置き場（Route Views Project から）
	* [Index of /bgpdata](http://archive.routeviews.org/bgpdata/)
* Route Views のファイルを ExaBGP が食える形に変換
	* [YoshiyukiYamauchi/mrtparse](https://github.com/YoshiyukiYamauchi/mrtparse)

# install Python
Mac なので入ってた
{% highlight bash %}
$ python
Python 2.7.5 (default, Mar  9 2014, 22:15:05) 
[GCC 4.2.1 Compatible Apple LLVM 5.0 (clang-500.0.68)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
{% endhighlight %}

# configure SRX
Factory setting から BGP に関するものとかを入れただけ。

{% gist shakemi/56e8939447eef375b729 %}

# advertise full route
1 時間以上かかってる...
{% highlight bash %}
$ ./sbin/exabgp ~/mrtparse/examples/full.conf
{% endhighlight %}
