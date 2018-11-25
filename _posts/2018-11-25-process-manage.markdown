---
layout: post
title:  "浅谈Linux程序管理"
date:   2018-11-25 20:30:00
categories: Linux
tags: linux process centos
---

* content
{:toc}

### 进程查看

进程查看常见的命令有：ps，top

* ps：将某个时间点的进程运行情况选取出来

    ps aux  <== 查看系统所有进程数据
        
    ps aux | grep `service name`   <== 显示具体某个服务的进程信息
    
* top： 动态查询进程的变化

    top   <==  查看所有进程的变化情况
    
    top -d `TIME` -p `PID`   <== `TIME`秒刷新一次只查看进程ID`PID`的进程
    
### 进程的管理

进程管理的命令：kill，killall

* kill：通过PID管理进程 `kill -signal PID`

    kill -9 PID  <== 强制中断一个进程的进行
    
    kill -1 PID  <== 启动被终止的进程
    
*  killall：通过进程名称管理进程 `killall -signal [command name]`
    
    比如：killall -9 httpd   强制终于所有以httpd启动的进程
    
### 系统资源的查看

* 查看内存使用情况：free
    
    free -m  <== 查看内存使用情况，使用单位MB
    
* 查看系统与内核信息：uname

    uname -a  <== 输出系统的基本信息
    
* 查看CUP使用情况：vmstat

    vmstat 1 3  <== 统计目前主机CPU状态，每秒一次，共3次
    
    vmstat -d <== 磁盘的读写状态
    
### 网络管理

网络管理命令：netstat

    netstat -[atunlp]
    
        -a: 将系统上所有的连接、监听、Socket数据都列出来
        -t: 列出所有tcp网络数据包
        -u: 列出所有udp网络数据包
        -n: 端口号
        -l: 正在监听的网络
        -p: 进程PID
        
        



    
    

    




