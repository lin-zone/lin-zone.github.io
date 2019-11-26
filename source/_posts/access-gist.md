---
title: 修改host解决gist.github.com无法访问的问题
date: 2019-11-27 01:35:42
categories: Questions
tags:
- gist
- github
---
修改`hosts`文件，添加以下内容

```bash
192.30.253.118 gist.github.com
192.30.253.119 gist.github.com
```

`hosts`文件路径

* Windows: `C:\Windows\System32\drivers\etc\hosts`
* Linux: `/etc/hosts`
