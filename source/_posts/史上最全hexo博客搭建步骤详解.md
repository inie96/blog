---
title: 史上最全hexo博客搭建步骤详解
date: 2022-05-21 14:08:36
cover: /image/hexo.webp
thumbnail: /image/hexo.webp
tags:
   - hexo
   - icarus
   - blog
   - 博客
categories:
   - 技术
---

我的第一篇博客，先给hexo~
<!--more-->

## 前言
本篇讲解主要参考codesheep的关于hexo搭建的视频，结合自己踩的一些坑，综合各路大神的指南而成，如果你在实践本篇博文的过程中有任何问题，欢迎和我一起交流~

>搭建博客的目的：

明确我们的目标才不会让你半途而废
* 社招、校招加分项
* 追求极客范儿
* 挑战自己，我很棒

>总览一下我们搭建hexo博客的步骤：
1. 搭建node.js环境
2. 安装加速包cnpm
3. hexo安装
4. 使用hexo搭建博客
5. 新建第一篇博文
6. 把博客部署到github
7. 博客换肤
以上就是博客搭建过程概览

下面我们按照上面的步骤逐一实现，你也可以拥有属于自己的博客哟~
操作的过程中先不用问太多为什么，照做就行了

## 1、搭建node.js环境
### 1.1 下载node.js
hexo是node.js生成的，需要node.js环境

nodejs官网：nodejs.org

nodejs官网图

建议：不要下载最新的node版本，我下载的12版本的

12版本list图

自动安装包格式.pkg

傻瓜安装，一直点同意就好了

安装的结果实际上安装了两个文件一个是node.js另一个是npm包管理器,这是搭建hexo必备

### 1.2 查看安装的node与npm版本
>打开终端
~~~
查看node版本：输入 node -v
查看npm版本：输入 npm -v
~~~
这里codesheep是在root用户下操作的
，但是到后面我使用编辑器操作文件会有点麻烦，总是需要root权限，所以这个因人而异吧

啰嗦一句~每次我们安装或者操作什么都要及时检查这个操作是否成功，程序员基操吧

## 2、安装加速包cnpm
因为国内镜像源的安装速度慢，所以我们安装一个淘宝镜像源，为一会安装hexo速度快
### 2.1利用npm安装cnpm
~~~
输入 npm install -g cnpm --registry=https://registry.npm.taobao.org
~~~
### 2.2查看cnpm版本
~~~
输入 cnpm -v
~~~
cnpm版本截图

## 3、hexo安装
### 3.1用cnpm安装hexo
~~~
输入 cnpm install -g hexo-cli
~~~
### 3.2查看hexo版本
~~~
输入 hexo -v
~~~
图

## 4、使用hexo搭建博客
### 4.1建一个空的文件夹blog
这个文件夹是存放我们博客所有内容的，那么在建文件夹前先看一下我们当前的位置，方便后续寻找我们的blog文件夹在哪
~~~
查看当前位置：输入 pwd
~~~
图
~~~
新建blog文件夹：输入 mkdir blog
进入blog：输入 cd blog
查看当前位置：输入 pwd
~~~
此时我们的路径是/blog结尾，接下来是在这个blog文件初始化我们的hexo
### 4.2 初始化hexo
~~~
初始化hexo：输入 init hexo
~~~
此时可以看到克隆到了hexo文件和默认landscape主题

进入blog文件查看初始化都自动生成了哪些文件，后续我们写博客都基于这里面的文件，瞅一眼有啥就行
### 4.3启动博客
~~~
启动hexo:输入 hexo s
~~~
此时终端会出现 http://localhost:4000/

表示我们再本地已经启动成功博客，点这个链接进来看看我们搭建的博客
以上我们的博客就搭建完成了，是不是没那么难~

### 博客有了我们开始写文章吧~
## 5、新建第一篇博文
### 5.1 创建博文
~~~
新建博文：输入 hexo n "你的博文标题"
~~~
可以看到我们的博文被创建到source/_posts目录下了，并且是.md格式的，到编辑器(我使用的是vscode)里面打开这个文件，开始写你的第一篇博文吧~

### 5.2 查看你完成的第一篇博文
写完之后，再次启动一下我们的博客，在本地查看我们新写的一篇博文

看下当前你的位置
~~~
输入 pwd
~~~
我们后面的操作依然要回到blog文件下面

接着输入 hexo clean 清理一下
~~~
输入 hexo g 生成一下
~~~
先不要问为啥，你以后会知道，照做
~~~
输入 hexo s 启动
~~~
刷新刚打开的网址，可以看到我们刚写的博文已经出现了

## 6、把博客部署到github
我们想要一个远端地址可以查看我们的博客，推荐github部署方式，免费万岁！
### 6.1 创建github仓库
网址：github.com

没有账号的自己注册，不赘述啦，毕竟我们的主题是hexo

登录进来

页面右上角，头像的左边👈🏻有个➕号，➕号下拉框里点New repository新建一个仓库

点进来填写Repository name

命名规范：你的用户名.github.io

你的用户名就是旁边的Owner里面写的

比如我的用户名：inie96

那么就是 inie96.github.io

用户部署个人博客的github仓库的命名必须是这个

点 Create repository 创建仓库完成

### 6.2 安装git部署插件

终端进入到blog文件下
~~~
安装git：输入 cnpm install --save hexo-deployer-git
~~~
### 6.3 设置blog文件下的_config.yml文件

来编辑器里，找到blog文件下的_config.yml文件

最下面有个# Deployment 找到他

在他下面配置上这三行
~~~
type: git
repo: git@github.com:inie96/inie96.github.io.git
（这里配置成我们刚创建仓库的ssh地址，注意是ssh）
branch: master
~~~
图

最终长这样

### 6.4 向github部署博客

终端回到blog

输入 hexo d

接着会提示你输入github账号密码

部署完成后去刷新刚创建的github仓库，此时已经有文件进来了，就是部署成功了

把仓库名拿出来访问inie96.github.io就可以在远端查看博客了~

以上我们的博客远端部署完成

## 7、博客换肤

### 7.1 挑选皮肤

网址：https://hexo.io/themes/

### 7.2 进入喜欢的皮肤的仓库

我选的是icarus

仓库地址：https://github.com/ppoffice/hexo-theme-icarus

### 7.3 下载主题

回到终端blog下面

克隆/下载主题：输入 git clone https://github.com/ppoffice/hexo-theme-icarus.git themes/icarus

themes/icarus 是我们要下载到的文件位置

此时在文件夹中打开这个路径就可以看到我们下载的主题文件

### 7.4 给我的博客配置icarus主题

修改刚刚我们也改过的blog文件下的_config.yml文件

这个文件还蛮重要

~~~
修改 theme: icarus
~~~
修改成themes下的icarus文件名

图

此时我们再次

~~~
hexo clean
hexo g
hexo s
~~~

在本地查看一下更换的主题

打开 http://localhost:4000/

查看没有问题，推送到远端
~~~
输入 hexo d
~~~
在远端地址查看更改后的皮肤，换肤完成

## 总结

1. 安装node
2. 安装cnpm
3. 安装hexo
4. 初始化hexo：init hexo
5. 创建hexo博文：hexo n
6. 部署hexo到github
   * 创建github仓库
   * 安装git
   * 配置文件
   * hexo d
7. 博客换肤
   * 下载主题 git clone
   * 配置文件
   * hexo d

hexo四件套
~~~
hexo clean
hexo g
hexo s
hexo d
~~~

欢迎观看~

完结撒花~