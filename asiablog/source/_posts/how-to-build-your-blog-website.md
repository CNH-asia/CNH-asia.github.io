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

node会附带安装npm（前端包管理器），在cmd（快捷键`Win`+`R`）输入 `node -v` 和 `npm -v` 查看对应的版本。


- git

git是一个免费开源的快速版本控制工具，用于管理我们的项目，访问[官网](https://git-scm.com/)下载，
![下载git安装包](../images/how_to_build_your_blog/download_git.png)
安装时勾选默认的选项即可。
安装完成后在桌面点击鼠标右键，会发现菜单中多了两个git的选项，
![查看git菜单](../images/how_to_build_your_blog/git_menu.png)
选择`git bash here`打开git窗口，这里是我们输入命令来进行项目代码版本管理的地方，简单来说就是更新代码提交代码等等操作，在后面的步骤中会详细说明。
![打开git窗口](../images/how_to_build_your_blog/git_window.png)


- hexo

[hexo](https://hexo.io/docs/)是我们写博客的工具，在cmd输入`npm install hexo -g`全局安装，安装完毕后`hexo -v`查看版本信息。
![查看hexo版本](../images/how_to_build_your_blog/hexo_v.png)


到这里我们就准备好了所需的环境，接下来就要进入到编程部分了。


## 编写博客

### 创建项目

首先我们打开刚刚创建的github项目，复制ssh地址克隆到本地，
![克隆项目](../images/how_to_build_your_blog/clone_1.png)
在cmd中输入命令`git clone ${复制的ssh地址}`，回车，这时候会看到提示没有权限，因为没有配置key，也就是密钥。

打开cmd，依次输入以下命令：

```bash
ssh-keygen -t rsa -b 4096 -C "github注册的邮箱"
eval $(ssh-agent -s)
ssh-add ~/.ssh/id_rsa
clip < ~/.ssh/id_rsa.pub
```
完成最后一步以后就复制了生成的key，回到github项目，打开 设置->deploy keys->add deploy key，
![添加ssh key](../images/how_to_build_your_blog/sshkey_1.png)
粘贴到key文本框，title输入框中随便填个名字，勾选 Allow write access，点击添加。 
![添加ssh key](../images/how_to_build_your_blog/sshkey_2.png)
再回到cmd中输入命令`git clone ${复制的ssh地址}`，回车，成功克隆。

### 启动项目

进入到项目文件夹的根目录中，执行`hexo init myblog`，可以看到生成了一个博客项目，`cd myblog`，执行
```
hexo g //生成网页文件
hexo s //启动服务
```
服务默认地址 http://localhost:4000/ ，访问即可看到博客的首页。

> 注：myblog为项目的文件夹名称，可以随意命名，但避免中文。

#### 目录结构

```js
├─.github
├─node_modules
├─public //hexo g 命令生成的文件
├─scaffolds //文章模板
├─source //源码
├─themes //主题文件
├─_config.yml //hexo配置文件
├─.gitignore //git忽略的文件
├─package.json //项目配置文件
```

### 编写博客

下面我们来新建一篇文章，在myblog下执行`hexo new post mypaper`，会生成mypaper.md文件，编辑文件并保存，可以看到网页内容也随之变化了。

### markdown语法简单说明

markdown是一种标记语法，能快速生成html网页，网上有很多教程，这里就不再赘述。贴一篇[文章](https://www.jianshu.com/p/191d1e21f7ed)供参考。

### 主题

hexo支持修改[主题](https://hexo.io/themes/)，以本站使用的主题[one-paper](https://github.com/zheli-design/hexo-theme-one-paper)为例，下载zip包后解压到themes目录下，更改 _config.yml 配置：theme: one-paper，执行`hexo s`预览效果。
![主题](../images/how_to_build_your_blog/theme.png)

### 部署到github

1.在myblog目录下执行命令`npm i hexo-deployer-git --save`，修改_config.yml配置：
```js
url: https://cnh-asia.github.io //博客地址
```

```
deploy:
  type: git
  repo: https://github.com/CNH-asia/CNH-asia.github.io //项目地址
  branch: master //代码分支，默认是master
  token: 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
```
token的获取方法：访问[设置](https://github.com/settings/tokens)，
![主题](../images/how_to_build_your_blog/generate_token.png)
执行

```bash
hexo clean //清除上次生成的文件
hexo g //生成文件
hexo d //部署到github
```
如果成功连接会弹出一个git窗口，可以输入token进行登录，成功的信息：
![成功的打印信息](../images/how_to_build_your_blog/success.png)
完成后访问博客主页，最新的内容已经成功发布了。
如果提示timeout则表示连接超时，需要翻墙。
> 注：建议把博客发布到master分支，新建一个分支用来保存源码。




