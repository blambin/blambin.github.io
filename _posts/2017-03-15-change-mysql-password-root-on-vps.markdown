---
layout: post
title: 更改mysql的root密码在vps上
date: 2017-03-15
comments: true
archive: false
---
[官方的办法]:https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html
[phpmyadmin]:https://www.phpmyadmin.net/

1.在vps上执行命令进入到mysql的后台界面: mysql -u root -p ,用[官方的办法][]只是把本地的密码改了，通过网络访问还是使用旧的密码.
因为之前都是用root帐号启动mysql的。mysql帐号都无法运行 mysqld_safe --init-file

2.使用
{% highlight mysql %}
SET PASSWORD FOR 'root'@'localhost' = PASSWORD('MyNewPass');
{% endhighlight %}
命令后只是服务器本地上的密码被修改了，通过远程访问的还是使用的旧密码。

3.通过这个更新语句把root用户在所有机器上连接过来的帐号密码都改掉(包括从网络上连接过来的).
{% highlight mysql %}
UPDATE mysql.user
    SET Password = PASSWORD('MyNewPass'), password_expired = 'N'
    WHERE User = 'root' ;
FLUSH PRIVILEGES;
{% endhighlight %}

4.如果有安装 [phpmyadmin] 话，通过网页修改会容易得多了
