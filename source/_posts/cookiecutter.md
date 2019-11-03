---
title: 模板工具cookiecutter
date: 2019-10-23 09:34:05
categories: Python
tags:
- template
- cookiecutter
- jinja2
---
> 使用cookiecutter通过项目模板创建Python项目

## 安装 cookiecutter

```bash
pip install cookiecutter
```

选择项目模板 [A Pantry Full of Cookiecutters](https://github.com/cookiecutter/cookiecutter/tree/db14e06a1dcc0187beeafde72685c3acef93eb68#a-pantry-full-of-cookiecutters)

## 使用模板

下载模板

```bash
cookiecutter https://github.com/audreyr/cookiecutter-pypackage
# 从GitHub下载模板
cookiecutter gh:audreyr/cookiecutter-pypackage
```

根据提示输入项目信息, 然后生成项目

> `cookiecutter`下载的模板会保存在`~/.cookiecutter`目录下, 可以通过项目名再次使用. 项目的配置信息保存在`~/.cookiecutter_replay`目录下, 可以通过`--replay`选项从更新过的模板创建项目.

使用本地模板

```bash
# 从本地生成项目
cookiecutter cookiecutter-pypackage
```

重用模板

```bash
cookiecutter --replay gh:hackebrot/cookiedozer
```

在`Python`中使用`cookiecutter`

```python
from cookiecutter.main import cookiecutter

# Create project from the cookiecutter-pypackage/ template
cookiecutter('cookiecutter-pypackage/')

# Create project from the cookiecutter-pypackage.git repo template
cookiecutter('https://github.com/audreyr/cookiecutter-pypackage.git')
```

## 配置文件

创建`~/.cookiecutterrc`文件, 保存一些个人信息, 下次创建项目时就可以使用默认信息

```yml
default_context:
    full_name: "Audrey Roy"
    email: "audreyr@gmail.com"
    github_username: "audreyr"
cookiecutters_dir: "~/.cookiecutters/"
```

通过`--config-file`指定配置文件

```bash
cookiecutter --config-file /home/audreyr/my-custom-config.yaml cookiecutter-pypackage
```

或者设置系统变量`COOKIECUTTER_CONFIG`

```bash
export COOKIECUTTER_CONFIG=/home/audreyr/my-custom-config.yaml
```

## 基本原理

`cookiecutter`使用`Jinja2`语法将`cookiecutter.json`文件中的变量`name`替换模板文件中所有被双`{}`包裹的标签(可以是文件名, 目录名, 文件内的字符串), 然后生成项目.

## 创建模板

项目结构

```bash
cookiecutter-something/
├── {{cookiecutter.project_slug}}/
├── hooks
│   ├── pre_gen_project.py
│   └── post_gen_project.py
└── cookiecutter.json
```

* `cookiecutter.json` - 设置配置变量, 变量的值也可以使用`Jinja2`语法标记, 如

```json
{
  "project_name": "My New Project",
  "project_slug": "{{ cookiecutter.project_name|lower|replace(' ', '-') }}",
  "pkg_name": "{{ cookiecutter.project_slug|replace('-', '') }}"
}
```

* `hooks/` - 生成项目时会执行`hooks`文件内的脚本

```python
# hooks/pre_gen_project.py
import re
import sys


MODULE_REGEX = r'^[_a-zA-Z][_a-zA-Z0-9]+$'

module_name = '{{ cookiecutter.module_name }}'

if not re.match(MODULE_REGEX, module_name):
    print('ERROR: %s is not a valid Python module name!' % module_name)

    # exits with status 1 to indicate failure
    sys.exit(1)
```

* 其他地方按照正常方法创建项目, 然后将需要替换的地方用`Jinja2`语法标签标记即可

## 参考

* [cookiecutter.readthedocs.io](https://cookiecutter.readthedocs.io/en/latest/)

* [Create a new cookiecutter template project](https://raphael.codes/blog/create-your-own-cookiecutter-template/)

