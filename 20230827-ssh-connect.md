---
title: 不同主机间的ssh链接互通
date: 2023-06-27 23:48:19
tags:
- ssh
- linux
---

在 Linux 系统上 SSH 是非常常用的工具，通过 SSH Client 我们可以连接到运行了 SSH Server 的远程机器上。SSH Client 的基本使用方法是：

```
ssh user@remote -p port
```

+ user 是你在远程机器上的用户名，如果不指定的话默认为当前用户
+ remote 是远程机器的地址，可以是 IP，域名，或者是后面会提到的别名
+ port 是 SSH Server 监听的端口，如果不指定的话就为默认值 22


### 免密码登入
每次 ssh 都要输入密码是不是很烦呢？与密码验证相对的，是公钥验证。也就是说，要实现免密码登入，首先要设置 SSH 钥匙。



查看有没有ssh server
```
/etc/init.d/ssh status
```

怎么生成密钥
```
ssh-keygen -t rsa 
```

查看本机的ssh密钥公钥
```
-- windows 目录
/c/Users/xxxx/.ssh
```

怎么添加其他机器的公钥

密钥怎么使用
```
# 密钥发送
 ssh-copy-id -i id_rsa.pub xxx@192.168.0.103

```

防火墙开启ssh
```
   41  /usr/sbin/ufw
   47  /usr/sbin/ufw allow ssh
   60  /usr/sbin/ufw status
   70  /etc/init.d/ufw restart
   60  /usr/sbin/ufw status
   60  /usr/sbin/ufw enable # 开机自启

```
ssh 开机自启
```
   87  systemctl enable ssh
```
重启后 ufw状态变为inactive问题
```
在设置开机自启后还有问题那大概率可能为启动顺序问题，修改/lib/systemd/system/ufw.service文件，在[Unit]中加入After=netfilter-persistent.service即可。

After=netfilter-persistent.service

```
root安装的docker，普通用户无法使用  
```
permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get "http://%2Fvar%2Frun%2Fdocker.sock/v1.24/containers/json": dial unix /var/run/docker.sock: connect: permission denied


```

