# CentOS 7 之 MySQL

> CentOS 7.3 64 位 root权限

[TOC]



## 安装 

### 卸载 *MariaDB*

> *CentOS 7* 默认安装 *MariaDB* 而不是 *MySQL*，而且 *yum* 服务器上也移除了 *MySQL* 相关的软件包。
>
>  *MariaDB* 和 *MySQL* 可能会冲突，故先卸载 *MariaDB* 。

```shell
# 系统是否安装，无输出则跳过
$ rpm -qa | grep -i mariadb
> mariadb-libs-5.5.52-1.el7.x86_64
# 不同版本预装的不一样，这里提示的版本记得复制到下面去卸载
$ rpm -e --nodeps mariadb-libs-5.5.52-1.el7.x86_64
```

### 获取 *yun* 源

> 地址：https://dev.mysql.com/downloads/repo/yum/

在 *MySql*  页面找到*rpm*包 复制链接地址

```shell
# 下载源
$ wget https://dev.mysql.com/get/mysql57-community-release-el7-11.noarch.rpm
# 安装源
yum -y localinstall mysql57-community-release-el7-11.noarch.rpm
```

### *MySQL*

```shell
$ yum -y install mysql-community-server
```

## 命令

```shell
# 启动
$ systemctl start mysqld
# 重启
$ systemctl restart mysqld
# 停止
$ systemctl stop mysqld
```

自启动

```shell
$ systemctl enable mysqld
$ systemctl daemon-reload
```



## 连接

### 初次连接

```shell
# 查看root本地登录临时密码
$ vim /var/log/mysqld.log
# 找到下面输出
[Note] A temporary password is generated for root@localhost: krs/w;b?g3sR
```

### *root* 登录

```shell
$ mysql -u root -p
# 输入上面的临时密码
< krs/w;b?g3sR
# 更改密码
< ALTER USER 'root'@'localhost' IDENTIFIED BY '密码（Aa+8）';
# 退出
< exit
```

### 允许远程登录

```shell
< GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY '密码（Aa+8）' WITH GRANT OPTION;
```

## 配置

### *utf-8* 编码

```shell
# 编辑 /etc/my.cnf
$ vim /etc/my.cnf
# 在 [mysqld] 下面添加
character_set_server=utf8
init_connect='SET NAMES utf8'
```





