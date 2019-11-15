---
title: VirtualBox 启动错误
date: 2019-11-15 23:55:19
categories: VirtualBox
tags:
- error
- hyper-v
- window10
---
## 问题

Call to WHvSetupPartition failed: ERROR_SUCCESS (Last=0xc000000d/87) (VERR_NEM_VM_CREATE_FAILED).

![VirtualBoxError](https://github.com/lin-zone/lin-zone.github.io/blob/hexo/source/images/VirtualBoxError.png?raw=true)

## 解决

在 Windows10下开启了Hyper-V功能, 需关闭Hyper-V并重启两次

## 参考

[Ticket #18536](https://www.virtualbox.org/ticket/18536)