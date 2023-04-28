---
title: Vuex笔记
date: 2023-04-10 20:23:55
tags:
    - Vue
    - Vuex
categories:
    - 笔记
---
详见下文
<!--more-->


vuex就相当于前端的数据库，只不过是存储在内存中的
> 官方描述：
Vuex 是一个专为 Vue.js 应用程序开发的状态管理模式 + 库。它采用集中式存储管理应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化。


### 基本使用

1. 安装

`npm install vuex --save`

2. main.js引入vuex
```
import Vuex from 'vuex'
Vue.use(Vuex)
```

###### 以保存登录用户名的实例讲解

3. store/index.js文件

```
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

// 公共对象，存储所有组件用到的状态

const state = {
    user:{
        name:''
    }
}

// 唯一取值方法，计算属性

const getters = {
    getUser(state){ //把上面的传入进来
        return state.user //返回状态中的对象值
    }
}

// 唯一可以修改state值的方法,同步阻塞
// 用commit调mutations中的方法

const mutations={
    updateUser(state,user){
        state.user = user // 把获取到的外部参数存储到状态中
    }
}

// 异步调用mutations方法
// 用dispatch调action中的方法

const actions={
    asyncUpdateUser(context,user){//context是上下文，就是当前这个文件的对象
        context.commit('updateUser',user)
    }
}

// 暴露出去
export default new Vuex.Store({
    state,
    getters,
    mutations,
    actions,
})
```

4. 在main.js中引入刚刚定义好的

```
import store from './store'
```

5. 在main.js中导出store

```
new Vue({
    el:'#app',
    router,
    store,
    render:h=>h(App)
})
```

6. 在登录页存储 user.name

```
this.$store.dispath('asyncUpdateUser',{name:this.form.name})
```

7. 在展示页获取 user.name

```
this.$store.getters.getUser.name
```
### 解决浏览器刷新后Vuex数据消失问题

1. 思路

存：
监听页面是否刷新
刷新了 把state对象存到ls

取：
打开一个页面 判断ls中是否有state
如果有 表示页面刷新过 获取ls中的state
如果没有 表示第一次进入页面 取vuex中定义的state初始值

2. 实现

修改App.vue文件
```
mounted(){
    window.addEventListener('upload',this.saveState)
}
methods:{
    saveState(){
        Vue.ls.set('state',JSON.stringify(this.$store.state))
    }
}
```
修改store/index.js文件
```
const state = null != Vue.ls.get('state') ?
          JSON.parse(Vue.ls.get('state')) :
          {
              user:{
                  name:''
              }
          }
```

### Vuex模块化

>由于使用单一状态树，应用的所有状态会集中到一个比较大的对象。当应用变得非常复杂时，store 对象就有可能变得相当臃肿。

为了解决以上问题，Vuex 允许我们将 store 分割成模块（module）。每个模块拥有自己的 state、mutation、action、getter、甚至是嵌套子模块——从上至下进行同样方式的分割：
```
const moduleA = {
  state: () => ({ ... }),
  mutations: { ... },
  actions: { ... },
  getters: { ... }
}

const moduleB = {
  state: () => ({ ... }),
  mutations: { ... },
  actions: { ... }
}

const store = new Vuex.Store({
  modules: {
    a: moduleA,
    b: moduleB
  }
})

store.state.a // -> moduleA 的状态
store.state.b // -> moduleB 的状态
```

以上面的用户名实例再次修改

1. 创建store/modules/user.js文件
```
// 公共对象，存储所有组件用到的状态

const user = {
    state: {
        user:{
            name:''
        }
    }

    // 唯一取值方法，计算属性

    getters: {
        getUser(state){ //把上面的传入进来
            return state.user //返回状态中的对象值
        }
    }

    // 唯一可以修改state值的方法,同步阻塞
    // 用commit调mutations中的方法

    mutations: {
        updateUser(state,user){
            state.user = user // 把获取到的外部参数存储到状态中
        }
    }

    // 异步调用mutations方法
    // 用dispatch调action中的方法

    actions: {
        asyncUpdateUser(context,user){//context是上下文，就是当前这个文件的对象
            context.commit('updateUser',user)
        }
    }
    
}

export default user
```
2. 修改 store/index.js文件

```
import Vue from 'vue'
import Vuex from 'vuex'
import user from './modules/user' //导入模块
Vue.use(Vuex)

export default new Vuex.Store({
    modules:{ //导出模块
        user
    }
})
```

3. 存取状态使用的是getters和actions处理，代码不用改变，但是和state相关的要变

4. 修改App.vue

```
methods:{
    saveState(){
        Vue.ls.set('state',JSON.stringify(this.$store.state.user))
    }
}
```