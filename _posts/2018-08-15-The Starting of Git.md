---
layout: post
title: 'git用法'
subtitle: 'git用法'
date: 2018-08-15
categories: 技术
cover: ''
tags: jekyll 前端开发 设计
---

### 代码高亮
``` python
@requires_authorization

```

### todolist

- [x] 已完成
	- [x] 已完成2
- [ ] 代办

## git简介和安装
### 安装，
[下载地址](https://git-scm.com/downloads)  
下载后默认安装就行，菜单中，Git Bash  
然后配置账户名和密码，具体百度

```java
git config --global user.name "Your Name" 
git config --global user.email "email@example.com" 
```

### 创建版本库 
第一步使用`git init`命令，添加文件到仓库可以分两步：  
-第一步使用命令`git add <file>`添加 
-第二步使用`git commit -m "说明"`完成   
## 时光穿梭机   
使用`git status`查看状态情况   
使用`git diff`查看不同  
### 版本回退
使用`git log`查看日志，可以使用`git log --pretty=oneline`让它变成一行   
版本表示`HEAD^`表示上一个版本，`HEAD~x`表示x前的版本   
退回上一个版本使用`git reset --hard HEAD^`退回上个版本也可以通过`git reset --hard xxxx`退回到xxx版本指定版本号的版本   
通过`git reflog`查看自己的所有命令 
### 工作区和缓存区 
#### 工作区就是目前工作目录，如我的D:/ 
#### 版本库就是.git版本库，其中存了stage的暂存区，以及第一个分支master以及指向它的HEAD图
![](https://cdn.liaoxuefeng.com/cdn/files/attachments/001384907702917346729e9afbf4127b6dfbae9207af016000/0)
其实git status查看的是暂存区的文件信息  
![](https://cdn.liaoxuefeng.com/cdn/files/attachments/001384907720458e56751df1c474485b697575073c40ae9000/0)  
### 管理修改
git优秀地方在于它管理的是修改，不是文件
### 撤销修改
使用`git checkout -- file`来丢弃工作区的修改  
使用`git reset HEAD file`丢弃暂存区的内容
### 删除文件
## 远程仓库
所以过程是：
-mkdir test
-cd test
-git init()
-远程创建test
-git remote add origin git@github.com:sczcl/mytest.git
-git push -u origin master如果远程有文件，得先git pull --rebase origin master下载
如果推不上去，则表示本地仓库为空，需要添加文件后再推送。
使用
`git add .`
可以添加全部文件
使用` git remote add origin git@github.com:sczcl/mytest.git`添加远程仓库，其中origin是远程仓库，miche是用户名，使用`git push -u origin master`把本地库的所有放到远程上  
### 克隆
创建一个项目，然后`git clone git@github.com:michaelliao/gitskills.git` 取下来
## 分支管理
### 创建和合并分支
git中版本控制分支是master分支
![](https://cdn.liaoxuefeng.com/cdn/files/attachments/0013849087937492135fbf4bbd24dfcbc18349a8a59d36d000/0)
用`git checkout -b dev`创建并切换到dev分支
使用`git branch`查看分支
合并`git merge dev`然后就能使用`git branch -d dev`删除dev分支
当master和分支都有新信息之后，不能快速合并。使用`git status`查看冲突。在<<<<<<<和======之间是当前分支，======和>>>>>>之间是有问题分支，修改之后就行
使用`git log --graph --pretty=oneline --abbrev-commit`查看提交
### 分支管理策略
合并分支Git可以的话会默认用Fast forward模式，这种模式下删除分支会丢弃分支信息。强制禁用这个模式的时候，Git会在merge的时候产生一个新的commit，我们可以用--no-ff的方式git merge，首先`git checkout -b dev`然后修改提交，然后`git merge --no-ff -m "merge with no-ff" dev`合并
### bug分支
在当前分支工作的时候发现还有bug不能提交，就是在主线上有问题，但是我们是在分支线上开发的，所以需要调整。这时候所以使用Git的stash功能将当前工作存储起来，等恢复以后继续。`git stash`
修复完成以后使用`git stash list`查看存储的列表，使用两种方法恢复：
	-第一种，使用`git stash apply`这时候完成了stash内容不删除，需要手动`git stash drop`
	-第二种，用`git stash pop`这时候自动删除了
### Feature分支
为了防止出错，先建立一个Feature分支，在上面开发后合并，最后删除分支。列入开发Vulcan的新功能
### 多人协作
`git push origin 分支`推送到远程，
## 标签管理
就是对版本库打标签，确定版本
### 创建标签
首先切换到打标签的分支上，然后`git tag name`就可以打标签了，可以对指定id的打标签，`git tag name id`，或者`git tag -a name -m remark id`打标签，`git show name`看看到说明，看通过`git tag -s v`用私钥名一个标签
### 操作标签
`git tag -d name`可以删除
