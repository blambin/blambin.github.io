---
layout: post
title: 在cygwin下安装jekyll
date: 2017-03-10
comments: true
archive: false
---
1. 安装ruby ruby-devel

{% highlight bash %}
apt-cyg install ruby ruby-devel
{% endhighlight %}

2. gem 安装 jekyll 时需要手动安装依赖：
{% highlight bash linenos %}
ruby-devel
libffi-devel
gcc-core
gcc-g++
make
automake
{% endhighlight %}

3.另外就是在我的环境下面 jekyll 会被安装到 ~/bin/下了，需要在 .zshrc 下添加

{% highlight bash %}
export PATH=~/bin/:$PATH
{% endhighlight %}

就可以使用了.
