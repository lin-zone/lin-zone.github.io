---
title: 在Linux上安装Miniconda
date: 2019-11-27 01:14:05
categories: Package
tags:
- conda
- install
- linux
- ubuntu
---
> Anaconda是一个开源的Python包管理器，而Miniconda则是轻量级的Anaconda

## 下载

[官网地址](https://docs.conda.io/en/latest/miniconda.html)

```bash
sudo apt-get install wget
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
```

## 安装

```bash
bash Miniconda3-latest-Linux-x86_64.sh
```

```bash
# 一直按回车然后输入yes
please answer 'yes' or 'no':
>>> yes

# 选择安装路径, 文件名前加点号表示隐藏文件
Miniconda3 will now be installed into this location:
>>> ~/.miniconda3

# 添加配置信息到 ~/.bashrc文件
Do you wish the installer to initialize Miniconda3 by running conda init? [yes|no]
[no] >>> yes
```

运行配置信息文件或重启电脑

```bash
source ~/.bashrc
```

## 测试

测试是否安装成功

```bash
conda --version
```

创建虚拟环境

```bash
conda create -n venv python=3.6
```

激活虚拟环境

```bash
conda activate venv
```

退出虚拟环境

```bash
conda deactivate
```
