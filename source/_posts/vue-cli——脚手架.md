---
title: Vue CLI——脚手架
date: 2023-05-09 22:30:33
tags:
    - Vue CLI
categories:
    - 笔记
---
详见下文
<!--more-->


### 什么是Vue CLI

+ CLI是 Command Line Interface 命令行界面 俗称脚手架

![iQMGWt.png](https://i.328888.xyz/2023/05/09/iQMGWt.png)

+ 主要作用就是快速搭建**vue开发环境**和对应的**webpack配置**（最重要就是生成webpack配置）


### 准备工作

+ Vue CLI 使用前提——Node
![iQMQ4x.png](https://i.328888.xyz/2023/05/09/iQMQ4x.png)

+  Vue CLI 使用前提——Webpack
![iQMqdL.png](https://i.328888.xyz/2023/05/09/iQMqdL.png)

### Vue CLI使用

+ 安装 Vue CLI
+ 拉取脚手架2
+ Vue CLI2初始化项目
+ Vue CLI3初始化项目
![iQPnAZ.png](https://i.328888.xyz/2023/05/09/iQPnAZ.png)
![iQPkuQ.png](https://i.328888.xyz/2023/05/09/iQPkuQ.png)
ES(js)Lint 会让es代码写的更规范
e2e test 就是 end to end 端到端测试
![iqejJv.png](https://i.328888.xyz/2023/05/11/iqejJv.png)

### cli2创建项目是runtimecompiler和runtimeonly的区别（面试可能问）

仅在main.js中存在区别
![iuIepF.png](https://i.328888.xyz/2023/05/12/iuIepF.png)
![iuIz9H.png](https://i.328888.xyz/2023/05/12/iuIz9H.png)

+ 过程解释
模板通过template: 传给vue的时候，vue会做个保存，保存在vm.options
parse——解析
ast——抽象语法树（abstract syntax tree）
compile——编译
render函数
virtual dom —— 虚拟dom
UI上面的是真实dom，最终会把虚拟dom渲染成真实dom
+ 区别
**runtime-compiler：**
template->ast->render->vdom->UI
**runtime-only：**
render->vdom->UI
+ 下面的文件更轻，打包更小，以后项目都选runtime-only

### render函数是什么

1. render函数的用法
+ 普通用法，给createElement函数传入元素名、属性、内容
+ 给createElement函数传入组件

2. render(h)=>{return h(APP)} 这个h只是个函数名代号
其实是createElement这个函数
![VZrziV.png](https://i.328888.xyz/2023/05/14/VZrziV.png)

![VZrh0z.png](https://i.328888.xyz/2023/05/14/VZrh0z.png)
![VZrSJa.png](https://i.328888.xyz/2023/05/14/VZrSJa.png)
![VZr95L.png](https://i.328888.xyz/2023/05/14/VZr95L.png)

### npm run dev 和 build 底层图
![VZrLbU.png](https://i.328888.xyz/2023/05/14/VZrLbU.png)
![VZrMzv.png](https://i.328888.xyz/2023/05/14/VZrMzv.png)


### 修改webpack配置: 起别名(参照其他讲过的)

![VZraCy.png](https://i.328888.xyz/2023/05/14/VZraCy.png)

### 认识 Vue CLI3

![VZ3fbE.png](https://i.328888.xyz/2023/05/14/VZ3fbE.png)
![VZRGpw.png](https://i.328888.xyz/2023/05/14/VZRGpw.png)
![VZRodL.png](https://i.328888.xyz/2023/05/14/VZRodL.png)
![VZRgdN.png](https://i.328888.xyz/2023/05/14/VZRgdN.png)
```
$mount('#app') 和 el:'#app' 方式都是一样的 在源码做了一层判断，如果没有传el就会自己执行 $mount('#app')，最终都是把#app的元素替换成传入的元素
```

+ 如何找到vue的配置文件
    1. vue ui 会启动一个可视化本地服务，里面可以修改配置
    2. 去modules文件里找
    3. 添加vue.config.js文件，到时候会和vue的module里面的配置进行合并
    ![VZRsup.png](https://i.328888.xyz/2023/05/14/VZRsup.png)
    ![VZcA9J.png](https://i.328888.xyz/2023/05/14/VZcA9J.png)


### 扩展

1. -g 全局安装 global
2. yarn的出现是因为早期npm不好用，想要取代它出现的，但是随着npm的升级，npm也没那么难用
3. 全局的gitconfig里面配置了个人信息
4. 以前js想要运行需要搞个index.html然后跑在浏览器上
现在出现了node，不用浏览器就可以执行js，node是c++开发的，核心是v8引擎
5. chrome比火狐、ie运行代码都快是因为chrome用了v8引擎
6. 原来：js->字节码->浏览器
现在：js->二进制代码（直接机器可读语言）
v8引擎可以直接把js代码翻译成二进制代码
效率很高
v8引擎用c++写的
7. node就是服务端执行js代码的底层支撑，执行一个文件直接`node 文件名`
8. rm 是remove缩写 删除 
删除之前打包的文件夹配置用到
9. 安装脚手架失败，npm缓存清除的方法——把npm-cache这个文件删掉再安装
![iuImdv.png](https://i.328888.xyz/2023/05/12/iuImdv.png)
10. eslint如何对代码进行检测
+ 不一定是你们公司的规范，不同规范的写法也不一样，要花一段时间去适应
+ 选择了eslint但是不想用怎么关掉
![iuIXHy.png](https://i.328888.xyz/2023/05/12/iuIXHy.png)
把这个设置成false，重新编译项目，就可以了
11. preset 配置
12. manually select features 手动的选择特性
13. rc —— run command 运行终端 
14. vcs —— 版本控制系统


> ### 内容回顾
> 1. 什么是cli
> + 脚手架是什么东西
> + cli依赖webpack,node,npm
> + 安装cli3->拉取cli2模块
> 2. cli2初始化项目的过程
> 3. cli2生产的目录结构解析