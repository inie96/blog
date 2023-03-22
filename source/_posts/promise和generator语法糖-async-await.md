---
title: promise和generator语法糖-async await
date: 2022-08-13 21:41:21
cover: /image/tangguo.webp
thumbnail: /image/tangguo.webp
tags:
   - ES6
   - async
   - await
categories:
   - 笔记
---
有了 async-await、promise 还有必要学习吗?
<!--more-->
async-await是promise和generator的语法糖。只是为了让我们书写代码时更加流畅，当然也增强了代码的可读性。
简单来说：async-await 是建立在 promise机制之上的，并不能取代其地位。
## async
~~~
async function timeout() {
   return 'hello world'
} 
timeout(); //为什么没有执行'hello world'
~~~
~~~
async function timeout() {
   return 'hello world'
}
console.log(timeout());   //Promise {<resolved>: "hello world"}
~~~
async 函数返回的是一个promise 对象，如果要获取到promise 返回值，应该用then 方法
~~~
async function fn(){
   return 100;
}
console.log(fn()); //Promise {<resolved>: 100}
let f = fn();
f.then(function(d){
   console.log(d)   //100
})
~~~
## await
await操作符用于等待一个Promise对象，它只能在异步函数async function内部使用。
返回值：
返回promise对象的处理结果，如果等待的不是promise对象，则返回该值本身
如果一个promise被传递给一个await操作符，await将等待promise正常处理完成并返回其处理结果
~~~
function f2(){
   console.log(4)
}
async function f(){
   await f2();     
   console.log(2)   
}
f();
console.log(3);
// 4 3 2
~~~
正常情况下，await命令后面是一个promise对象，它也可以是其它值，如字符串，布尔值，数值以及普通函数。
~~~
console.log(2)
async function fn(){
   console.log(3)
   await 100;  
   console.log(1)
}
fn()
console.log(4)
// 2 3 4 1
~~~
await命令后面是一个promise对象
~~~
function p(){
   return new Promise(resolve=>{
       resolve();
       console.log(1)
   });
};
async function fn(){
   console.log(2)
   await p();  
   console.log(3)
}
fn()
// 2 1 3
~~~
