+++
title = "UbuntuServer默认配置"
date = "2019-12-10T21:57:34+08:00"
categories = [ "技术" ]
tags = [ "ubuntu", "linux", "server" ]
draft = true
+++

# 目的

在阿里云新买的ECS，需要安装一些自己使用的软件，还有一些特定的配置。为了能给人以启发，所以将原先写好的bash脚本拆散，放在这里。

## 安装更新

```
sudo apt update
sudo apt upgrade
sudo apt autoremove
```

## 创建新用户

```
sudo useradd -m -s /bin/bash ubuntu
```

## sudo无需密码

```
sudo visudo
```

添加

```
ubuntu ALL=(ALL) NOPASSWD:ALL
```

## 修改sshd配置

### 打开配置文件

```
sudo vim /etc/ssh/sshd_config
```

### 找到下面的key，将其改为下面的值

```
ChallengeResponseAuthentication no
PasswordAuthentication no
PermitRootLogin no
```

### 让sshd重读配置

```
sudo /etc/init.d/ssh reload
```

## 创建ssh key，以便使用key登陆

## 之后的操作都是使用ubuntu这个用户了

## 安装Docker

```
sudo apt-get remove docker docker-engine docker.io containerd runc
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo apt-key fingerprint 0EBFCD88
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
sudo groupadd docker
sudo usermod -aG docker $USER
```

## 安装Docker Compose

```
sudo curl -L "https://github.com/docker/compose/releases/download/1.25.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```
