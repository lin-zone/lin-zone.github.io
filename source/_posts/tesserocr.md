---
title: 使用tesserocr库识别图形验证码
date: 2019-10-14 10:13:11
categories: Python
tags:
- tesseract
- tesserocr
- 识别验证码
---
简介

- Tesseract-OCR, 一款由Google维护的开源OCR引擎, 可用于图像识别
- tesserocr, Python的OCR识别库, 基于Tesseract-OCR做的Python API封装

安装Tesseract-OCR [下载地址](https://digi.bib.uni-mannheim.de/tesseract/)

将Tesseract-OCR安装路径添加到path环境变量中

用Tesseract-OCR测试识别验证码

![phototest.png](https://github.com/lin-zone/lin-zone.github.io/blob/hexo/source/images/phototest.png?raw=true)

```cmd
tesseract phototest.png result
```

![result.png](https://github.com/lin-zone/lin-zone.github.io/blob/hexo/source/images/result.PNG?raw=true)

使用conda安装tesserocr

```cmd
conda install -c simonflueckiger tesserocr
```

添加系统环境变量(改为Tesseract-OCR的安装路径)

```cmd
TESSDATA_PREFIX=C:\Program Files (x86)\Tesseract-OCR
```

使用tesserocr库识别验证码

```python
>>> import tesserocr
>>> text = tesserocr.file_to_text('phototest.png')
>>> print(text)
This is a lot of 12 point text to test the
cor code and see if it works on all types
of file format.

The quick brown dog jumped over the
lazy fox. The quick brown dog jumped
over the lazy fox. The quick brown dog
jumped over the lazy fox. The quick
brown dog jumped over the lazy fox.
```
