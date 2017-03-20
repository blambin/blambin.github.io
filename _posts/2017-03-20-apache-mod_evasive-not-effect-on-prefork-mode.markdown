---
layout: post
title: apache 上使用 mod_evasive 没有效果
date: 2017-03-20
comments: true
archive: false
---
[mod_evasive behind HAPROXY]:http://serverfault.com/questions/233092/mod-evasive-behind-haproxy
[How To Protect Against DoS and DDoS with mod_evasive for Apache on CentOS 7]:https://www.digitalocean.com/community/tutorials/how-to-protect-against-dos-and-ddos-with-mod_evasive-for-apache-on-centos-7

最近在使用apache的一个防ddos 的mod时遇到了一个问题，安装完模组运行的时候 通过查看 httpd 日记 发现时而能防住有时不行。  
像是随机可以防住DDos

{% highlight log %}
*.*.81.36 - - [20/Mar/2017:16:17:14 +0800] "GET /admin.php HTTP/1.1" 200 1207 "-" "-1 Firefox/52.0"
*.*.81.36 - - [20/Mar/2017:16:17:15 +0800] "GET /admin.php HTTP/1.1" 403 292 "-" "-1 Firefox/52.0"
*.*.81.36 - - [20/Mar/2017:16:17:34 +0800] "GET /admin.php HTTP/1.1" 403 292 "-" "-1
*.*.81.36 - - [20/Mar/2017:16:17:38 +0800] "GET /admin.php HTTP/1.1" 403 292 "-" "-1 Firefox/52.0"
*.*.81.36 - - [20/Mar/2017:16:17:38 +0800] "GET /admin.php HTTP/1.1" 403 292 "-" "-1 Firefox/52.0"
*.*.81.36 - - [20/Mar/2017:16:17:38 +0800] "GET /admin.php HTTP/1.1" 200 1207 "-" "-1
{% endhighlight %}

找了半天发现是因为 apache默认使用的 prefork 运行模式。
在这个模式下apache的多个进程之间没有办法共享计数器数据，导致计算出的结果不正确，如果换用 apache的另外两个工作模式的话，效果会好一点，但还是没有办法彻底解决问题。  
除非使用单进程？

对于这个mod的默认配置，MaxClient=50,意思就是单个进程的最大请求数上限为 50。
多进程的情况下 如果单一进程的请求结束之后，这个进程就会被杀死，所以在某些情况下，mod_evasive根本没有效果。

参考:

*  [How To Protect Against DoS and DDoS with mod_evasive for Apache on CentOS 7]
*  [mod_evasive behind HAPROXY]
