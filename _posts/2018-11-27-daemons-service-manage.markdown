---
layout: post
title:  "简单认识系统服务"
date:   2018-11-27 20:30:00
categories: Linux
tags: linux daemon centos
---

* content
{:toc}

系统为了某种功能必须要提供一些服务（不论是系统本身还是网络方面），这个服务就称为**service**。但是service的提供总是需要进程的运行，所以实现这个service的程序就称为**daemon**。两者可相似的认识是相同的。

### daemon的分类

依照daemon的启动与管理方式来区分，基本上可以将daemon分为**独立启动**的**stand alone**，与通过一个super daemon来统一来管理的服务两大类。
我这边主要来介绍stand_alone。

* stand_alone：此daemon可以自行单独启动服务（常见的HTTP，FTP服务）

    stand_alone启动并加载内存后就一直占用内存与系统资源，最大的优势就是：因为是一直存在内存内持续的提供服务，因此对于发生客户端的请求时，stand_alone的daemon响应速度较快。

* super daemon：一个特殊的daemon来统一管理（常见的telent服务）

### daemon常见相关文件位置

文件说明 | 文件地址
------ | ------
查看服务与端口文件 | /etc/servcies
服务启动脚本文件  | /etc/init.d/*
各服务的初始化环境配置文件 | /etc/sysconfig/*
各服务各自的配置文件 | /etc/*
各服务产生的数据库 | /var/lib/*
各服务的程序PID记录处 | /var/run/*

### stand alone的启动方式

* 通过/etc/init.d/*启动

    /etc/init.d/[service name] {start|stop|status|restart|condrestart}

        /etc/init.d/syslog status    查看syslog这个daemon的状态

        /etc/init.d/syslog restart    重新启动syslog这个服务

* 通过service命令启动

        service [service name] {start|stop|status|restart|condrestart}

        service syslog restart    重新启动syslog这个服务


        service --status-all   显示目前系统上的所有服务状态

### 服务的防火墙管理 xinetd，TCP Wrappers

任何以[xinetd](https://zh.wikipedia.org/wiki/Xinetd)管理的服务（日常见到的绝大部分服务）都可以通过/etc/hosts.allow和/etc/hosts.deny来设置防火墙。
顾名思义/etc/hosts.allow配置的就是允许访问服务的主机，/etc/hosts.deny配置的就是禁止访问服务的主机。

* 配置文件语法

        <service (program name)> : <IP, domain, hostname> : <action>

        <服务         (即程序名称)> : <  IP 或 域名 或 主机  > : <操作 allow 或 deny>

    写在hosts.allow文件当中的IP与网段默认是allow的，写在hosts.deny中的IP，网段默认是deny的，所以第三列可以省略。

    这两个文件的判断依据：以/etc/hosts.allow为优先，若分析到的IP或网段并没有记录在/etc/hosts.allow，则以/etc/hosts.deny来判断。

    文件中service（program name）是**启动该服务的程序**的文件名，举例说，/etc/init.d/sshd这个script，实际启动ssh服务的是sshd这个程序，所以需要service是sshd

* <service (program name)>, <IP, domain, hostname>的特殊参数解释

    ALL：代表全部的program_name或者是IP都接受的意思，比如 ALL:ALL:allow

    LOCAL：代表本机的意思，比如 ALL:LOCAL:deny

    UNKNOWN：代表不知道的IP或者domain或者服务时

    KNOWN：代表为可解析的IP，domain等信息

* 实例

    只允许140.116.0.0/255.255.0.0 与 203.71.39.0/255.255.255.0这两个域，以及203.71.38.123这个主机可以访问我们的rsync服务

    此外，其他IP全部都挡掉

        # vim /etc/hosts.allow

        rsync: 140.116.0.0/255.255.0.0

        rsync: 203.71.39.0/255.255.255.0

        rsync: 203.71.38.123

        rsync: LOCAL


        # vim /etc/hosts.deny

        rsync: ALL


### 开机启动

* 查看开机启动项

        chkconfig --list [service name]   <== service name 服务名称（可不填）

* 设置开机启动项

        chkconfig [--add|--del] [service name]








