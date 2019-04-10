## redis在linux环境下安装

注意:linux环境下安装redis需要gcc环境. 需要提前安装gcc. 本文在在CentOS 6.5环境下安装
 
安装命令: `yum install gcc`

### 安装步骤

在linux环境联网环境下,可通过命令下载redis-stale版本. 如果linux环境不能连接外网,可访问[redis官网](https://redis.io/download)下载redis的linux版本安装包. 
  

1. 获取redis稳定版本：`wget http://download.redis.io/redis-stable.tar.gz`
2. 解压：`tar -xvf redis-stable.tar.gz`
3. 切换目录：	`cd redis-statle`
4. 编译：`make`
5. 安装：`make install`

安装成功后redis会将可执行文件放于/usr/local/bin目录下

### 安装成功页面
切换到`cs /usr/local/bin`目录下，执行`./redis-server`启动,启动成功后如下图

![redis启动成功](https://raw.githubusercontent.com/zengzhiwei12138/software_install/master/image/redis启动成功.png "redis启动成功")

### 常见问题
- 若出现如下提示，则说明未安装gcc，使用命令安装gcc：yum install gcc
    
    	[root@localhost redis-2.8.17]# make
    	cd src && make all
    	make[1]: Entering directory `/root/redis-2.8.17/src‘
    	CC adlist.o
    	/bin/sh: cc: command not found
    	make[1]: *** [adlist.o] Error 127
    	make[1]: Leaving directory `/root/redis-2.8.17/src‘
    	make: *** [all] Error 2

- 若出现如下提示，则将make改为make MALLOC=libc，推测是因为编译库的问题。

	    [root@localhost redis-2.8.17]# make
	    cd src && make all
	    make[1]: Entering directory `/root/redis-2.8.17/src‘
	    CC adlist.o
	    In file included from adlist.c:34:
	    zmalloc.h:50:31: error: jemalloc/jemalloc.h: No such file or directory
	    zmalloc.h:55:2: error: #error "Newer version of jemalloc required"
	    make[1]: *** [adlist.o] Error 1
	    make[1]: Leaving directory `/root/redis-2.8.17/src‘
	    make: *** [all] Error 2

### 参考文献

[redis安装及常见问题](https://blog.csdn.net/wzygis/article/details/51705559)