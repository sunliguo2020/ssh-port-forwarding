---
typora-root-url: pic
---

项目背景：
	在家中电脑访问公司nas中的mysql数据库。
	
项目环境：
	家中：
		win10系统
	公司：
		倍控小主机运行Debian	ip:192.168.1.21
		TNAS运行着mysql数据库  ip：192.168.1.207 port：3306
	阿里云：
		centos 	blog.sunliguo.com
	家中win10和公司都能访问aliyun的服务器。
项目需求：
	在家中能访问公司的mysql数据库。
	
步骤：
	1、在Debian中实现实现远程端口转发。

1.1 Debian中安装autossh，并将公钥保存到阿里云的centos上。


	1.2 autossh -M 53305 -NR 127.0.0.1:53306:192.168.1.207:3306 sunliguo@blog.sunliguo.com -f -p 22
		其中192.168.1.207为mysql数据库的ip，3306为端口号。Debian和数据库在同一个网段中，可以直接访问。		


​	
			在阿里云上：
			[root@aliyun ssh]# netstat -nltp
			Active Internet connections (only servers)
			Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name
			tcp        0      0 127.0.0.1:53305         0.0.0.0:*               LISTEN      529425/sshd: sunlig
			tcp        0      0 127.0.0.1:53306         0.0.0.0:*               LISTEN      529425/sshd: sunlig
			现在在aliyun上访问53306就可以访问mysql数据库了。


2、家中win10 本地端口转发。

​	安装MobaXterm

​	2.1：Tools ->MobaSSHTunel(port forwarding)

![image-20220604185718562](D:\桌面\ssh端口转发\pic\image-20220604185718562.png)

![2022-06-04_182217](D:\桌面\ssh端口转发\2022-06-04_182217.png)![2022-06-04_182217](/2022-06-04_182217.png)