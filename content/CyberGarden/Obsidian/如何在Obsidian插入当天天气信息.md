---
draft: false
aliases:
  - 安装 Templater
  - 如何在Obsidian插入当天天气信息
created: 2021-07-09 21:25
tags:
  - Obsidian
link: https://github.com/SilentVoid13/Templater
date: 2022-11-05 11:02:00
date modified: 2023-03-16 12:17
up: "[[Obsidian]]"
updated: 2024-01-09 05:38:32
---

# 安装 Templater

地址:https://github.com/SilentVoid13/Templater

# Mac

## 1 安装# [Homebrew](https://brew.sh/)

`/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"`

## 2 安装 [curl](https://everything.curl.dev/get/macos)

`brew install curl`

## 3 踩过的坑

 1. Templater 这个插件在 1.X 之后更新了自己的设计.网上大部分的教程已经失效.
需要参考 https://silentvoid13.github.io/Templater/docs/
才能正常设置.
2. 插件插入的模板和正常模板插入是不一样的,正常的插入模板是无法启动插件功能的.必须去设置一个专用的快捷键.才能正常使用.
3. 查询天气用的是这个 https://github.com/chubin/wttr.in
4. 在创建模板时,需要 `tp.user.函数名称()`,如果需要给日历等插件使用,还要一个单独的文件夹放日历模板.
5. 装不上

`curl 'wttr.in/shanghai?format=3'`

## 使用情况

[[2022-10-26]] 今天天气服务突然不能用了。

up:: [[../Obsidian Plugin/Templater]]