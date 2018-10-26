---
layout: post
title: Linux_Android交叉编译
tags:
  - 原创分享
date: '2018-10-26'
---

* * *
### 又是一轮圆月时

# 记录一下对 x86 平台与 arm 平台的交叉编译

# 1.准备工作

- 安装 gcc: 
  `sudo apt-get install arm-linux-gnueabi-gcc` 
- 安装g++: 
  `sudo apt-get install arm-linux-gnueabi-g++`
- 安装cmake: 
  `sudo apt-get install cmake` 
  `sudo apt-get install cmake-gui` 

# 2.准备`toolchain`工具

这个工具很强大，可以让 camke 实现全自动！ 
以 openCV 为例，其中有别人已经造好的轮子。 
位于 `opencv/platforms/linux` 目录中（3.4 版的比较全，2.4 版可能会有缺失，从 3.4 版中拷贝即可）。

# 3.编译依赖工程——以 openCV 为例

1. 切换至 opencv 源目录 。
2. `mkdir build_arm`
3. `cmake -DCMAKE_TOOLCHAIN_FILE=../platforms/linux/arm-gnueabi.toolchain.cmake ..`
4. 等待直到 cmake 完成 。
   ![](http://ww1.sinaimg.cn/large/6db7045egy1fwlyon2qfuj2070013t8i.jpg)
5. 如果安装了`cmake-gui`可以双击![](http://ww1.sinaimg.cn/large/6db7045egy1fwlyseos40j204702eq2r.jpg)设置编译选项。建议去掉 `BUILD_DOCS`和 `BUILD_TEST` 的勾，然后重新点击 `Configure`,`Generate`,生成 cmake cache。
6. `make -j4` 开始编译 。
   ![](http://ww1.sinaimg.cn/large/6db7045egy1fwlyxvnjjdj20k90blgoa.jpg)
   ![](http://ww1.sinaimg.cn/large/6db7045egy1fwm0g4qxekj20k00anq50.jpg)

注：如果勾选了 Eigen，注意设置 `EIGEN_INCLUDE_PATH` 否则可能会出现 `fatal error: unsupported/Eigen/MatrixFunctions: No such file or directory`错误

# 3.编译我们的工程

1. 切换到才工程目录，`mkdir build_arm`。
2. 将 `toolchain`拷贝到我们的 build 目录，linux 目录下的几个 `toolchain` 都一起拷贝。
3. `cmake -DCMAKE_TOOLCHAIN_FILE=./arm-gnueabi.toolchain.cmake ..`
   ![](http://ww1.sinaimg.cn/large/6db7045egy1fwm0oj1yfgj20is02k74d.jpg)
4. 双击`CMakeCache.txt`指定`OpenCV_DIR`为刚才编译生成的目录。然后重新点击 `Configure`,`Generate`,生成 cmake cache。
5. `make`等待编译完成。
    ![](http://ww1.sinaimg.cn/large/6db7045egy1fwm1vsf631j20jy04rmxz.jpg)
   6.执行，因为是交叉编译的，在 linux 上执行不了，交叉编译成功。
   ![](http://ww1.sinaimg.cn/large/6db7045egy1fwm1x3u8z1j20gq010mx6.jpg)
