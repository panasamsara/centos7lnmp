# 虚拟机装CentOS7.2 以及php7.2 nginx1.12 mysql5.7安装配置

------

装centos就不说了，直接跳过。网上教程很多，这里主要讲php相关环境的安装，参考了很多，具体我会在后面都贴出来。
装好后联网相关的设置可以看这里
https://www.cnblogs.com/cc11001100/p/7137896.html

------
## 一、首先php nginx mysql整个流程可以看这个
虚拟机Linux Centos7搭建web环境（LNMP）
https://blog.csdn.net/JayceDeng/article/details/78886038

------
## 二、第一步：修改 yum 源
### 1.[root@localhost ~]# rpm -Uvh https://dl.Fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
### 2.[root@localhost ~]# rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm
### 3.[root@localhost ~]# rpm -Uvh  http://dev.mysql.com/get/mysql57-community-release-el7-9.noarch.rpm

------
## 三、参照他的顺序，先装nginx
可以直接参考上面整个流程里面的，但是里面配置的说明很少，只说了要改防火墙，我又参考了别的地方。

### 1.这里可以看nginx用的哪个配置文件
https://www.cnblogs.com/zhangxintong1314/p/6545061.html


### 2.这文章里第4步，详细说了修改哪个文件以及怎么改
https://www.cnblogs.com/peteremperor/p/6740725.html

------

## 四、再装mysql

同样，他写的也比较详细，可以依照着安装。至于配置，依旧可以参照别的地方
### 1.装完之后参照这里第7步，修改密码（因为mysql5.7，默认生成了随机密码）
http://www.jb51.net/article/116032.htm

### 2.这里修改防火墙，这样可以远程连虚拟机里的数据库了
http://www.jb51.net/article/124228.htm?utm_source=debugrun&utm_medium=referral


## 五、最后装php7.2
流程上依旧可以照着那整个流程走，不过他装的7.1
### 1.我装的7.2看下面
https://blog.csdn.net/hu_zhe_kan/article/details/79368169
装完后，再跟着那整个流程改php相关配置

### 2.不过其中有一个可以暂时不改，就是open_basedir = .:/tmp/ 这个，详细介绍可以看这里
https://www.oschina.net/question/878142_106780
防止跨站攻击之类的，反正虚拟机，不用管，因为设置不好的话，会导致主机访问虚拟机html文件可以，但是php文件就显示Access denied，权限不够。线上环境的话，这个就确实应该设置了


## 六、最后全部弄完应该就可以了
在nginx的html目录里，放一个phpinfo.php, 
里面内容是
```php
<?php phpinfo(); ?>
```

然后就可以在浏览器 访问： 虚拟机ip/phpinfo.php，看到php信息了

