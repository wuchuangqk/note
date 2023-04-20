# yum和apt-get

yum是debian系linux发行版的包管理器：debian、ubuntu

apt-get是redhat系linux发行版的包管理器：redhat、centos、fedora

## yum

安装

```sh
yum install <package_name>
```

卸载

```sh
yum remove <package_name>
```

更新

```sh
yum update <package_name>
```

## apt-get
安装

```sh
apt-get install <package_name>
```

卸载

```sh
apt-get remove <package_name>
```

更新

```sh
apt-get update <package_name>
```

查看本机已安装软件列表

```sh
apt list --installed
apt list --installed | grep nodejs
```



### 设置国内源

编辑`/etc/apt/sources.list`，替换里面的全部内容

阿里云源

>deb http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse
>deb http://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse
>deb http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse
>deb http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse
>deb http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse
>deb-src http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse
>deb-src http://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse
>deb-src http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse
>deb-src http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse
>deb-src http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse

# node





# git

安装git

```sh
apt-get install git
```

# ssh

查看ssh服务状态



# redis

安装redis步骤

> [Install Redis on Windows | Redis](https://redis.io/docs/getting-started/installation/install-redis-on-windows/)

开启redis服务

```sh
sudo service redis-server start
```

查看redis服务状态

```sh
sudo service redis-server status
```

redis-cli

```sh
redis-cli 
127.0.0.1:6379> ping
PONG
127.0.0.1:6379> quit
```

