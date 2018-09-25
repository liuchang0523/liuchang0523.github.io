---
layout: post
title: pyinstaller 打包py脚本成exe
tags:
  - 原创分享
date: '2018-09-24'
---
---

# 使用 `pyinstaller`打包 py 脚本
1. 到 [github](https://github.com/pyinstaller/pyinstaller) 下载`pyinstaller` Windows 平台下载 zip，解压。
2. 切换到目录， 运行`python setup.py install`开始安装。
3. 切换到要打包的程序目录 `pyinstaller -F test.py`。(-F 打包成单文件 运行会很慢，但是简洁) 

# Problem1
>RecursionError: maximum recursion depth exceeded 

![](http://ww1.sinaimg.cn/large/6db7045egy1fvky260pknj20qo0dcq37.jpg) 
## 解决方案
找到`*.spec`文件，在第二行添加
```python
import sys
sys.setrecursionlimit(5000) # or more
```
执行`pyinstaller test.spec` 

参考文献： 
 [pyinstaller and matplotlib gets maximum recursion depth exceeded](https://stackoverflow.com/questions/30677110/pyinstaller-and-matplotlib-gets-maximum-recursion-depth-exceeded)

# Problem 2
>UnicodeDecodeError: 'utf-8' codec can't decode byte 0xce in position 110: invalid continuation byte 

![](http://ww1.sinaimg.cn/large/6db7045egy1fvkydohqycj20qo0dcjru.jpg)

## 解决方案
控制台输入`chcp 65001`将 cmd 切换至 utf-8 编码，重新运行`pyinstaller test.spec`

# 安装成功
![](http://ww1.sinaimg.cn/large/6db7045egy1fvkzcqtipcj20qo0avglw.jpg)
![](http://ww1.sinaimg.cn/large/6db7045egy1fvkzgh7u7aj20xk0h1aba.jpg)
