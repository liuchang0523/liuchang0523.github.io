---
layout: post
title: 修改默认Windows SDK版本
date: 2017-12-28
tags: 原创分享
---
---

## 适用情况

使用VS2017+Qt5新建Qt程序时，Windows SDK版本默认被设置为8.1。  
而VS2017安装的Windows SDK版本为10.0.16299.0。  
每次都需要修改SDK版本才能进行编译。如果不修改则会报错。
![](http://lcloveqq.me/assets/images/2017-12-28/9.png)
![](http://lcloveqq.me/assets/images/2017-12-28/1.png)
![](http://lcloveqq.me/assets/images/2017-12-28/2.png)



## 自己动手修改默认Windows SDK版本为10.0.16299.0

找到Qt VS Tools安装目录
`C:\Users\***\AppData\Local\Microsoft\VisualStudio\15.0_40f57358\Extensions`
![](http://lcloveqq.me/assets/images/2017-12-28/3.png)

这里是`Extensions`的安装目录，文件夹内即安装的插件的内容（名字是随机的）。

找到Qt VS Tools的目录
![](http://lcloveqq.me/assets/images/2017-12-28/4.png)

打开`\ProjectTemplates\VC\Qt\1033`，这里就是创建模版存放的位置。找到需要修改的模版，比如我要修改gui。
![](http://lcloveqq.me/assets/images/2017-12-28/5.png)

进入目录，用记事本打开`gui.vcxproj`项目文件。
![](http://lcloveqq.me/assets/images/2017-12-28/6.png)

在`PropertyGroup`里面添加`<WindowsTargetPlatformVersion>10.0.16299.0</WindowsTargetPlatformVersion>`，保存即可。
![](http://lcloveqq.me/assets/images/2017-12-28/7.png)

再创建的Gui程序的默认Windows SDK版本就是想要的10.0.16299.0了。
![](http://lcloveqq.me/assets/images/2017-12-28/8.png)