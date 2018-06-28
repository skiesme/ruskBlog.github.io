---
layout: post
title: 'GitLab'
date: 2018-06-28
author: 如花与食客
catalog: true
tags: CentOS
---

# CentOS -- GitLab

> ps:操作系统：`Cetnos7`

## 一、环境搭建
### 1.1 下载 wget
```
yum install -y wget
```
### 1.2 备份初始源
```
mv /etc/yum.repos.d /etc/yum.repos.d.backup
```

### 1.3 设置新的yum目录
```
mkdir /etc/yum.repos.d
```

### 1.4 下载阿里yum配置到该目录中
```
wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo
```

### 1.5 重建yum缓存
```
yum clean all
yum makecache
```

### 1.6 升级所有包
```
yum update -y
```

## 二、安装gitlab
### 2.1 安装gitlab的依赖项
```
yum install curl openssh-server openssh-clients postfix cronie policycoreutils-python –y
```

### 2.2 启动postfix，并设置为开机启动 
```
systemctl start postfix
systemctl enable postfix
```

### 2.3 设置防火墙
```
firewall-cmd --add-service=http --permanent
firewall-cmd --reload
```

### 2.4 获取gitlab的rpm包
查看清华开源镜像站，获取rpm包
```
wget https://mirrors.tuna.tsinghua.edu.cn/gitlab-ce/yum/el7/gitlab-ce-11.0.1-ce.0.el7.x86_64.rpm
```
安装rpm包
```
rpm -i gitlab-ce-11.0.1-ce.0.el7.x86_64.rpm
```

##  三、配置gitlab
### 3.1 修改ip地址
```
vi /etc/gitlab/gitlab.rb
```
将external_url变量的地址修改为gitlab所在centos的ip地址。
```
例如：external_url '192.168.20.90'
```
### 3.2 修改worker_processes
修改worker_processes,可防止gitlab占用内存过大的问题，最小值为`2`，推荐值`设备最大核数+1`：
```
 unicorn['worker_processes'] = 2
```

### 3.3 重新加载配置
```
gitlab-ctl reconfigure
gitlab-ctl restart
```

### 3.4 `ruby_block[supervise_redis_sleep] action run` 问题
在初次加载配置时，可能遇到卡死，问题如下``ruby_block[supervise_redis_sleep] action run``

解决方案：
```
1、按住CTRL+C强制结束；

2、运行：sudo systemctl restart gitlab-runsvdir；

3、再次执行：sudo gitlab-ctl reconfigure
```
