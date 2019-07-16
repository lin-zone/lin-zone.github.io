---
title: 使用hexo搭建个人博客
date: 2019-07-16 11:39:55
tags: hexo
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

hexo clean
hexo g
hexo d
```
