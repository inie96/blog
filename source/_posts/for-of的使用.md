---
title: for of的使用
date: 2023-03-23 21:00:24
tags:
    - js
categories:
    - 笔记
---
详见下文
<!--more-->

1. for of 可以代替forEach
2. for( let [i,v] of arr.entries)
加不加中括号的区别？
数组使用解构的写法去写？
看你拿到的数据是什么情况的，判断是不是能够用解构的方式取到键值
如果拿到的数据不行，就要转换一下arr.entries()
3. 对象运用for of
本来不能用 因为对象没有遍历器
要把对象转换一下用Object.entries(obj)
```
var obj = {
id:1,
name:'abc'
};
for (let k in obj) {
console.log(k);
console.log(obj[k]);
}
for (let k of obj) {
console.log(k);
}
// TypeError: es6[Symbol.iterator] is not a function
解决的办法
for (let [k,v] of Object.entries(obj)) {
console.log(k); //获取键
console.log(v); //获取值
}
```
4. 与其他遍历的比较
for：取值不方便
forEach：取值方便，但是不能添加返回，无法中途退出循环
map：有返回值
for in：获取值的时候还要用另一个方式，有一点麻烦
```
for （let i in arr）{
console.log(i); //获取键
console.log(arr[v]); //获取值
}
```
for of 可以直接添加 break continue
