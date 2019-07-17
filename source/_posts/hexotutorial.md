---
title: 使用hexo搭建个人博客
date: 2019-07-17 01:01
author: lin-zone
categories: Blog
tags:
- hexo
- blog
---

准备工作

* Node.js
* npm
* Git
* GitHub账号

## 快速开始

### 安装hexo

```bash
npm install -g hexo
```

### 初始化

`lin-zone`改为自己的GitHub账号

```bash
hexo init lin-zone.github.io
cd lin-zone.github.io
npm install
```

### 启动服务

```bash
hexo server
```

访问 [http://localhost:4000](http://localhost:4000)

配置`_config_yml`

```yml
title: #网站标题
subtitle: #网站副标题
author: #作者名字
```

生成静态文件

```bash
hexo generate
```

### 部署到GitHub

在GitHub新建`lin-zone.github.io`仓库

配置`_config.yml`

```yml
deploy:
  type: git
  repository: git@github.com:lin-zone/lin-zone.github.io.git
  branch: master
```

安装插件

```bash
npm install hexo-deployer-git --save
```

提交到GitHub

```bash
hexo deploy
```

访问 [https://lin-zone.github.io/](https://lin-zone.github.io/)

### 新建文章

```bash
hexo new hexotutorial
# 编辑文章
# 提交
hexo clean
hexo g
hexo d
```

## 高级配置

### 更换主题

安装 hexo-theme-matery

```bash
git clone https://github.com/blinkfox/hexo-theme-matery themes/matery
```

安装插件

```bash
npm i -S hexo-prism-plugin
npm install hexo-generator-search --save
npm i hexo-permalink-pinyin --save
npm i --save hexo-wordcount
npm install hexo-generator-feed --save
```

### git分支进行多终端工作

添加分支`hexo`, 上传文件

在仓库的`settings`中选择默认分支为`hexo`分支

#### 在另一个终端

安装`hexo`

```bash
npm install hexo-cli -g
```

克隆文件, 安装依赖

```bash
git clone git@github.com:lin-zone/lin-zone.github.io.git
cd lin-zone.github.io
npm install
npm install hexo-deployer-git --save
```

生成, 部署

```bash
hexo g
hexo d
```

可能错误

`INFO No layout: index.html`

原因

直接在`themes`文件下克隆主题造成仓库嵌套, `git`不会上传嵌套的仓库

解决

删除`.git`文件并删除缓存

```bash
git rm --cached themes/matery
```
