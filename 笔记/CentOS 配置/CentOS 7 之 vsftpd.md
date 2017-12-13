# CentOS 7 之 vsftpd

> CentOS 7.3 64 位 root权限

[TOC]




## 安装

### 检查

```shell
$ rpm -qa |grep vsftpd
# 若无任何输出则说明没有安装
```

### 使用 *yun* 安装

```shell
$ yum install vsftpd* -y
```

安装成功后，会自动添加系统用户【ftp】`/var/ftp` 

## 命令

### 基本命令

```shell
# 启动服务
$ service vsftpd start
> Starting vsftpd (via systemctl):		[  OK  ]
# 停止服务
$ service vsftpd stop
> Stopping vsftpd (via systemctl): 		[  OK  ]
# 重启服务
$ service vsftpd restart
> Restarting vsftpd (via systemctl): 	[  OK  ]
```

### 自动启动

```shell
$ chkconfig vsftpd on
```



现在可以使用 *FTP* 客户端（匿名）访问 *FTP* 服务器（21端口）

若无法访问，请查看服务器的安全组规则是否开放 *21* 端口

## 配置

配置文件在：`/etc/vsftpd/vsftpd.conf`，使用 *vi / vim*  编辑文件

**说明** ：`i` 插入；`Esc` 退出编辑；`:wq` 保存退出

### 匿名登录

> 默认情况，可以使用匿名登录

```makefile
# /etc/vsftpd/vsftpd.conf #
# 是否允许匿名ftp,如否则选择NO
anonymous_enable=YES
# 匿名用户是否能上传
anon_upload_enable=YES
# 匿名用户是否能创建目录
anon_mkdir_write_enable=YES
# 修改文件名和删除文件
anon_other_write_enable=YES
```

### 本地登录

```makefile
# /etc/vsftpd/vsftpd.conf #
# 是否允许本地用户登录
local_enable=YES
# umask 默认755
local_umask=022
# 本地用户禁锢在宿主目录中
chroot_local_user=YES
# 是否将系统用户限止在自己的home目录下
chroot_list_enable=YES
# 列出的是不chroot的用户的列表
chroot_list_file=/etc/vsftpd/chroot_list
```

#### 配置*chroot*列表

```shell
$ touch /etc/vsftpd/chroot_list
# 编辑 chroot_list 列表
$ vim /etc/vsftpd/chroot_list
这里是系统用户名-1
这里是系统用户名-2
```



### 虚拟用户登录

安装*PAM*

```shell
# PAM（用于用户认证）
$ yum install pam* -y
# DB4（用于生成虚拟用户的用户名密码的db文件）
$ yum install db4* -y
```

#### 配置

```makefile
# /etc/vsftpd/vsftpd.conf #
# 启用虚拟用户
guest_enable=YES
# 虚拟用户借用的系统本地用户名(ftp:默认创建的)
guest_username=ftp
# 虚拟用户的配置文件路径
user_config_dir=/etc/vsftpd/virtualuser_conf
```

#### 创建目录

```shell
$ mkdir /etc/vsftpd/virtualuser_conf
$ cd /etc/vsftpd/virtualuser_conf
```

#### 创建用户配置

```shell
# 配置文件名与虚拟用户名一样
$ vim vvschool
# 该虚拟用户上传下载的根目录
local_root=/website/vvschool
write_enable=YES
anon_umask=022
anon_world_readable_only=NO
anon_upload_enable=YES
anon_mkdir_write_enable=YES
anon_other_write_enable=YES
```

#### 创建虚拟用户名单

```shell
$ touch /etc/vsftpd/virtualuser_passwd.txt
# 编辑 virtualuser_passwd.txt 一行用户名；一行密码
$ vim /etc/vsftpd/virtualuser_passwd.txt
这里是虚拟用户-1
这里是密码
这里是虚拟用户-1
这里是密码
```

#### 生成认证

```shell
$ db_load -T -t hash -f /etc/vsftpd/virtualuser_passwd.txt /etc/vsftpd/virtualuser_passwd.db
# 编辑 /etc/pam.d/vsftpd
$ vim /etc/pam.d/vsftpd
# 注释该文件内全部内容，添加下面两行内容
auth required pam_userdb.so db=/etc/vsftpd/virtualuser_passwd
account required pam_userdb.so db=/etc/vsftpd/virtualuser_passwd
```

#### 设置目录权限

```shell
# 虚拟用户上传下载的根目录(上文设置的)
$ chown -R ftp:ftp /website/vvschool/
$ chmod 077 /website/vvschool/
```

到此可以使用虚拟用户登录

若出现 `500 OOPS: vsftpd: refusing to run with writable root inside chroot ()` ，在 `/etc/vsftpd/vsftpd.conf` 中添加

```makefile
# /etc/vsftpd/vsftpd.conf #
allow_writeable_chroot=YES
```



### 设置 *log* 日志

```makefile
# /etc/vsftpd/vsftpd.conf #
xferlog_enable=YES
xferlog_file=/etc/vsftpd/vsftpd.log
xferlog_std_format=YES
```



## 参考：

[linux下ftp配置文件详解](http://www.cnblogs.com/mrcln/p/6189665.html)

[vsftpd: 500 OOPS 连接错误](http://blog.csdn.net/xiaokui_wingfly/article/details/45606061)









