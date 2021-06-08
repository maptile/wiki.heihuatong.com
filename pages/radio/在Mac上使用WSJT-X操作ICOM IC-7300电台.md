+++
title = "在Mac上使用WSJT-X操作ICOM IC-7300电台"
date = "2020-01-29T21:57:34+08:00"
categories = [ "无线电" ]
tags = [ "mac", "wsjt-x", "radio", "ic-7300", "7300" ]
draft = false
+++

# 安装WSJT-X

1. 到 https://www.physics.princeton.edu/pulsar/K1JT/wsjtx.html 下载WSJT-X
1. 假设目前的WSJT-X版本为2.1.2，Mac版
1. 双击打开刚才下载的wsjtx-2.1.2-Darwin.dmg，会发现有几个文件：wsjtx、ReadMe.txt、sysctl.conf
1. 先将wsjtx拖动到Applications目录下（即Mac上标准的安装程序方式）
1. 再将sysctl.conf复制到桌面
1. 打开终端，输入以下命令
```
sudo cp "$HOME/Desktop/sysctl.conf" /etc/
sudo chmod 664 /etc/sysctl.conf
sudo chown root:wheel /etc/sysctl.conf
```
1. 重启Mac
1. 运行WSJT-X

# 如果你的系统是10.14 (Mojave)

WSJT-X需要访问麦克风，才能接收到信号，在Mojave及之后的版本中需要赋予其麦克风权限。

1. 你需要先运行WSJT-X
1. 打开系统选项 > 安全与隐私 > 隐私，在列表中选择"麦克风"，并且允许WJST-X访问麦克风。
1. 重启WSJT-X

# 安装驱动

1. 点击屏幕左上角的苹果标志，打开"关于此电脑"
1. 点击"系统报告"
1. 在左侧找到USB，并点击
1. 在右侧可以看到CP2101 USB to UART Bridge Controller，如果你看到的不是这个，可能要自己找相关的驱动下载了。
1. 到 https://www.silabs.com/products/development-tools/software/usb-to-uart-bridge-vcp-drivers 下载CP210X驱动
1. 安装

# IC-7300上的设置

点击Menu > SET > Connectors
- DATA OFF MOD: MIC,ACC
- USB Serial Function: CI-V

点击Menu > SET > Connectors > CI-V
- CI-V Baud Rate: 19200
- CI-V Address: 94h
- CI-V Transceive: ON
- CI-V USB-> REMOTE Transceive Address: 00h
- CI-V Outout (for ANT): OFF
- CI-V USB Port: Link to [REMOTE]

# 使用USB线缆连接电台和电脑

1. 电缆两端最好加上磁环


