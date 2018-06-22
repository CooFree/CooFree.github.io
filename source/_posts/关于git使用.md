---
title: git的基本操作以及hexo主题个性化设置
date: 2018-06-01 15:49:11
description: 
tags:
categories:  学习
---

##  hexo 博客

1、 多台电脑操作hexo个人网站<br>
https://blog.csdn.net/Zhangxiaorui_9/article/details/79723288

2、如何生成SSH key<br>
https://blog.csdn.net/u014702999/article/details/52779319

3、hexo的next主题个性化配置教程<br>
https://segmentfault.com/a/1190000009544924

## git基本使用
https://blog.csdn.net/qq_32531823/article/details/53259822<br>
https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/0013758392816224cafd33c44b4451887cc941e6716805c000

## git遇到的问题
##### 1、 git commit 没写-m  说明进入vim模式的处理
```
输入i，进入insert输入模式，输入说明
输入完后，按ESC，下方insert消失
输入：，再输wq，回车。
```

##### 2.、提交代码 发现空目录
```
提交代码到服务器后发现git clone下来的有些目录是空的。
查看服务器的目录果然是空的。看本季git add .    后查看git  status 

modified: xxx(modified content, untracked content)
大概意思是xxx目录没有被跟踪。那自然push上去的时候是空的了
解决办法：后来发现这主要是xxx目录下有一个.git 目录(隐藏文件，按shift+common+.可显示)，
可能是被人给你这个目录的时候里面有了.git目录。删除.git目录。重新git add .就可
```
