---
title: vuex
date: 2023-05-17 22:34:08
tags:
    - Vue
    - Vuex
categories:
    - 笔记
---
详见下文
<!--more-->

### 1-介绍vuex

#### 1.1-什么是vuex

+ 因为组件树很庞大，如果多个组件想共用一个变量，这个变量放在哪个组件都不方便取用，需要有一个地方集中进行管理，这就是vuex产生的原因

![VVR4Go.png](https://i.328888.xyz/2023/05/17/VVR4Go.png)

#### 1.2-vuex管理什么状态,用在哪

+ 在多个组件中都用到，共享的状态

![VVRzWP.png](https://i.328888.xyz/2023/05/17/VVRzWP.png)

#### 1.3-单页面的状态管理

+ 定义状态在view上面显示，用户操作显示的内容会有一些actions，这些操作的改变又会改变数据数据——单页面状态管理
![VVRKkb.png](https://i.328888.xyz/2023/05/17/VVRKkb.png)
![VyVKbL.png](https://i.328888.xyz/2023/05/19/VyVKbL.png)

#### 1.4-安装vuex
```
npm install vuex --save
生产环境也需要用
```
+ 在src下创建一个文件夹store
![VyfAlC.png](https://i.328888.xyz/2023/05/19/VyfAlC.png)
+ import vuex
+ Vue.use(vuex)
+ 创建对象new Vuex.store
  + 对象中放state、mutations、actions、getters、modules 
+ 导出store对象
+ 在main.js中引用这个文件，挂载这个对象

![VyAtn3.png](https://i.328888.xyz/2023/05/19/VyAtn3.png)


#### 1.5-多界面状态管理

![VyfhYQ.png](https://i.328888.xyz/2023/05/19/VyfhYQ.png)
![VyyAdk.png](https://i.328888.xyz/2023/05/19/VyyAdk.png)
+ 在组件中引用vuex中的state,但是修改这个状态不应该直接去改变state
修改1：如果没有异步 可以用mutation
修改2：如果有异步 要先actions 再mutations
devTools这个插件可以跟踪 mutation中状态的变化，如果修改错了可以及时发现 
actons中可以和后端进行异步请求

#### 1.6-安装mutations插件，如何跟踪mutations变化

![Vy4w0d.png](https://i.328888.xyz/2023/05/19/Vy4w0d.png)
![Vy40zN.png](https://i.328888.xyz/2023/05/19/Vy40zN.png)
修改mutation要调用commit提交这个方法
![Vy4rbk.png](https://i.328888.xyz/2023/05/19/Vy4rbk.png)
![Vy4TlV.png](https://i.328888.xyz/2023/05/19/Vy4TlV.png)
![VyAiVa.png](https://i.328888.xyz/2023/05/19/VyAiVa.png)
![VyAl8Z.png](https://i.328888.xyz/2023/05/19/VyAl8Z.png)

#### 小结-vuex最基本使用
1. 在state中定义一个状态count
2. 在页面中使用this.$store.state.count
3. 在mutations中定义改变状态的方法
4. 在页面中使用this.$store.commit('changeCount')去改变状态

#### vuex5大核心概念

1. status
2. getters
3. mutations
4. actions
5. modules


#### 2.1-单一状态树

+ 在一个项目里面只创建一个store去管理状态，不要建多个，不方便维护，也叫单一数据源
#### 2.2-getters的基本使用

+ getters就相当于计算属性
+ 什么时候使用计算属性？有一个值你不要直接展示，需要进行一些操作后展示出来就需要计算属性
```
state:{
  count:1,
}

getters:{
  powerCount(state) {
    return state.count*2
  }
  powerCountLength(state,getters) {//还可以拿到其他getters
    return getters.powerCount.length
  }
  //如果getters想传入参数，可以这样写返回一个函数
  moreAgeStu(state){
    return function(age){
      return state.students.filter(s => s.age > age)
    }
  }
  //箭头函数的写法
  moreAgeStu(state){
    return age => {
     return state.students.filter(s => s.age > age)
    }
  }
  //调用时
  this.$store.getters.moreAgeStu(8)

}

$store.getters.addroutes
```

#### mutations状态更新

1. mutation基本使用

+ vuex的store状态的更新唯一方式：提交mutation 
+ mutation包括两部分：字符串的事件类型、一个回调函数（回调函数第一个参数就是state）

mutation定义方式
```
mutations:{
  increment(state){
    state.count++
  }
}
```

通过mutation更新
```
this.$store.commit('increment')
```

案例1：根据传参增加相应个数
commit时想传入参数
```
mutations:{
  incrementCount(state,count){
    state.count += count
  }
}

this.$store.commit('incrementCount', count)
//参数是payload负载
// 参数可以是一个对象 
```

2. mutation提交风格


案例2：mutation特殊提交风格
```
this.$store.commit({
  type:'incrementCount',
  count,
})

// 传参会有变化
mutations:{
  incrementCount(state,payload){
    state.count += payload.count
  }
}
```

3. mutation响应规则


 
### 补充
1. 使用插件的步骤
   + 引入插件文件
   + 安装插件Vue.use(插件)(底层会执行这个插件的install方法 )
   + 创建对象
2. 不要在main.js文件引用很多插件，代码不好管理，不规范，可以在其他文件写好了再引入main.js
3. store 仓库的意思 
