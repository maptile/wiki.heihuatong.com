+++
title = "Thunderbird常见问题及解决方法"
date = "2018-07-27T13:29:34+08:00"
categories = [ "技术" ]
tags = [ "Thunderbird" ]
draft = false
+++

# 附件下载不完整/损坏

打开Preferences => Advanced => General => Config Editor

将mail.server.default.fetch_by_chunks改为false即可
