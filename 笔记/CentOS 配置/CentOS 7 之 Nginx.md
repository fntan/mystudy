# CentOS 7 之 Nginx

> CentOS 7.3 64 位 root权限

[TOC]



## 安装

### 编译环境

```shell
# gcc 环境
$ yum install -y gcc-c++
```

### 必要的库

#### *PCRE* 库cd

```shell
# 下载
$ wget ftp://ftp.csx.cam.ac.uk/pub/software/programming/pcre/pcre-8.41.tar.gz
# 解压
$ tar -zxvf pcre-8.41.tar.gz
$ cd pcre-8.41
# 编译
$ ./configure
$ make && make install
```

#### *zlib* 库

```shell
# 下载
$ wget http://zlib.net/zlib-1.2.11.tar.gz
# 解压
$ tar -zxvf zlib-1.2.11.tar.gz
$ cd zlib-1.2.11
# 编译
$ ./configure
$ make && make install
```

####  *ssl* 

```shell
# 下载
$ wget https://www.openssl.org/source/openssl-1.1.0f.tar.gz
# 解压
$ tar -zxvf openssl-1.1.0f.tar.gz
$ cd openssl-1.1.0f
# 编译
$ ./config
$ make && make install
```

###  *Nginx*

```shell
# 下载
$ wget http://nginx.org/download/nginx-1.13.5.tar.gz
# 解压
$ tar -zxvf nginx-1.13.5.tar.gz
$ cd nginx-1.13.5
# 编译
$ ./configure --prefix=/usr/local/nginx
$ make && make install
```

**注意** ：在编译时，可指定依赖源目录

```shell
$ ./configure --prefix=/usr/local/nginx  \
--with-pcre=/PCRE 库绝对路径				\
--with-zlib=/zlib 库绝对路径				\
--with-openssl=/OpenSSl绝对路径
```

到此 *Nginx*  安装成功！`/usr/local/nginx/` 

## 命令

```shell
# 启动
$ /usr/local/nginx/sbin/nginx
# 重启
$ /usr/local/nginx/sbin/nginx -s reload
# 停止
$ /usr/local/nginx/sbin/nginx -s quit
# (强制)停止
$ /usr/local/nginx/sbin/nginx -s stop
```

### 配置环境变量

```shell
$ vim /etc/profile
export NGINX_HOME=/usr/local/nginx
export PATH=$PATH:$NGINX_HOME/sbin
# 启用配置
$ source /etc/profile
```

### 自启动

```shell
$ vim /etc/rc.local
# 在最后增加一行
/usr/local/nginx/sbin/nginx

$ chmod 755 /etc/rc.local
```

## 配置

```makefile
# /usr/local/nginx/conf/nginx.conf #

/website/vhosts
```



```makefile
#user  nobody;
worker_processes  1;

#error_log  logs/error.log;
#error_log  logs/error.log  notice;
#error_log  logs/error.log  info;

#pid        logs/nginx.pid;


events {
    worker_connections  1024;
}

http {
    include       mime.types;
    default_type  application/octet-stream;
    sendfile        on;
    keepalive_timeout  65;
    gzip  on;

	include /website/vhosts/*.conf;
}
```



```makefile
server {
    listen       80;
    server_name  horui.wang www.horui.wang;
    root   /website/horui/public_home;
    index  index.html index.htm;
}
```

