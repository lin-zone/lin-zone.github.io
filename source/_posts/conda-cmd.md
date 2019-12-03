---
title: conda 命令速查
date: 2019-11-27 10:07:38
categories: Package
tags:
- conda
- 命令速查
---
### 创建环境

`conda create -n <env_name> <package_names>`

### 切换环境

`activate <env_name>`

### 退出环境

`deactivate`

### 显示已创建环境

`conda env list`

### 复制环境

`conda create -n <new_env_name> --clone <copied_env_name>`

### 删除环境

`conda remove -n <env_name> --all`

### 当前环境已安装包信息

`conda list`

### 在指定环境中安装包

`conda install -n <env_name> <package_name>`

### 在当前环境中安装包

`conda install <package_name>`

### 卸载指定环境中的包

`conda remove -n <env_name> < package_name>`

### 卸载当前环境中的包

`conda remove <package_name>`

### 更新所有包

`conda update --all`

### 更新指定包

`conda update <package_name>`

### 导出环境

`conda env export > environment.yaml`

### 导入环境

`conda env create -f enviroment.yaml`
