---
title: 从零开始构建个人博客
date: 2022-05-25 15:58:37
tags:
---

翻到五年前创建的博客，发现只写了一篇文章，源码也没有上传到github，于是重新构建一个，也是给css的新手教程。

总体思想简单来说是用hexo工具构建，发布在github网站上。

## 申请github账号

到[GitHub](https://github.com/)官网，点击[Sign up]注册个人账号。
登录后点击右上角的用户头像菜单，创建一个项目，
![创建目录](../images/how_to_build_your_blog/create_repo.png)
名字格式必须为`xxx.github.io`，填写名称以后点击create按钮。
![填写目录信息](../images/how_to_build_your_blog/create_repo_1.png)

然后访问 https://xxx.github.io/， 这就是你的博客地址了，这时候页面是白的，因为我们还没有添加网页，稍后的步骤会说明。



## 环境准备

因为创建博客需要写代码，接下来我们来准备所需要的编程环境。

- node.js

访问[Node](http://nodejs.cn/download/)官网，选择“长期支持版本”，下载对应电脑系统的安装包（.msi文件）。
![下载node安装包](../images/how_to_build_your_blog/download_node.png)
点击安装，注意安装的目录最好选择c盘（“/c/nodejs/”），其他选项直接默认即可。
![下载node安装包](../images/how_to_build_your_blog/install_node.png)

- git

- hexo
