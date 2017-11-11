---
layout: post
title: "zookeeper的搭建"
date: 2017-11-11
description: "zookeeper的搭建"
tag: 工具
---   

# Zookeeper集群的搭建
## 前提条件
```
三个zookeeper实例。Zookeeper也是java开发的所以需要安装jdk。
1、Linux系统
2、Jdk环境。
3、Zookeeper。
```
```
1.jdk
2.把Zookeeper安装包上传到Linux
3.解压 tar -zxf zookeeper-3.4.6.tar.gz 
4.复制到想安装集群的目录 在usr/local下创建一个solrcloud目录（解压后的文件夹，3份）
	分别命名为Zookeeper1、2、3
mkdir /usr/local/solrcloud
mv zookeeper-3.4.6 /usr/local/solrcloud/zookeeper1
/usr/local/solrcloud
cp -r zookeeper1/ zookeeper2
cp -r zookeeper1/ zookeeper3
```
# 配置zookeeper
```
	1.在每个zookeeper文件夹下创建一个data目录
	/usr/local/solrcloud/zookeeper1----------》mkdir data
	2.在data文件夹下创建一个文件名称为myid,文件的内容就是此zookeeper的编号1、2、3
	在data下，echo 1 >> myid
	[root@localhost solrcloud]# mkdir zookeeper2/data
	[root@localhost solrcloud]# echo 2 >> zookeeper2/data/myid
	
	[root@localhost solrcloud]# mkdir zookeeper3/data
	[root@localhost solrcloud]# echo 3 >> zookeeper3/data/myid
配置，在/usr/local/solrcloud/zookeeper1/conf下把
	cp zoo_sample.cfg zoo.cfg  复制一份
	修改zoo.cfg的配置
	dataDir=/usr/local/solrcloud/zookeeper1/data（创建的data目录全路径）
	clientPort=2181（客户端的端口号）
	添加(集群中节点的信息，包括ip地址及投票、选举的端口)：
	server.1=192.168.148.132:2881:3881
	server.2=192.168.148.132:2882:3882
	server.3=192.168.148.132:2883:3883
```
![](/images/mybatisnxgc/zookeepera.jpg)
## 同理2和3也要改
![](/images/mybatisnxgc/zookeeperb.jpg)
![](/images/mybatisnxgc/zookeeperc.jpg)
```
启动zookeeper
	在bin目录下
	[root@localhost bin]# ./zkServer.sh start
关闭
	./zkServer.sh stop
查看状态：./zkServer.sh status
```
![](/images/mybatisnxgc/zookeeperd.jpg)