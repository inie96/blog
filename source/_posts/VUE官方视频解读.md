---
title: VUE官方视频解读
date: 2023-03-24 22:40:07
tags:
    - VUE
categories:
    - 笔记
---
详见下文
<!--more-->

### VUE核心概念

#### 渐进式js框架

由浅入深 由简单到复杂

#### 优点

```
体积小

运行效率快
虚拟DOM 一种预先通过js计算 把最终的DOM操作计算出来并优化的技术
由于这个DOM的操作是预处理 并没有真实的操作DOM 所以叫虚拟DOM

双向数据绑定

生态丰富 新手友好

```

#### 展示数据

步骤
```
引入vue库
创建vue实例
通过应用ID嵌入到我们的根元素（el）中
将数据放入一个叫data的对象中
用双括号表达式展示数据
```

魔力：
数据变更时vue自动更新html
vue是响应式的reactive
数据改变时 vue会帮你更新所有页面上用到它的地方
除了字符串，其他数据类型也是如此

#### v-for指令

展示列表
从实际API获取信息
fetch

#### computed计算属性

reduce求和

#### chrome的vue插件

查看页面中的数量

#### v-model指令

input框增加v-model指令和数量做绑定
快速变更数据

#### 初始化vue工程

```
vue init webpack my-project

build
config
node_modules
src
static
test
```

#### vue单文件组件

```
.vue

HTML
JS
CSS/SCSS
```

