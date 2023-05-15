---
title: promise
date: 2023-05-15 20:39:30
tags:
   - promise
   - ES6
categories:
   - 笔记
---
<!--more-->

### 01-promise的使用
#### 1.1-promise的基本使用

+ promise是一种优雅的方式解决回调地狱问题

+ 优雅在链式编程

```
1.给Promise传入一个函数
2.resolve、reject分别又是两个函数
3. then传入一个函数
4. catch传入一个函数

new Promise((resolve,reject)=>{
    //函数体里面写入异步请求
    //用settimeout模拟异步请求
    setTimeout(()=>{
        resolve()
    },1000)
}).then(()=>{
    console.log(1)
    ...//很多代码
    return new Promise((resolve,reject)=>{
        setTimeout(()=>{
            resolve()
        },2000)
    })
}).then(()=>{
    console.log(2)
    ...
    return new Promise((resolve,reject)=>{
        setTimeout(()=>{
            resolve()
        },3000)
    })
}).then(()=>{
    console.log(3)
    ...
    return new Promise((resolve,reject)=>{
        setTimeout(()=>{
            resolve()
        },4000)
    })
}).then(()=>{
    console.log(4)
    ...
})
```

![测试结果1](https://i.328888.xyz/2023/05/15/VZuVQ5.png)
![测试结果2](https://i.328888.xyz/2023/05/15/VZuUnH.png)

+ resolve的数据就是then中res携带的结果的数据

+ 什么时候会用promise?
    一般在异步请求操作的时候，使用promise对这个异步操作进行封装，就是把异步请求扔到promise函数体里面去

+ promise原理
    new一个promise -> 构造函数（1.保存了状态信息，2.立即执行传入的函数）-> 在执行传入的回调函数时，会传入2个参数，resolve,reject,这俩本身又是函数

+ 优雅在对异步请求的代码和返回结果处理代码做了分离

+ 优雅在对调用成功、失败结果处理做了分离

```
new Promise((resolve,reject)=>{
    resolve('成功')
    reject('失败')
}).then(res=>{
    console.log(res)
}).catch(err=>{
    console.log(err)
})
```
![测试结果](https://i.328888.xyz/2023/05/15/VZu9sQ.png)

+ promise的三种状态和图解
![ViZWWx.png](https://i.328888.xyz/2023/05/15/ViZWWx.png)

#### 1.2-promise的另外处理形式

```
new Promise((resolve,reject)=>{
    setTimeout(()=>{
        resolve('成功')
        //reject('失败')
    },1000)
}).then(res=>{
    console.log(res)
  },err=>{
    console.log(err)
  })
```
![测试结果](https://i.328888.xyz/2023/05/15/ViZQZv.png)

#### 1.3-promise的链式调用

![ViZua5.png](https://i.328888.xyz/2023/05/15/ViZua5.png)

+ promise的链式简化

+ 需求
    aaa——第一次回调结果
    aaa111——第二次回调结果
    aaa111222——第三次回调结果

常规写法1

```
new Promise(resolve=>{
    setTimeout(()=>{
        resolve('aaa')
    },1000)
}).then(res=>{
    console.log(res,'第一次处理了10行代码')
    return new Promise(resolve=>{
        resolve(res+'111')
    })
}).then(res=>{
    console.log(res,'第二次处理了10行代码')
    return new Promise(resolve=>{
        resolve(res+'222')
    })
}).then(res=>{
    console.log(res,'第三次处理了10行代码')
})
```
![ViivVE.png](https://i.328888.xyz/2023/05/15/ViivVE.png)

简化写法2

```
new Promise(resolve=>{
    setTimeout(()=>{
        resolve('aaa')
    },1000)
}).then(res=>{
    console.log(res,'第一次处理了10行代码')
    return Promise.resolve(res+'111')
}).then(res=>{
    console.log(res,'第二次处理了10行代码')
    return Promise.resolve(res+'222')
    // return Promise.reject('error') //异常的调用
    // throw 'error'
}).then(res=>{
    console.log(res,'第三次处理了10行代码')
}).catch(err=>{
    console.log(err)
})
```
![ViiSRH.png](https://i.328888.xyz/2023/05/15/ViiSRH.png)


简化写法3

```
new Promise(resolve=>{
    setTimeout(()=>{
        resolve('aaa')
    },1000)
}).then(res=>{
    console.log(res,'第一次处理了10行代码')
    return res+'111'
}).then(res=>{
    console.log(res,'第二次处理了10行代码')
    return res+'222'
}).then(res=>{
    console.log(res,'第三次处理了10行代码')
})
```

![Vii5UF.png](https://i.328888.xyz/2023/05/15/Vii5UF.png)