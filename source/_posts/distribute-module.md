---
title: 发布Python模块到PyPI
date: 2019-11-27 10:20:05
categories: Package
tags:
- python
- pypi
- setup
- pip
---
## 项目结构

```bash
packaging_tutorial/
    example_pkg/
        __init__.py
    setup.py
    LICENSE
    README.md
```

## 内容模板

### `__init__.py`

```python
name = "example_pkg"
version = "0.1.0"
```

### `setup.py`

```python
import setuptools

with open("README.md", "r") as fh:
    long_description = fh.read()

setuptools.setup(
    name="example-pkg-your-username",
    version="0.0.1",
    author="Example Author",
    author_email="author@example.com",
    description="A small example package",
    long_description=long_description,
    long_description_content_type="text/markdown",
    url="https://github.com/pypa/sampleproject",
    packages=setuptools.find_packages(),
    classifiers=[
        "Programming Language :: Python :: 3",
        "License :: OSI Approved :: MIT License",
        "Operating System :: OS Independent",
    ],
)
```

### `README.md`

```markdown
# Example Package

This is a simple example package. You can use
[Github-flavored Markdown](https://guides.github.com/features/mastering-markdown/)
to write your content.
```

### `LICENSE`

```license
Copyright (c) 2018 The Python Packaging Authority

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

## 打包模块

### 安装`setuptools`和`wheel`

```bash
python -m pip install --user --upgrade setuptools wheel
```

### 打包文件

```bash
python3 setup.py sdist bdist_wheel
```

产生如下文件

```bash
dist/
    example_pkg_your_username-0.0.1-py3-none-any.whl
    example_pkg_your_username-0.0.1.tar.gz
```

## 上传模块

1. 安装`twine`

    ```bash
    python -m pip install --user --upgrade twine
    ```

2. 上传测试PyPI

    ```bash
    python -m twine upload --repository-url https://test.pypi.org/legacy/ dist/*
    ```

3. 输入账号和密码, 确保已注册账号并验证过邮箱

4. 安装上传的测试包

    ```bash
    python -m pip install --index-url https://test.pypi.org/simple/ --no-deps example-pkg-your-username
    ```

5. 测试能否导入模块

    ```python
    >>> import example_pkg
    >>> example_pkg.name
    'example_pkg'
    ```

6. 正式上传模块

    ```bash
    python -m twine upload dist/*
    ```
