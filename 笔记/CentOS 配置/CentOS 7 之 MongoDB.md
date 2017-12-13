# CentOS 7 之 MongoDB

> CentOS 7.3 64 位 root权限

[TOC]



## 安装

```shell
# 下载
$ wget https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-rhel70-3.4.9.tgz
# 解压
$ tar -zxvf mongodb-linux-x86_64-rhel70-3.4.9.tgz
# 移动
$ mv mongodb-linux-x86_64-rhel70-3.4.9 /usr/local/mongodb
```

安装路径：`/usr/local/mongodb ` 

现在还无法运行 *MongoDB* ，因为缺少数据储存路径等相关配置。

## 命令

可执行文件储存在 `/usr/local/mongodb/bin` 路径

```shell
# 启动服务
$ mongod -f ./mongodb.conf
# 打开shell
$ mongo
```

## 配置

### 配置文件

在 `/usr/local/mongodb/bin` 路径下创建 `mongodb.conf` 

```shell
$ vim /usr/local/mongodb/bin/mongodb.conf
# 键入 i 插入配置
# 端口(默认端口)
port=27017
# 访问IP 
bind_ip=0.0.0.0
# 日志路径
logpath=/usr/local/mongodb/log/mongodb.log
# 启动日志不追加,太过庞大
logappend=false
# 设置mongodb的db路径
dbpath=/usr/local/mongodb/data/db
# 后台驻留(守护)进程服务运行
fork=true
# 键入 Esc 键；输入 :wq 即可
```

### 创建数据储存路径等

**注意：** 路径需要与配置里的相同

```shell
# 创建数据存储文件
$ mkdir /usr/local/mongodb/data
$ mkdir /usr/local/mongodb/data/db
# 创建日志文件
$ mkdir /usr/local/mongodb/log
$ touch /usr/local/mongodb/log/mongodb.log
```

现在可以启动 *mongodb* 服务了

### 自启动

```shell
# 注意配置文件路径
$ vim /etc/rc.d/rc.local
# 在最后增加一行
/usr/local/mongodb/bin/mongod –-config /usr/local/mongodb/bin/mongodb.conf
```

### 配置环境变量

```shell
$ vim /etc/profile
export MGDB_HOME=/usr/local/mongodb
export PATH=$PATH:$MGDB_HOME/bin
# 启用配置
$ source /etc/profile
```

##  

## 管理 *MongoDB*

> 默认情况下，*MongoDB* 无需权限即可访问

https://yq.aliyun.com/articles/70032?spm=5176.100239.blogcont58269.13.xyTBu7



https://yq.aliyun.com/articles/58269
