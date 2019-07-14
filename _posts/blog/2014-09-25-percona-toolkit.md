---
layout: post
title: percona-toolkit工具的使用
description: mysql数据库一致性校验
category: blog
---

## 安装percona-toolkit-2.2.10-1

下载percona-toolkit-2.2.10-1

    # wget http://www.percona.com/downloads/percona-toolkit/LATEST/RPM/percona-toolkit-2.2.10-1.noarch.rpm

首先安装依赖组件:

    # yum -y install perl-DBI  perl-DBD-MySQL  perl-TermReadKey perl-IO-Socket-SSL perl-DBD-MySQL

    # rpm -ivh percona-toolkit-2.2.10-1.noarch.rpm

## 修改mysql数据库配置文件

my.cnf 文件:

    [client]
    default-character-set = utf8  //防止乱码
    [mysqld]
    binlog_format=STATEMENT
重启mysql数据库

## 添加mysql用户权限

在主库上操作，恢复数据库的用户权限要最高注：bak 账户权限要最高

    [root@centos64-a3 ~]#  pt-table-checksum --nocheck-replication-filters --replicate=baseA.checksums --databases=baseA --tables=area h=127.0.0.1,u=bak,p=bak,P=3306;

 检查结果如下：

    TS               ERRORS  DIFFS  ROWS  CHUNKS  SKIPPED  TIME   TABLE
    05-08T16:21:06      0      1      4      1       0     0.012  baseA.person

* TS            ：完成检查的时间。
* ERRORS        ：检查时候发生错误和警告的数量。
* DIFFS         ：0表示一致，1表示不一致。当指定--no-replicate-check时，会一直为0，当指定--replicate-check-only会显示不同的信息。
* ROWS          ：表的行数。
* CHUNKS        ：被划分到表中的块的数目。
* SKIPPED       ：由于错误或警告或过大，则跳过块的数目。
* TIME          ：执行的时间。
* TABLE         ：被检查的表名。

恢复数据 从master 恢复到 slave
    
    [root@centos64-a3 ~]# pt-table-sync --replicate=baseA.checksums h=127.0.0.1,u=bak,p=bak,P=3306 h=192.168.3.124,u=bak,p=bak,P=3306 --print 

打印出结果,并执行结果
    
    [root@centos64-a3 ~]# pt-table-sync --replicate=baseA.checksums h=127.0.0.1,u=bak,p=bak,P=3306 h=192.168.3.124,u=bak,p=bak,P=3306 --print --execute  

