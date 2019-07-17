---
title: 使用Graphviz和Pyreverse绘制Python项目结构图
date: 2019-07-17 21:44:02
categories: Python
tags:
- graphviz
- pyreverse
- python
- uml
---
## 简介

- `Graphviz`开源的图形绘制工具包

- `Pyreverse`分析Python代码和类关系的工具

## 安装

1. 安装`Graphviz` [官网下载地址](http://www.graphviz.org/download/)

    注意添加`bin/`目录的路径到系统路径, 测试是否安装成功

    ```bash
    dot --help
    ```

2. 安装`Pyreverse`

    现在`pyreverse`已经集成到`pylint`, 直接安装`pylint`即可

    ```bash
    pip install pylint
    ```

    测试是否安装成功

    ```bash
    pyreverse --help
    ```

3. 使用`Pyreverse`分析Python代码

    以`flask/`代码为例

    ```bash
    pyreverse flask/
    ```

    `pyreverse`会分析`flask`文件的代码并在当前目录下生成`classes.dot`和`packages.dot`两个`dot`格式的文件

4. 使用`Graphviz`将`dot`文件转换为图形格式

    转换为`png`格式

    ```bash
    dot -Tpng -o classes.png classes.dot
    dot -Tpng -o packages.png packages.dot
    ```

    也可以转换为`jpg`和`pdf`格式

    ```bash
    dot -Tjpg -o classes.jpg classes.dot

    dot -Tpdf -o packages.pdf packages.dot
    ```

    生成的图形如下所示

    ![](https://github.com/lin-zone/lin-zone.github.io/blob/hexo/source/images/packages.png?raw=true)
