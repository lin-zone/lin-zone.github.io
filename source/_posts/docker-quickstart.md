---
title: Docker快速入门
date: 2019-11-27 11:06:00
categories: Docker
tags:
- install
- windows
- 命令速查
---
## Windows 10 安装

* 下载[Docker Desktop](https://download.docker.com/win/stable/Docker%20for%20Windows%20Installer.exe)
* 打开`Hyper-V`
* 安装`Docker for Windows`

Docker Hub [官网](https://hub.docker.com/)

## Docker 命令

### 检查docker的版本

```bash
docker version
```

### 搜索可用的docker镜像

```bash
docker search tutorial
```

### 下载容器镜像

```bash
docker pull learn/tutorial
```

### 在docker容器中运行hello world

```bash
docker run learn/tutorial echo "hello world"
```

### 在容器中安装新的程序

```bash
docker run learn/tutorial apt-get install ping
```

### 保存对容器的修改

```bash
docker commit [ID] learn/ping
```

### 运行新的镜像

```bash
dockere run learn/ping ping www.google.com
```

### 检查运行中的镜像

```bash
docker inspect [ID]
```

### 发布自己的镜像

```bash
docker login
docker tag learn/ping myname/ping
docker push myname/ping
```
