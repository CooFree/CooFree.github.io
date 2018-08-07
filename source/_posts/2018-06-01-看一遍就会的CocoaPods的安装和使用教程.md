---
title: 看一遍就会的CocoaPods的安装和使用教程
date: 2018-06-01 15:49:11
tags:
categories:  学习
---

#### 什么是CocoaPods？

CocoaPods是专门为iOS工程提供对第三方库的依赖的管理工具，通过CocoaPods，我们可以更方便地管理每个第三方库的版本，而且不需要我们做太多的配置。直观、集中和自动化地管理我们项目的第三方库。

我们都有这样的经历，当我们添加第三方库的时候，需要导入一堆相关依赖库，更新的时候也要删掉重新导入然后再配置。当我们需要更新某个第三方库的时候，我们又要手动移除该库，导入新的库，然后再配置。这些是很麻烦且没有意义的工作。

当我们开始使用CocoaPods管理第三方库后，我们只需要相当少的配置，其它的一切都交由CocoaPods来管理即可，我们使用起来就更省心了。

#### 安装CocoaPods

1.首先更新gem到最新版本，在终端中输入：$ sudo gem update --system,注意不要把“$”复制上。等待一会儿会看到：


更新gem
2.删除自带的ruby镜像，终端输入：gem sources --remove https://rubygems.org/。
3.添加淘宝的镜像，终端输入：gem sources -a https://gems.ruby-china.org/(原来的淘宝镜像 https://ruby.taobao.org/已经不能用了)。
4.可以用gem sources -l 来检查使用替换镜像位置成功，结果应该只有 https://gems.ruby-china.org/ 才对。


修改镜像
5.安装CocoaPods，终端输入：sudo gem install cocoapods。
等待一会儿会看到：


安装CocoaPods
6.然后配置下CocoaPods，终端输入：pod setup。


配置CocoaPods
等待过程可能有点长，成功后会看到：


配置成功
到这里CocoaPods就安装好了。

#### 查找第三方库

比如查找MJExtension，终端输入：pod search MJExtension，第一次搜索他需要建索引，等待一会儿就可以了。


建索引中
完成后他会自动进入一个新的页面显示搜索结果，上下滑动查看更多，要退出的话按wq就可以了。以后再搜索就不需要建索引了。

查找结果

#### 引入第三方库到项目中

我先在桌面上新建一个Test项目，然后演示把MJExtension导进去。
刚开始的文件目录是这样的


原始目录.png
1,首先打开终端，cd到Test路径下。


Test

2.然后生成并编辑一个Podfile文件，命令为vim Podfile，要导入的第三方都要在这里面写上。进去后需要先按I键进入编辑状态，写完后按esc，然后按shift+zz(或者先按shift+:,再按wq)就可以保存退出了。下面的动图里面都有。
Podfile的格式大概如下，其中'Test'为你的target的名字。
platform :ios,'8.0'
target 'Test' do
pod 'MJExtension', '~> 3.0.13'
end
3.安装，命令为：pod install。


安装第三方
安装成功之后，就可以去项目里面使用了。现在的项目文件变成了这样


屏幕快照 2016-09-07 23.23.19.png
之前我们一直是双击Test.xcodeproj打开项目，以后我们就要双击Test.xcworkspace打开了，打开后发现项目里面多了红色框的部分，可以看到MJExtension已经被引入了。

多出来的文件

#### 使用第三方

你会发现当引入MJExtension的头文件时，可以#import <MJExtension.h>或者#import <MJExtension/MJExtension.h>，但是却不能在输入#import "MJExtension.h"的时候出现提示。虽然强制输入也可以编译通过，但是感觉很不爽。
解决这个问题的办法是在工程的Build Settings搜索Search，然后在User header search paths中添加$(SRCROOT)并选择recursive。


头文件不提示的解决办法

现在就可以提示#import "MJExtension.h"啦。
然后我们就可以在项目里面使用MJExtension的方法啦。

使用MJExtension

#### 增加新的第三方

如果使用过程中我还想添加其他的第三方怎么办，只要在Podfile里面接着添加，然后终端再执行pod install就可以了。

新增第三方

#### 更新CocoaPods中的第三方们。

第三方库们都有人在维护升级，我们需要隔断时间就要更新下我们工程中第三方库的版本。只需要终端输入命令pod update就可以了。

如果遇到pod install或者pod update慢的问题，原因在于当执行以上两个命令的时候会升级CocoaPods的spec仓库，加一个参数可以省略这一步，然后速度就会提升不少。加参数的命令如下：
pod install --verbose --no-repo-update
pod update --verbose --no-repo-update

#### 删除CocoaPods中的某些第三方们。

当我们需要去掉某个第三方库时，只需要在Podfile删除该引入该库的语句，然后执行pod update或者pod install就可以了。

#### 将CocoaPods从项目中删除

如果你在以后的使用过程中不想用CocoaPods了怎么办？很简单，把多出来的东西们都删掉就可以了，不过为了项目正常运行，你需要手动导入已经使用的第三方们哦。

将CocoaPods从项目中删除

#### 升级CocoaPods

升级CocoaPods版本的命令和安装CocoaPods的命令一样，都是sudo gem install cocoapods。
如果老版本升级cocoapods的时候提示Operation not permitted - /usr/bin/xcodeproj，改用命令sudo gem install -n /usr/local/bin cocoapods --pre就可以了。

#### 卸载CocoaPods

卸载CocoaPods的命令是sudo gem uninstall cocoapods


卸载CocoaPods
执行完命令后，最下面打印Successfully uninstalled cocoapods字样就代表已经成功卸载了。

#### CocoaPods Mac App的安装和使用

CocoaPods桌面应用版下载地址：https://cocoapods.org/app
打开应用会提示你是否安装命令行工具，选择install就也可以在命令行使用Pod了。省去了上面的步骤们，方便快捷的使用CocoaPods。


是否安装命令行工具
现在假如要给一个Test项目加入第三方库
1.选择File-New Podfile from Xcode Project，去选择项目的Project文件。


选择项目
2.填写自动生成的Podfile，并且安装。


Podfile
然后就可以去打开工程了，是不是比命令行简单多了。
注意：Cocoapods.app 删掉并执行命令可能会报错：Unable to locate the CocoaPods.app application bundle. Please ensure the application is available and launch it at least once


错误信息.png
这时候只要执行sudo gem install -n /usr/local/bin cocoapods命令就可以了。

#### CocoaPods官方使用指南

链接：https://guides.cocoapods.org/
有什么不了解的或者遇到错误可以去这里查看一下。