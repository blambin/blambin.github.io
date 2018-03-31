---
layout: post
title:  记录配置 Https SSL证书 的一个坑
date: 2018-03-31
comments: true
archive: false
---

[android-doesnt-trust-the-certificat]: https://community.letsencrypt.org/t/android-doesnt-trust-the-certificate/16498

的配置文件是这样的：

{% highlight bash %}
...
    SSLCertificateFile /etc/letsencrypt/live/blambin.org/fullchain.pem
    SSLCertificateKeyFile /etc/letsencrypt/live/blambin.org/privkey.pem
</VirtualHost>

{% endhighlight %}

在 windows ,linux 上完全没有问题 ，但是android上就提示证书不正确的问题

SSLCertificateFile 被我配置成了证书链的那个文件 ，同时在firefox的证书详情里也看到确实证书链没有问题，但是这在android上是有问题的

改成下面这样的配置就可以了

{% highlight bash %}
...
    SSLCertificateFile /etc/letsencrypt/live/blambin.org/cert.pem
    SSLCertificateKeyFile /etc/letsencrypt/live/blambin.org/privkey.pem
    SSLCertificateChainFile /etc/letsencrypt/live/blambin.org/chain.pem
</VirtualHost>
{% endhighlight %}

参考:

*  [android-doesnt-trust-the-certificat]
