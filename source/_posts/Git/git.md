---
title: Git笔记
description: 🍠本文汇总Git基础教程 ，可作为文档进行查询
mathjax: true
tags:
  - Git
categories: 
  - 前端笔记
cover: https://s1.vika.cn/space/2023/03/21/6ae4c272bdc44d47b9177929349bcfca
abbrlink: 500
date: 2023-02-29 16:00:00
updated: 2023-02-29 16:00:00
---

## Git常用命令

| 命令                                 | 作用                         |
| ------------------------------------ | ---------------------------- |
| git config --global user.name 用户名 | 设置用户签名                 |
| git config --global user.email 邮箱  | 设置用户签名                 |
| git init                             | 初始化本地库                 |
| git status                           | 查看本地库状态               |
| git add 文件名                       | 添加到暂存区                 |
| git commit -m "日志信息" 文件名      | 提交到本地库（将会记录版本） |
| git reflog                           | 查看历史纪录                 |
| git log                              | 查看详细历史记录             |
| git reset --hard 版本号              | 版本穿梭                     |

## 分支的操作

| 命令                | 作用                         |
| ------------------- | ---------------------------- |
| git branch 分支名   | 创建分支                     |
| git branch -v       | 查看分支                     |
| git checkout 分支名 | 切换分支                     |
| git merge 分支名    | 把指定的分支合并到当前分支上 |

## 远程仓库操作

| 命令                               | 作用                                                     |
| ---------------------------------- | -------------------------------------------------------- |
| git remote -v                      | 查看当前所有远程地址                                     |
| git remote add 别名 远程地址       | 添加远程仓库并为其起别名                                 |
| git push 别名 分支                 | 推送本地分支上的内容到远程仓库                           |
| git clone 远程地址                 | 将远程仓库的内容克隆到本地                               |
| git pull 远程库地址别名 远程分支名 | 将远程仓库对于分支最新内容拉下来后与当前本地分支直接合并 |

## SSH连接远程仓库

添加SSH

```bash
ssh-keygen -t rsa -C "553344777@qq.com"
```

检查SSH

```bash
ssh -T git@github.com
```

