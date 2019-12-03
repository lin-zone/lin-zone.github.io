---
title: 使用PuTTY从Linux服务器上下载文件
date: 2019-12-03 21:02:01
categories: Linux
tags:
- putty
- pscp
---
### 下载PuTTY

* [官网下载](https://www.putty.org/)

### 使用pscp

1. 测试`pscp`是否可用, 在Windows命令行下输入

    ```sh
    pscp -V
    ```

2. 从Linux服务器上下载文件

    ```sh
    pscp [user@]host:source target
    ```

    * `user`: 登录服务器的用户名
    * `host`: 服务器IP
    * `source`: 文件在服务器上的路径
    * `target`: 本地保存路径
