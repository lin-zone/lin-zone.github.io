---
title: poetry 使用
date: 2019-10-23 10:15:13
categories: Python
tags:
- poetry
- 包管理
- 依赖管理
---
[官方文档](https://poetry.eustace.io/docs/)

## 安装 poetry

`pip install poetry`

## poetry 命令

* 更新 poetry

`poetry self:update`

* 创建新项目

`poetry new <project>`

* 添加包

`poetry add <package_name>`

* 删除包

`poetry remove <package_name>`

* 安装包

`poetry install`

* 显示包信息

`poetry show`

* 打包

`poetry build`

* 发布到 PyPI

`poetry publish`

* 发布到个人仓库

`poetry publish -r <my-repository>`

* 创建`pyproject.toml`文件

`poetry init`

* 显示配置信息

`poetry config --list`

* 在虚拟环境中运行

`poetry run python -V`

* 生成 shell

`poetry shell`

* 检查项目结构

`poetry check`

* 不安装`pyproject.toml`指定的依赖

`poetry lock`

* 更新项目版本

`poetry version <rule>`

> rule 可以是 `patch, minor, major, prepatch, preminor, premajor, prerelease`

## pyproject.toml 文件

* 定义脚本

```toml
[tool.poetry.scripts]
my-script = "my_module:main"
```

* 模板文件

```toml
[tool.poetry]
name = "poetry-setup"
version = "0.3.6"
description = "make setup.py (setutools) from pyproject.toml (poetry)"
authors = [
    "Gram Orsinium <master_fess@mail.ru>"
]
license = "Apache-2.0"
readme = "README.md"
homepage = "https://github.com/orsinium/poetry-setup"
repository = "https://github.com/orsinium/poetry-setup"
keywords = ["packaging", "dependency", "poetry", "setuptools", "pip"]
classifiers = [
    "Development Status :: 4 - Beta",
    "Environment :: Console",
    "Topic :: Software Development :: Build Tools",
    "Topic :: Software Development :: Libraries :: Python Modules"
]

[tool.poetry.dependencies]
python = "^3.4"
autopep8 = "*"
jinja2 = "*"
poetry = "*"
yapf = "*"

[tool.poetry.dev-dependencies]
pytest = "*"

[tool.poetry.scripts]
poetry-setup = "poetry_setup.core:main"
```
