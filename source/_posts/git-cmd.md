---
title: Git 命令速查
date: 2019-11-27 16:41:24
categories: Git
tags:
- 命令速查
---
### 设置姓名和邮箱地址

```bash
git config --global user.name "Firstname Lastname"
git config --global user.email "your_emailexample.com"
```

### 单行显示每个提交信息的历史记录

```bash
git config format.pretty oneline
```

### 打开GUI工具

```bash
gitk
```

### 生成`SSH Key`

```bash
ssh-keygen -t rsa -C "your_emailexample.com"
```

### 初始化仓库

```bash
git init
```

### 克隆仓库

```bash
# 克隆本地仓库
git clone /path/to/repository
# 克隆远程仓库
git clone username@host:/path/to/repository
# 克隆GitHub仓库
git clone git@github.com:<username>/<repository.git>
git clone https://github.com/<username>/<repository.git>
```

### 查看仓库状态

```bash
git status
```

### 添加到暂存区

```bash
git add <filename>
# 添加所有文件
git add *
```

### 提交改动

```bash
git commit -m "代码提交信息"
```

### 修改提交信息

```bash
git commit --amend
```

### 添加远程仓库

```bash
git remote add origin <server>
```

### 推送到远程仓库

```bash
git push origin <branch>
```

### 拉取并合并远程仓库

```bash
git pull origin <branch>
```

### 拉取远程分支到本地

```bash
git fetch origin master:tmp
```

### 比较文件差异

```bash
git diff <source_branch> <target_branch>
```

### 合并分支

```bash
git merge <branch>  # 消除冲突, 然后重新提交
```

### 显示所有分支

```bash
git branch -a
```

### 创建并切换分支

```bash
git checkout -b <branch>
```

### 切换分支

```bash
git checkout <branch>
```

### 删除分支

```bash
git branch -d <branch>
```

### 查看提交记录

```bash
git log
```

### 只看某人的提交记录

```bash
git log --author=bob
```

### 以图表形式查看提交记录

```bash
git log --graph
```

### 单行输出提交记录

```bash
git log --pretty=oneline
```

### 回溯历史版本

```bash
git reset --hard <hash-value>
```

### 丢弃本地所有的改动与提交

```bash
git fetch origin
git reset --hard origin/master
```

### 压缩历史

```bash
git rebase -i HEAD~2
```

### 创建标签

```bash
git tag 1.0.0 1b2e1d63ff
```

### 合并两个不相干的分支

```bash
git merge <branch> --allow-unrelated_histories
```

### 删除远程分支

```bash
git push origin -d <branch>
```
