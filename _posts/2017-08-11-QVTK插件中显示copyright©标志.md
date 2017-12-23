---
layout: post
title: QVTK插件中显示copyright©标志
date: 2017-08-11
tags: 原创分享
---
---
# 问题

©符号因为字符集的原因在VS2013中使用Qt的时候显示不正常。

网上查阅多种解决方案，尝试多种字符集均无法结局此问题。

# 但是

在QDesiner中打开ui文件，然后控件的title设置名字中包涵©可显示正常。

# 解决方案1

打开插件生成的ui_XXX.h文件，找到©字符所对应的转义字符“\302\251”，替换掉需要©字符的位置即可。

![](http://upload-images.jianshu.io/upload_images/5865351-bc6521f66fa5f117.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

# 解决方案2

使用宏QStringLiteral("©")；

