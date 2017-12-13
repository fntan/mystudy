# CentOS 7 之 Node

> CentOS 7.3 64 位 root权限

[TOC]

## 安装

```shell
# 下载
$ wget https://nodejs.org/dist/v8.6.0/node-v8.6.0-linux-x64.tar.xz
# 解压
$ xz -d node-v8.6.0-linux-x64.tar.xz
$ tar -xvf node-v8.6.0-linux-x64.tar
# 移动目录
$ mv node-v8.6.0-linux-x64 node /usr/local/node/v8.6.0
```

### 配置环境变量

```shell
$ vim /etc/profile
export NODE_HOME=/usr/local/node/v8.6.0
export PATH=$NODE_HOME/bin:$PATH
# 启用配置
$ source /etc/profile
```

### 



## 