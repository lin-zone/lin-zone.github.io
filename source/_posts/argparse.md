---
title: argparse模块
date: 2019-11-27 09:43:24
categories: Python
tags:
- 标准库
- 命令行
---
### 基本操作

```python
import argparse                                 # 导入模块

parser = argparse.ArgumentParser()              # 创建解析对象
parser.add_argument()                           # 添加参数和选项
group = parser.add_mutually_exclusive_group()   # 分组
group.add_argument()
args = parser.parse_args()                      # 解析参数
```

### 定位参数

```python
parser.add_argument("h")
```

### 短参数

```python
parser.add_argument("-h")
```

### 长参数

```python
parser.add_argument("--help")
```

### 默认布尔参数

通过`action`定义

```python
parser.add_argument("-h", action="store_true")
```

### 定义参数类型

默认参数类型为`str`, 转换其他类型通过`type`定义

```python
parser.add_argument('x', type=int)
```

### 限定参数范围

```python
parser.add_argument("-x", choices=[0, 1, 2])
```

### 定义参数帮助信息

```python
parser.add_argument('x', help="the base")
```

### 定义程序帮助信息

```python
argparse.ArgumentParser(description="function help")
```

### 互斥参数

```python
group = parser.add_mutually_exclusive_group()
group.add_argument("-v", "--verbose", action="store_true")
group.add_argument("-q", "--quiet", action="store_true")
```

### 参数默认值

```python
parser.add_argument("-v", "--verbosity", default=1)
```
