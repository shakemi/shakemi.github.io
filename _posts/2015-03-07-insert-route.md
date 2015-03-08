---
layout: post
title: full route 食わせるのが時間掛かり過ぎるので API を試す
tags: [routing, juniper]
---

{% include google_analytics.html %}

# Motivation
フルルート食わせるのに 3 時間かかるのでどうにかしたい

# ExaBGP API
conf に process -> run って書くとその program を実行してくれる

{% gist shakemi/a866d877945173412c5d %}

program を Python で書いた
full route の 1 つを program で挿入することにする

{% gist shakemi/024cdd2d81fb67769024 %}

実行結果

{% highlight bash %}
$ ./sbin/exabgp ./api-add-remove.conf 
<snip>
Sat, 07 Mar 2015 14:00:50 | INFO     | 53046  | processes     | Forked process announce-routes
Sat, 07 Mar 2015 14:00:53 | INFO     | 53046  | network       | Connected to peer neighbor 192.168.1.100 local-ip 192.168.1.20 local-as 65000 peer-as 64512 router-id 192.168.1.20 family-allowed in-open (out)
Sat, 07 Mar 2015 14:00:55 | INFO     | 53046  | processes     | Command from process announce-routes : announce attribute next-hop 192.168.1.254 nlri 1.0.132.0/22 
Sat, 07 Mar 2015 14:00:55 | INFO     | 53046  | reactor       | Route added to neighbor 192.168.1.100 local-ip 192.168.1.20 local-as 65000 peer-as 64512 router-id 192.168.1.20 family-allowed in-open : 1.0.132.0/22 next-hop 192.168.1.254
Sat, 07 Mar 2015 14:00:56 | INFO     | 53046  | reactor       | Performing dynamic route update
Sat, 07 Mar 2015 14:00:56 | INFO     | 53046  | reactor       | Updated peers dynamic routes successfully
{% endhighlight %}

SRX 側で受信できてる経路

{% highlight text %}
root> show route    

inet.0: 4 destinations, 4 routes (4 active, 0 holddown, 0 hidden)
+ = Active Route, - = Last Active, * = Both

1.0.132.0/22       *[BGP/170] 00:00:08, localpref 100, from 192.168.1.20
                      AS path: 65000 I
                    > to 192.168.1.254 via fe-0/0/0.0
192.168.1.0/24     *[Direct/0] 00:29:35
                    > via fe-0/0/0.0
192.168.1.1/32     *[Local/0] 00:32:21
                      Reject
192.168.1.100/32   *[Local/0] 00:32:13
                      Local via fe-0/0/0.0
{% endhighlight %}

# Reference
* [Large Configuration File · Exa-Networks/exabgp Wiki](https://github.com/Exa-Networks/exabgp/wiki/Large-Configuration-File)
	* full route 食わせるときとかの行数の多い conf の場合には秘密の API を使うといいよ
* [Controlling ExaBGP : possible options for process · Exa-Networks/exabgp Wiki](https://github.com/Exa-Networks/exabgp/wiki/Controlling-ExaBGP-:-possible-options-for-process)
	* conf に書ける process についての説明
	* run 以外にもいくつかあるらしい
* [Internet Exchanges : Do we need a new Route Server?](http://thomas.mangin.com/data/pdf/Euro-IX%2024%20-%20Mangin%20-%20ExaBGP.pdf)
	* ちょっと参考になった Euro-IX の資料

# Feedback
NLRI ってこういうことだったのね
