---
layout: post
title: '防火墙和端口'
date: 2018-06-26
author: 如花与食客
catalog: true
tags: CentOS
---

# CentOS -- 防火墙和端口
> 此文以`8090`为示例端口号 

## 1.查看端口占用
```
netstat -lnp|grep 8090
```

#### 查看详情
```
ps 8090
```

#### 杀掉进程
```
kill -9 8090
```

## 2.seLinux
#### 查看端口是否加入seLinux允许的http端口
```
semanage port -l | grep http_port_t
```

#### 添加端口
```
semanage port -a -t http_port_t  -p tcp 8090
```

## 3. `firewalld` 添加开放端口
#### 查看`firewalld`运行状态
```
systemctl status firewalld.service
```

#### 查看default zone和active zone
我们还没有做任何配置，default zone和active zone都应该是public
```
firewall-cmd --get-default-zone
firewall-cmd --get-active-zones
```

#### 查看当前开了哪些端口
其实一个服务对应一个端口，每个服务对应`/usr/lib/firewalld/services`下面一个xml文件。
```
firewall-cmd --list-services
```

#### 查看还有哪些服务可以打开
```
firewall-cmd --get-services
```

#### 添加一个服务到firewalld
```
firewall-cmd --add-service=http //http换成想要开放的service
```

这样添加的service当前立刻生效，但系统下次启动就失效，可以测试使用。要永久开发一个service，加上 --permanent
```
firewall-cmd --permanent --add-service=http
```

#### 如果要添加的端口并没有服务对应
就要新建一个服务，在`/usr/lib/firewalld/services`，随便拷贝一个xml文件到一个新名字，比如`myservice.xml`,把里面的
```
<?xml version="1.0" encoding="utf-8"?>
<service>
<short>Transmission-client</short>
<description>Transmission is a lightweight GTK+ BitTorrent client.</description>
<port protocol="tcp" port="51413"/>
</service>
```
short改为想要名字（这个名字只是为了人来阅读，没有实际影响。重要的是修改 protocol和port。修改完保存。我的经验是这是要重启firewalld服务，`systemctl restart firewalld.service`，否则可能提示找不到刚才新建的service。然后把新建的service添加到firewalld
```
firewall-cmd --permanent --add-service=myservice
```

#### 重启生效
```
systemctl restart firewalld.service
```