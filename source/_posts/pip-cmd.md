---
title: pip 命令速查
date: 2019-11-27 10:50:54
categories: Python
tags:
- pip
- 命令速查
---
### 安装

`pip install [package]`

### 卸载

`pip uninstall [package]`

### 导出依赖文件

`pip freeze > requirements.txt`

### 通过依赖文件安装

`pip install -r requirements.txt`

### 升级模块

`pip install -U [package]`

### 显示模块所在目录

`pip show -f [package]`

### 搜索模块

`pip search [keyword]`

### 显示所有安装的模块

`pip list`

### 显示可升级的模块

`pip list -o`

### 打包模块

`pip wheel [package]`
