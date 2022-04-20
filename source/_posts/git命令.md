---
title: git命令
date: 2021-10-18 22:16:33
tags: git命令
categories: 技术积累
---

﻿### GIT命令行提交到gihub

git init

检查加密传输是否设置：ssh -T git@github.com

git pull origin master
$ git remote add origin git@github:你的github远程地址.git
输入命令行 
`$ git add . 
//注意add后面是有”.“的，而且和add之间有一个空格 
$ git commit -m "提交说明”

$ git push origin master

移除原来设置的远程地址：git remote rm origin
再重新用git remote add origin git@github:你的github远程地址.git设置再重复上述提交步骤。




### 使用git LFS提交大文件

git lfs track “*.zip”
git add .gitattributes
cat .gitattributes  #自动生成的文件，需一并提交到 Git，否则 Clone 项目的时候 Git LFS 不起作用

git add 提交文件名
git commit -m ‘xxx’
git push 

删除提交记录：
git log 
得出记录名字

git reset --hard 记录ID

git push origin HEAD --force
