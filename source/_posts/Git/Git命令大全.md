---
title: Git命令
description: 🍞本文汇总Git命令教程，可作为文档进行查询
mathjax: true
tags:
 - Git
categories:
 - Git
abbrlink: 501
cover: https://s1.vika.cn/space/2022/12/29/6255146637d24df6a40e1f95c75b5908
sticky: 1
swiper_index: 1
date: 2023-03-13 10:00:00
updated: 2023-08-13 18:00:00
---
## git
{% note info no-icon %}Git是一个分布式的版本控制系统。
GitHub是一个基于Git做版本控制的代码托管平台。类似的还有Gitee, BitBucket等。
{% endnote %}

> 在Windows上使用Git，需要下载 Git for windows 软件，在官网下载，速度比较慢，可以找相关资源网站去下载
> MINGW32 / MINGW64
> 可以去下面的网站下载 
> [http://npm.taobao.org/mirrors/git-for-windows/](http://npm.taobao.org/mirrors/git-for-windows/)

## 初次使用

```bash
git init
# 初始化git仓库。先进入到要初始化的仓库的文件夹，再执行此命令

#第一次使用时，需要配置 用户名和邮箱等：
git config --global user.name "填入自己的用户名"
git config --global user.email "填入自己的邮箱地址"


git reflog    用来记录你的每一次命令
gitk [filename]		查看特定文件的历史修改记录

```

## 1. git config

>    Git 一共有3个配置文件：
>   - 仓库级的配置文件：在仓库的 `.git/.gitconfig`，该配置文件只对所在的仓库有效。  
>   - 全局配置文件：Mac 系统在  `~/.gitconfig`，Windows 系统在 `C:\Users\<用户名>\.gitconfig`。 
>   - 系统级的配置文件：在 Git的安装目录下（Mac 系统下安装目录在 `/usr/local/git`）的 etc 文件夹中的 `gitconfig`。

```bash
git config
# 查看当前git仓库的配置信息
git config --get remote.origin.url
# 查看远程仓库地址
git config -l
# 查看当前git环境详细配置
git config --list
# 和上面的是一样的效果。
git config <key>
# 检查Git的某一项设置，使用上面查出来的key
git config --system --list
# 查看系统配置
git config --global --list
# 查看当前用户global配置

第一次使用时，需要配置 用户名和邮箱等：
git config --global user.name "填入自己的用户名"
git config --global user.email "填入自己的邮箱地址"


```

## 2. git clone
从远程仓库克隆一个版本库到本地。
```bash

# 默认在当前目录下创建和版本库名相同的文件夹并下载版本到该文件夹下
$ git clone <远程仓库的网址>

# 指定本地仓库的目录
$ git clone <远程仓库的网址> <本地目录>

# -b 指定要克隆的分支，默认是master分支
$ git clone <远程仓库的网址> -b <分支名称> <本地目录>
```


## 3. git init
初始化项目所在目录，初始化后会在当前目录下出现一个名为 .git 的目录。

```bash
# 初始化本地仓库，在当前目录下生成 .git 文件夹
$ git init

```
## 4. git status
查看本地仓库的状态。

```bash
# 查看本地仓库的状态
$ git status

# 以简短模式查看本地仓库的状态
# 会显示两列，第一列是文件的状态，第二列是对应的文件
# 文件状态：A 新增，M 修改，D 删除，?? 未添加到Git中
$ git status -s

```
## 5. git add
把要提交的文件的信息添加到暂存区中。当使用 git commit 时，将依据暂存区中的内容来进行文件的提交。

```bash
# 把指定的文件添加到暂存区中
$ git add <文件路径>

# 会监控工作区的状态树，使用它会把工作时的所有变化提交到暂存区，包括文件内容修改(modified)以及新文件(new)，但不包括被删除的文件。
$ git add .

# 添加所有修改、已删除的文件到暂存区中
$ git add -u [<文件路径>]
$ git add --update [<文件路径>]

# 添加所有修改、已删除、新增的文件到暂存区中，省略 <文件路径> 即为当前目录
$ git add -A [<文件路径>]
$ git add --all [<文件路径>]

# 查看所有修改、已删除但没有提交的文件，进入一个子命令系统
$ git add -i [<文件路径>]
$ git add --interactive [<文件路径>]


```
## 6. git commit
将暂存区中的文件提交到本地仓库中。

```bash
# 把暂存区中的文件提交到本地仓库，调用文本编辑器输入该次提交的描述信息
$ git commit

# 把暂存区中的文件提交到本地仓库中并添加描述信息
$ git commit -m "<提交的描述信息>"

# 把所有修改、已删除的文件提交到本地仓库中
# 不包括未被版本库跟踪的文件，等同于先调用了 "git add -u"
$ git commit -a -m "<提交的描述信息>"

# 修改上次提交的描述信息
$ git commit --amend


```
## 7. git remote

操作远程库。

```bash
# 列出已经存在的远程仓库
$ git remote

# 列出远程仓库的详细信息，在别名后面列出URL地址
$ git remote -v
$ git remote --verbose

# 添加远程仓库
$ git remote add origin  <远程仓库的URL地址>

# 修改远程仓库的别名
$ git remote rename <原远程仓库的别名> <新的别名>

# 删除指定名称的远程仓库
$ git remote remove <远程仓库的别名>
$ git remote remove origin


# 修改远程仓库的 URL 地址
$ git remote set-url <远程仓库的别名> <新的远程仓库URL地址>


```
## 8. git pull

从远程仓库获取最新版本并合并到本地。
首先会执行 git fetch，然后执行 git merge，把获取的分支的 HEAD 合并到当前分支

```bash
# 从远程仓库获取最新版本。
$ git pull
#  用master举例
$ git pull origin master


```

## 9. git push
把本地仓库的提交推送到远程仓库。


```bash
# 把本地仓库的分支推送到远程仓库的指定分支
$ git push <远程仓库的别名> <本地分支名>:<远程分支名>
$ git push origin master

# 删除指定的远程仓库的分支
$ git push <远程仓库的别名> :<远程分支名>
$ git push <远程仓库的别名> --delete <远程分支名>


```
## 10. git branch
操作 Git 的分支命令。

```bash
# 列出本地的所有分支，当前所在分支以 "*" 标出
$ git branch

# 列出本地的所有分支并显示最后一次提交，当前所在分支以 "*" 标出
$ git branch -v

# 创建新分支，新的分支基于上一次提交建立
$ git branch <分支名>

# 修改分支名称
# 如果不指定原分支名称则为当前所在分支
$ git branch -m [<原分支名称>] <新的分支名称>
# 强制修改分支名称
$ git branch -M [<原分支名称>] <新的分支名称>

# 删除指定的本地分支
$ git branch -d <分支名称>

# 强制删除指定的本地分支
$ git branch -D <分支名称>


```

## 11. git checkout
检出命令，用于创建、切换分支等。

```bash
# 切换到已存在的指定分支
$ git checkout <分支名称>

# 创建并切换到指定的分支，保留所有的提交记录
# 等同于 "git branch" 和 "git checkout" 两个命令合并
$ git checkout -b <分支名称>

# 创建并切换到指定的分支，删除所有的提交记录
$ git checkout --orphan <分支名称>

# 替换掉本地的改动，新增的文件和已经添加到暂存区的内容不受影响
$ git checkout <文件路径>


```







