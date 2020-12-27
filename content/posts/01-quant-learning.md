---
title: "01-量化选股系统环境搭建"
date: 2020-12-26T14:15:11+08:00
draft: false
description: "一直想搞一个量化选股的程序，通达信太慢了，而且不适合程序员，所以我慢慢花时间搞一个友好的网站来实现"
tags: [量化选股系统]
---
准备搭建一套系统，让大家可以根据北向资金、欧奈尔的RPS还有一些其他的策略很方便的选出股票来。为啥搞这个呢，实在是通达信这个软件太慢了，不如自己用pyton和tushare搞一下，具体有哪些条件以后再列，先卖出第一步，配置系统的开发环境。
## 安装anaconda

安装好后我创建了一个stock的环境，我这里统一把股票都放到这个环境里，不会命令的就用图形界面也行。

切换环境用下面这个命令。

```
source active stock
```

## 安装tushare

tushare是个什么东西我就不多说了。
安装代码：

```bash
pip install tushare
```
安装好后验证下：
```bash
python
import tushare
print(tushare.__version__)
```

正常情况有输出的，如果出错了就去看下出了什么问题，我这里忘了安装pandas，所以用下面的命令再安装下pandas。

```bash
pip install pandas
```

再只想上面的命令验证tushare是否安装成功，我得到的版本信息如下：

> 1.2.62

## 安装django

我决定还是用django来把这个网站写出来，所以先装个django的框架吧

```
pip install Django
```

安装好后验证下：

```
>>> import django
>>> print(django.get_version())
```

> 3.1.4

基本上就这样了，剩下就是网站前台后台还有数据库什么的建设了，这个以后继续。