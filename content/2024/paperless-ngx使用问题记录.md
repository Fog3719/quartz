---
draft: false
aliases:
  - Reference
  - Paperless-ngx 使用问题记录
  - paperless-ngx使用问题记录
tags:
  - Software
number headings: auto, first-level 1, max 6, _.1.1
id: 20231229103422-f145cbaa-f2ed-4674-9a78-70b3cc8ffaf8
date modified: 2024-01-03 02:06:08
date: 2023-12-29 10:33:57
---

## 1 Docker 安装一直报 Redis:6379 错误？

==很简单的问题，是因为 paperless-ngx 安装需要依赖 Redis 服务。本机如果没有安装过的话，就一直无法启动。==
我的解决方法是在本机装了一个 Redis 服务，也是在 Docker 中安装的。安装 Redis 的方法是参考了 [[群晖 Docker 安装 redis|这篇文章]][^1]
安装完成之后，在 paperlessngx 的环境变量中添加一个 Redis 的服务地址。这一点可以参考官方文档里说明。
![Screenshot2023012029010043002.png|600](https://pic.237484.xyz/2023/12/202312291044404.png)

```
PAPERLESS_REDIS = `redis://:<password>@<host>:<port>`
```

## 2 数据挂载的问题

在群晖的 Docker 中设置挂载文件夹，也都是按照网上的教程设置的。但是在对应的文件夹内怎么也看不到数据。最后发现原来是对应的文件夹路径不对。网上说的都是直接挂在 `/data` 但实际上应该是 `/usr/src/paperless/media`
![Screenshot2023012029010049019.png|600](https://pic.237484.xyz/2023/12/202312291052315.png)

## 3 内网穿透时无法访问

根据官方文档的说明增加一个环境变量就好了。

![Screenshot2023012029010051056.png|600](https://pic.237484.xyz/2023/12/202312291052713.png)

> #### [`PAPERLESS_SECRET_KEY=<key>`](https://docs.paperless-ngx.com/configuration/#PAPERLESS_SECRET_KEY)
> Paperless uses this to make session tokens. If you expose paperless on the internet, you need to change this, since the default secret is well known.
> Use any sequence of characters. The more, the better. You don't need to remember this. Just face-roll your keyboard.
> Default is listed in the file `src/paperless/settings.py`.
> #### 3.1.1 [`PAPERLESS_URL=<url>`](https://docs.paperless-ngx.com/configuration/#PAPERLESS_URL)
> This setting can be used to set the three options below (ALLOWED_HOSTS, CORS_ALLOWED_HOSTS and CSRF_TRUSTED_ORIGINS). If the other options are set the values will be combined with this one. Do not > include a trailing slash. E.g. [https://paperless.domain.com](https://paperless.domain.com/)
> Defaults to empty string, leaving the other settings unaffected.

## 4 存储路径这个选项是什么意思？

仔细看了一下官方的文档，终于学会怎么使用这个存储路径了。
~~首先需要在环境变量中添加一个变量，把文件路径设置打开。默认是关闭的。~~
`PAPERLESS_FILENAME_FORMAT` 这个环境变量可以设置默认的存储路径。
![Screenshot2023012029011040041.png|600](https://pic.237484.xyz/2023/12/202312291147788.png)

## 5 官方文档

官方文档其实写的很清晰，基本大部分遇到的问题都可以通过文档来解决。
https://docs.paperless-ngx.com/configuration/#PAPERLESS_LOGOUT_REDIRECT_URL

# Reference

up:: [[常用软件分享]]
same::

[^1]: https://zhuanlan.zhihu.com/p/609267375