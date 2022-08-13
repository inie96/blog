---
title: 异步编程解决方案-Promise
date: 2022-08-13 21:05:24
tags: 
   - ES6
   - Promise
categories:
   - 笔记
---
一篇搞定Promise~
<!--more-->
## 定义
Promise 是异步编程的一种解决方案，比传统的解决方案——回调函数和事件——更合理和更强大。
所谓 Promise ，简单说就是一个容器，里面保存着某个未来才会结束的事件（通常是一个异步操作）的结果。
从语法上说，Promise 是一个对象，从它可以获取异步操作的消息。Promise 提供统一的 API，各种异步操作都可以用同样的方法进行处理。
解决 JS中多个异步回调难以维护和控制的问题
#### Promise 对象有以下两个特点
* 对象的状态不受外界影响。 Promise 对象代表一个异步操作，有三种状态： pending （进行
中）、 fulfilled （已成功）和 rejected （已失败）。只有异步操作的结果，可以决定当前是哪一种状态，任何其他操作都无法改变这个状态。这也是 Promise 这个名字的由来，它的英语意思就是“承 诺”，表示其他手段无法改变。
* 一旦状态改变，就不会再变，任何时候都可以得到这个结果。 Promise 对象的状态改变，只有两种可能：从 pending 变为 fulfilled 和从 pending 变为 rejected 。只要这两种情况发生，状态就凝固了，不会再变了，会一直保持这个结果，这时就称为 resolved（已定型）。如果改变已经发生了，你再对 Promise 对象添加回调函数，也会立即得到这个结果。这与事件（Event）完全不同，事件的特点是，如果你错过了它，再去监听，是得不到结果的。
## 基本用法
Promise 对象是一个构造函数，用来生成 Promise 实例。
~~~
var p = new Promise(function(resolve,reject){
       if(true){ //请求成功
           resolve('ok')
       }else {
           reject('error')
       }
});
p.then(function(res){
       console.log(res)
},function(res){
       console.log(res)
})
~~~
#### 解释
Promise 构造函数接受一个函数作为参数，该函数的两个参数分别是 resolve 和 reject 。它们是两个函数，由 JavaScript 引擎提供，不用自己部署。
resolve 函数的作用是，将 Promise 对象的状态从“未完成”变为“成功”（即从 pending 变为resolved），在异步操作成功时调用，并将异步操作的结果，作为参数传递出去； reject 函数的作用是，将 Promise 对象的状态从“未完成”变为“失败”（即从 pending 变为 rejected），在异步操作失败时调用，并将异步操作报出的错误，作为参数传递出去。
Promise 实例生成以后，可以用 then 方法分别指定 resolved 状态和 rejected 状态的回调函数。
then 方法可以接受两个回调函数作为参数。第一个回调函数是 Promise 对象的状态变为 resolved 时调用，第二个回调函数是 Promise 对象的状态变为 rejected 时调用。其中，第二个函数是可选的，不一定要提供。这两个函数都接受 Promise 对象传出的值作为参数。
#### 解决回调陷阱
~~~
let p = new Promise(function(resolve, reject){
   if (true){
       resolve("成功");
     } else {
       reject("失败");
     }
})
p.then(function(v){
   return new Promise(function(resolve, reject){
        if (true){
           resolve("成功");
        } else {
           reject("失败");
        }
   })
}, function(v){
   console.log(v)
}).then(function(){
   console.log(4)
}, function(){
   console.log(5)
})
~~~
## Promise.all()
Promise.all() 方法用于将多个 Promise 实例，包装成一个新的Promise 实例。
~~~
const p = Promise.all([p1, p2, p3]);
~~~
Promise.all() 方法接受一个数组作为参数， p1 、 p2 、 p3 都是 Promise 实例，如果不是，就会先调用下面讲到的 Promise.resolve 方法，将参数转为 Promise 实例，再进一步处理。另外，Promise.all() 方法的参数可以不是数组，但必须具有 Iterator 接口，且返回的每个成员都是Promise 实例。
p 的状态由 p1 、 p2 、 p3 决定，分成两种情况。
1. 只有 p1 、 p2 、 p3 的状态都变成 fulfilled ， p 的状态才会变成 fulfilled ，此时 p1 、 p2 、p3 的返回值组成一个数组，传递给 p 的回调函数。
2. 只要 p1 、 p2 、 p3 之中有一个被 rejected ， p 的状态就变成 rejected ，此时第一个被 reject的实例的返回值，会传递给 p 的回调函数。

实例：
~~~
var p1 = new Promise((resolve,reject)=>{
    setTimeout(()=>{
        resolve('1111')
    },1000)
});
var p2 = new Promise((resolve,reject)=>{
    setTimeout(()=>{
        resolve('22222')
    },4000)
});
 
Promise.all([p1,p2])
.then(([d1,d2])=>{  
    console.log(d1,d2);
},err=>{
});
~~~
## Promise.race()
~~~
const p = Promise.race([p1, p2, p3]);
~~~
只要 p1 、 p2 、 p3 之中有一个实例率先改变状态， p 的状态就跟着改变。那个率先改变的 Promise 实例的返回值，就传递给 p 的回调函数。
Promise.race() 方法的参数与 Promise.all() 方法一样，如果不是 Promise 实例，就会先调用下面讲到的 Promise.resolve() 方法，将参数转为 Promise 实例，再进一步处理。
~~~
var p1 = new Promise((resolve,reject)=>{
    setTimeout(()=>{
        resolve('1111')
    },1000)
});
var p2 = new Promise((resolve,reject)=>{
    setTimeout(()=>{
        resolve('22222')
    },4000)
});
Promise.race([p1,p2])
.then(d =>{  
    console.log(d);
},err=>{
});
~~~
