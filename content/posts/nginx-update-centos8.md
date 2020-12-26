---
title: "CentOS 8.3 升级默认 nginx"
date: 2020-12-26T00:03:47+08:00
draft: false
description: "CentOS 8.3默认yum的nginx版本太低了"
tags: [blog]
---
## 先添加中科大的仓库
```
vim /etc/yum.repos.d/nginx.repo
```

里面的内容如下：

```
[nginx-mainline]
name=nginx mainline repo
baseurl=http://mirrors.ustc.edu.cn/nginx/mainline/centos/$releasever/$basearch/
gpgcheck=0
enabled=1
module_hotfixes=true
```

## 升级

```
yum update nginx
```

## 查看nginx版本

```
nginx -v
```