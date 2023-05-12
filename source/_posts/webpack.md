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

> ### 内容概述
> + 认识webpack
> + webpack的安装
> + webpack的起步
> + webpack的配置
> + loader的使用
> + webpack中配置vue
> + plugin的使用
> + 搭建本地服务器

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

### webpack核心概念之一——loader

+ 为了项目运行时，css文件不单独一个个引用，一样打包到bundle.js文件中，到时候只引用这一个文件就能展示了，我们引入loader这个概念

![依赖css文件](https://i.328888.xyz/2023/04/29/iKzKNE.png)
![证明打包css文件需要安装合适的loader](https://i.328888.xyz/2023/04/29/iK6VrV.png)
![样式相关loader](https://i.328888.xyz/2023/04/29/iK6x1t.png)

+ 样式loader的使用
  1. 按照命令安装
  2. 在config文件引用

+ css-loader只负责帮助你加载css文件，不负责解析css代码，也不会把css代码放到html中让样式生效

+ 配置css文件的含义
![匹配和应用](https://i.328888.xyz/2023/04/29/iKF5cF.png)
`/ \.css$/`
`.` 在正则中有特殊含义 所以 `\.` 进行转义
匹配`.css`
`^`开始
`$`结尾

![iKzN4V.png](https://i.328888.xyz/2023/04/29/iKzN4V.png)
![iKFatc.png](https://i.328888.xyz/2023/04/29/iKFatc.png)
![iKGZGd.png](https://i.328888.xyz/2023/04/29/iKGZGd.png)
![iKGDta.png](https://i.328888.xyz/2023/04/29/iKGDta.png)
![iKGw23.png](https://i.328888.xyz/2023/04/29/iKGw23.png)

### less文件处理

1. 步骤

+ 创建less文件，些一些less代码
+ 在main.js引用less文件
+ 打包main.js
+ 在index.html引用打包的js文件
+ 测试代码是否执行成功
+ 测试需要less的loader
+ 安装less-loader和less
+ 在webpack.config文件加上less规则
![iTTp4H.png](https://i.328888.xyz/2023/05/05/iTTp4H.png)
![iTT72P.png](https://i.328888.xyz/2023/05/05/iTT72P.png)


### 图片资源文件处理

+ 创建图片文件
+ 安装url-loader
+ 配置图片文件
+ 文件大小*1024比limit小——直接转成base64字符串文件
+ 比limit大——要安装file-loader(不需要再配置)
  + 会在dist文件下打包了一个图片文件，用哈希值命名的，为了不重复
  + 如果安装后找不到图片路径要配置一下路径（publicPath:'dist/'），保证引用打包后图片文件的路径正确
  + 对图片命名进行规范

![iTTQhp.png](https://i.328888.xyz/2023/05/05/iTTQhp.png)
![iTTuHv.png](https://i.328888.xyz/2023/05/05/iTTuHv.png)
![iTaZe3.png](https://i.328888.xyz/2023/05/05/iTaZe3.png)
![iTaiay.png](https://i.328888.xyz/2023/05/05/iTaiay.png)


### ES6语法处理——babel的使用

+ 很多浏览器没有支持es6，适用性差
+ 打包的时候es6都转为es5，最终bundle.js文件应该都是es5的语法
+ 安装babel-loader、babel-core、babel-prest-es2015
+ 配置相应规则
![iTa2BJ.png](https://i.328888.xyz/2023/05/05/iTa2BJ.png)
![iTam0z.png](https://i.328888.xyz/2023/05/05/iTam0z.png)


### webpack配置vue

+ 安装vue
+ 引入vue，写一些vue代码
+ 如果不配置 默认引入的vue文件是runtime-only这个版本不能用template
+ 如果配置了地址 引入的就是runtime-compiler 可以有template
  + 指定使用的vue文件路径
  ![iTQgup.png](https://i.328888.xyz/2023/05/05/iTQgup.png)
  + 同时有el和template时，template中的内容整体替换#app的div
  ![iTY7SA.png](https://i.328888.xyz/2023/05/06/iTY7SA.png)

![iTaF13.png](https://i.328888.xyz/2023/05/05/iTaF13.png)
![iTQcva.png](https://i.328888.xyz/2023/05/05/iTQcva.png)
![iTYx3c.png](https://i.328888.xyz/2023/05/06/iTYx3c.png)
![iQLLcZ.png](https://i.328888.xyz/2023/05/09/iQLLcZ.png)

![iQLajQ.png](https://i.328888.xyz/2023/05/09/iQLajQ.png)
![iQL1FE.png](https://i.328888.xyz/2023/05/09/iQL1FE.png)
![iQLqlP.png](https://i.328888.xyz/2023/05/09/iQLqlP.png)


+ .vue文件要安装两个东西
+ vue-loader —— vue文件加载
  vue-template-compiler —— vue编译
+ 这俩仅开发时使用，加载编译完就不需要了
+ vue-loader 如果大于14（估摸）需要再装个插件才能运行，要不会报错让你安装那个插件
+ 安装一个13多的版本就不报错了

+ .vue文件封装过程

#### 以上loader就讲完

### webpack另一个核心——plugin

![iQLuxX.png](https://i.328888.xyz/2023/05/09/iQLuxX.png)

1. 添加版权的plugin
![iQMWwb.png](https://i.328888.xyz/2023/05/09/iQMWwb.png)
2. 打包html的plugin
![iQM0Mz.png](https://i.328888.xyz/2023/05/09/iQM0Mz.png)
3. js丑化压缩的plugin
![iQMwca.png](https://i.328888.xyz/2023/05/09/iQMwca.png)




### 搭建本地服务器


**搭建服务器步骤**
+ 安装webpack-dev-server   webpack的本地服务
+ 配置devServer 
```
contentBase:'./dist',
inline: true
```
+ 配置 ` 'dev': 'webpack-dev-server --open' ` 执行npm run dev 就会直接打开网页

![iQM2sx.png](https://i.328888.xyz/2023/05/09/iQM2sx.png)
![iQMOyk.png](https://i.328888.xyz/2023/05/09/iQMOyk.png)
base公共
prod生产
dev开发
![配置路径脚本](https://i.328888.xyz/2023/05/09/iQMjGp.png)

### webpack配置文件的分离

base公共
prod生产
dev开发 

公共和开发/生产 文件进行合并
需要安装webpack-merge

 

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

### 扩充

1. 文件夹组织方式

+ 作为入口的main.js放在外层
其他功能js代码放在文件夹中

2. bundle的意思是包

3. gitbook这个软件写的文档同步出去的会有这个网站名
![iK6Uaw.png](https://i.328888.xyz/2023/04/29/iK6Uaw.png)

+ 非盈利组织的网站后缀叫org
+ 盈利组织用com

4. --save-dev 开发时依赖
![iK65id.png](https://i.328888.xyz/2023/04/29/iK65id.png)

5. 早期dos操作系统文件后缀名只支持3位

所以jpg和jpeg是一个文件

htm就是html

现在windows系统可以支持很多位文件后缀

6. env就是environment环境的缩写

7. exclude排除
   include包含

8. vue项目最终会编译成2个版本

+ runtime-only 代码中不能有template
+ runtime-compiler 可以有template，因为vue的代码有compiler可以编译template
+ compiler编译的意思

9. 后缀扩展名都不想写怎么配置

+ webpack.config.js中 extensions:['.vue','.js','.css']


> ### 内容回顾
> 1. 什么是webpack
> + webpack和glup对比
> + webpack依赖环境
> + 安装webpack
> 2. webpack的起步
> + webpack命令
> + webpack配置：webpack.config.js/package.json
> 3. webpack的loader
> + css-loader/style-loader
> + less-loader/less
> + url-loader/file-loader
> + babel-loader
> 4. webpack中配置vue
> 5. webpack的plugin
> 6. 搭建本地服务器
> + webpack-dev-serve
> 7. 配置文件的分离
