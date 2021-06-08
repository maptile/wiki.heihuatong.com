+++
title = "Docker相关的命令与配置"
date = "2018-03-06T14:59:34+08:00"
categories = [ "技术" ]
tags = [ "Docker", "命令" ]
draft = false
+++

# 更改Docker Root Dir

Docker Root Dir默认为/var/lib/docker
如果当磁盘空间不足，或者其他原因需要将该目录放在其他盘时，可以使用下面的方法替换。

先停止docker daemon

```
sudo systemctrl stop docker
```

编辑daemon的配置文件

```
sudo vim /etc/docker/daemon.json
```

输入以下内容
```
{
    "data-root": "新路径"
}
```

之后再把/var/lib/docker中的目录复制到新地址。

再重新启动docker daemon

```
sudo systemctrl start docker
```

# 清理Docker占用的磁盘空间

```
# 删掉已退出的容器
docker ps --filter status=dead --filter status=exited -aq | xargs docker rm -v

# 删掉label是none的镜像
docker images --no-trunc | grep '<none>' | awk '{ print $3 }' | xargs -r docker rmi

# 清理无用的volume
docker volume ls -qf dangling=true | xargs -r docker volume rm

```

# 设置代理

将下面的内容写入`/etc/systemd/system/docker.service.d/proxy.conf`。如果该文件不存在，请先创建

内容为
```
[Service]
Environment="HTTP_PROXY=http://localhost:8118"
Environment="HTTPS_PROXY=http://localhost:8118/"
Environment="NO_PROXY="localhost,127.0.0.1,::1,OTHER-DOMAINS-1,OTHER-DOMAINS-2"
```

其中，8118是本机开启的http代理的端口。
OTHER-DOMAINS-1和OTHER-DOMAINS-2为其他需要直连的URL或IP，逗号分割。
