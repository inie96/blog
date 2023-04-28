---
title: webpack
date: 2023-04-24 22:51:33
tags:
    - webpack
categories:
    - 笔记
---
详见下文
<!--more-->

### 内容概述

+ 认识webpack
+ webpack的安装
+ webpack的起步
+ webpack的配置
+ loader的使用
+ webpack中配置vue
+ plugin的使用
+ 搭建本地服务器

### 什么是webpack
+ 包含两个核心：模块 和 打包
+ 打包工具：grunt/gulp/webpack
![ivPVtb.png](https://i.328888.xyz/2023/04/26/ivPVtb.png)

### 前端模块化
+ 打包生成大部分浏览器可以识别的代码
+ 不仅js可以模块化，css图片等都可以
+ 处理各个模块之间的依赖，形成关系网
+ webpack支持前述各种模块化规范
![ivPN2H.png](https://i.328888.xyz/2023/04/26/ivPN2H.png)
+ 打包：前端用的多的是webpack
![webpack和gulp对比](https://i.328888.xyz/2023/04/26/ivPTpv.png)

### webpack和node和npm的关系

+ 模块化开发->webpack模块化打包->打包文件放到服务器->用户访问浏览器访问服务器可以获取到内容
+ webpack为了正常运行，必须依赖node环境
+ node环境为了正常执行很多代码，需要很多依赖包
+ npm工具（node package manager）是安装node必备的，用来方便管理各种依赖包

### webpack安装 

+ webpack依赖node环境，所以先安装node(node版本不小于8.9)
+ 使用node中的包管理工具npm安装webpack
+ vue cli2 依赖 webpack3.6.0版本
+ -g 表示全局安装
![ivTmaL.png](https://i.328888.xyz/2023/04/26/ivTmaL.png)

### webpack起步

+ 项目重要文件
  + src 
    dist->distribution(发布)
+ webpack会自动处理模块之间的依赖，所以只打包main.js的文件，其他的依赖关系交给webpack处理
+ 开发流程(webpack基本使用)：
  + src中使用模块化方式开发->使用webpack打包main中的代码到dist->把dist中代码引入index.html就可以显示开发的内容

![i9vUOp.png](https://i.328888.xyz/2023/04/27/i9vUOp.png)
![i9vtav.png](https://i.328888.xyz/2023/04/27/i9vtav.png)
![i9vk03.png](https://i.328888.xyz/2023/04/27/i9vk03.png)

### webpack配置

+ 配置打包路径——入口出口配置
  ![iJQyBo.png](https://i.328888.xyz/2023/04/29/iJQyBo.png)

  + 想要更加智能的输入一个简单的指令就可以打包，而不是在命令行全部敲上从哪打包到哪

  + 此时我们需要通过一个配置文件告诉webpack这系列操作

  + 配置文件固定名——webpack.config.js

  + npm init 执行后 生成 package.json，这个文件告诉我们当前项目里一些信息的

  + npm install 如果 package.json 中有依赖 会根据这个文件给项目安装依赖

  + 如果要用到node的相关东西，要先建上package.json

  + 我们要用到node里的path，path模块有个函数resolve可以对文件路径进行拼接

  + path.resolve(__dirname,'dist')拿到绝对路径

  + __dirname是node上下文的一个全局变量，他保存的就是当前webpack.config.js这个文件所在的路径
  ![iJ1OdX.png](https://i.328888.xyz/2023/04/28/iJ1OdX.png)


+ webpack命令和npm run build命令映射
+ 
  ![package.json定义打包 ](https://i.328888.xyz/2023/04/29/iJQDDV.png)
  ![iJQ4JN.png](https://i.328888.xyz/2023/04/29/iJQ4JN.png)
  + 在package.json文件中scripts中添加build对应webpack，这样在命令行输入npm run build 时 执行的就是webpack这条命令 
  ![iJ1BNb.png](https://i.328888.xyz/2023/04/28/iJ1BNb.png)

+ webpack本地安装配置

  + 如果全局安装的webpack与本地克隆下来的项目的webpack版本不一致时，打包会报错
  + 要配置webpack优先使用本地版本打包，此时本地需要安装webpack
  + 执行命令npm install webpack@3.6.0 --save-dev
  + 开发时依赖与运行时依赖，webpack只在开发时打包模块化文件，运行在服务器就没用了
  ![iJ11rC.png](https://i.328888.xyz/2023/04/28/iJ11rC.png)
  ![iJ1QhP.png](https://i.328888.xyz/2023/04/29/iJ1QhP.png)
  + 如果直接在终端webpack此时用的是全局的webpack（除非找到wcj文件下再执行wbpk），而定义build脚本后运行npm run build则是优先在本地寻找wbpk版本，本地没有再去全局找



















### 文件路径配置——给文件起别名

![ioNUi3.png](https://i.328888.xyz/2023/04/24/ioNUi3.png)
resolve 解决路径相关的问题
extensions 导入文件后缀可省略
alias 取别名
'@':resolve('src') 给src取个别名
常用文件别名
![ioN3Cc.png](https://i.328888.xyz/2023/04/24/ioN3Cc.png)

+ 当在DOM中标签引入取别名的路径必须要增加~
![ioNRgA.png](https://i.328888.xyz/2023/04/24/ioNRgA.png)