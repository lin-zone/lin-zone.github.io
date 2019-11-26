---
title: 使用Gitolite搭建Git服务器
date: 2019-11-27 00:52:44
categories: Git
tags:
- git
- server
- install
---
## 运行环境

* Ubuntu18.04
* Gitolite

## 1. 在云服务上选择合适的镜像, 创建好实例

## 2. 启动实例更新系统

```bash
sudo apt update
sudo apt upgrade
```

## 3. 安装 Vim

```bash
sudo apt install vim
```

## 4. 安装 Git

```bash
sudo apt install git
```

## 5. 创建用户

* 创建git用户: `sudo adduser git`
* 切换到git用户: `su git`
* 进入git用户目录: `cd ~`

## 6. 安装 Gitolite

```bash
git clone https://github.com/sitaramc/gitolite
mkdir -p $HOME/bin
gitolite/install -to $HOME/bin
```

## 7. 注册仓库管理员

* 新建`YourName.pub`文件，将客户端公钥`.ssh/id_rsa.pub`复制到里面，然后注册为仓库管理员

    ```bash
    vim YourName.pub
    # 复制客户端公钥内容，按:wq保存退出
    $HOME/bin/gitolite setup -pk YourName.pub # 注册仓库管理员
    ```

    建议在服务器上新建`admin`用户作为仓库管理员

* 新建管理员用户`admin`

   ```bash
   sudo adduser admin
   ```

* 生成`SSH`公钥

   ```bash
   su admin
   ssh-keygen -t rsa -C "youremail@example.com"
   cp .ssh/id_rsa.pub /tmp/admin.pub
   ```

* 切回`git`用户，将`admin`用户注册为仓库管理员

    ```bash
    su git
    cd ~
    $HOME/bin/gitolite setup -pk /tmp/admin.pub
    ```

    注册管理员后会生成两个文件`projects.list`, `repositories/`  
    `projects.list` 保存仓库信息列表  
    `repositories/` 文件夹里有管理员仓库`gitolite-admin.git/` 和测试仓库`testing.git/`  
    新建的仓库都会保存在`repositories/` 文件夹中  

## 8. 管理远程仓库

* 在已经注册过的客户端克隆管理员仓库

    ```bash
    git clone git@host:gitolite-admin
    ```

    管理员仓库里有两个文件`conf/gitolite.conf` 和 `keydir/`  
    `gitolite.conf` 管理仓库信息  
    `keydir/` 保存`git`成员的公钥  

* 添加新成员: 将新成员的公钥保存到`keydir/` 下

* 新建仓库

    修改`conf/gitolite.conf` 文件，添加`newrepo`仓库

    ```conf
    repo gitolite-admin
            RW+     =   admin

    repo testing
            RW+     =   @all

    repo newrepo
            RW+     =   @all
    ```

* 添加仓库管理员

    ```conf
    repo gitolite-admin
        RW+     =   admin
        RW+     =   lin-zone

    repo testing
        RW+     =   @all

    repo newrepo
        RW+     =   @all
    ```

## 9. 将仓库信息推送到服务器

在客户端更新完仓库信息后，需要将其推送到服务器才能生效

```bash
git add .
git commit -m "commit message"
git push origin master
```

## 参考

[sitaramc/gitolite](https://github.com/sitaramc/gitolite)
