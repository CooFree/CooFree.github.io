---
title: ReacNative学习
date: 2018-06-01 15:49:11
tags:
categories:  学习
---

####  React-Native入门指南
> https://github.com/vczero/react-native-lesson

####  React-Native各类学习资源
> https://github.com/reactnativecn/react-native-guide

####  iOS打包到真机
> https://blog.csdn.net/ailongyang/article/details/54866469
```objective-c
1.进入rn项目的ios工程文件夹，找到和rn项目同名的文件件，打开AppDelegate.m文件，将这一行注释掉(为了方便真机和模拟器间的切换，尽量注释)：

jsCodeLocation = [[RCTBundleURLProvider sharedSettings] jsBundleURLForBundleRoot:@"index.ios" fallbackResource:nil];
新加一行：

jsCodeLocation = [[NSBundle mainBundle] URLForResource:@"index.ios" withExtension:@"jsbundle"];
如果需要切换回模拟器调试，只需要将新加这行注释掉，并恢复原代码即可。

新加这行代码大概意思就是告诉native rn代码的入口，我们会在下一步生成这个jsbundle。

 

2.打开终端，进入你的rn工程，在根目录下执行bundle命令：

react-native bundle --entry-file ./index.ios.js --bundle-output ./ios/bundle/index.ios.jsbundle --platform ios --assets-dest ./ios/bundle --dev false
```

####  问题
> https://www.jianshu.com/p/98c8f2a970eb

> lsof -n -i4TCP:8081<br>
> kill -9<br>
> rm -rf node_modules && npm i