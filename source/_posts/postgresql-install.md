---
title: PostgreSQL Windows 安装
date: 2019-10-21 23:46:36
categories: Database
tags:
- postgresql
- install
- windows
- database
---
## 下载

[官网地址](https://www.enterprisedb.com/downloads/postgres-postgresql-downloads)

## 服务端

* 创建数据库集群

```bash
initdb -D "K:\PostgreSQL\data"
```

* 启动数据库服务器

```bash
pg_ctl -D ^"K^:^\PostgreSQL^\data^" -l logfile start
```

* 注册Windows服务

```bash
pg_ctl register -N PostgreSQL -D "K:\PostgreSQL\data"
```

* 注销Windows服务

```bash
pg_ctl unregister -N PostgreSQL
```

## 客户端

* 客户端连接

```bash
psql -d postgres
```
