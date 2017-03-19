---
layout: post
title: 在linux上使用一个比正常情况下“更高”的解析度
date: 2017-03-19
comments: true
archive: false
---
[linux afake a higher resolution in linux]:http://www.joeldare.com/wiki/linux%3afake_a_higher_resolution_in_linux

现在我使用的一台笔记本电脑 在正常情况下，分辨率是 1366*768 的.  
当玩某些游戏，或是使用一些不支持缩放的程序的时候。 界面上的按钮就会跑到屏幕下面去了，当然通过滑动条下拉可以点击到它们，但总是有些不方便的地方.  
这个时候可以使用 xrandr 程序修改下分辨率

{% highlight bash %}
xrandr --output LVDS1 --mode 1024x600 --scale 1.50x1.50 --panning 1536x900
{% endhighlight %}

这个方式只会在当前会话里生效 。

LVDS1 换成 自己的显示器标示 ,可以用 xrandr 查看 , mode 为正常时的分辨率, scale 是缩放比率 ,panning 为最终的“假”分辨率 。

比如你的显示器 正常情况下是 1366x768 ,要 设置成 1.5 倍率

1366 * 1.5 =  2049  
768 * 1.5 = 1152

最终就是

{% highlight bash %}
xrandr --output LVDS1 --mode 1366x768 --scale 1.50x1.50 --panning 2049x1152
{% endhighlight %}

这样才不会导致变形  
如果觉得字体 太小的话，可以 把字号调大 1.5 倍，这样看起来就会比较舒服了.

参考 [linux afake a higher resolution in linux]
