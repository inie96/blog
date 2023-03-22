---
title: markdown语法
date: 2022-09-08 19:46:17
cover: /image/markdown.webp
thumbnail: /image/markdown.webp
tags:
   - markdown
categories:
   - 笔记
---
10个你需要了解的md语法
<!--more-->
## 1、标题

> 语法：
```
# + 文字
（最多到6级标题）

# 标题1 #
## 标题2 ##
### 标题3 ###
#### 标题4 ####
##### 标题5 #####
###### 标题6 #######
```

> <span style="color:red">效果</span>

# 标题1 #
## 标题2 ##
### 标题3 ###
#### 标题4 ####
##### 标题5 #####
###### 标题6 #######

## 2、列表
* ### 无序列表

> 语法：
```
+ a
+ b
+ c

- d
- e
- f

* g
* h
* i
```
> <span style="color:red">效果</span>
+ a
+ b
+ c

- d
- e
- f

* g
* h
* i
* ### 有序列表

> 语法：
```
有序列表
1. abc
2. abc
3. dada

错序列表
2. awfa
5. awef
25. dfaf
```
> <span style="color:red">效果</span>

有序列表

1. abc
2. abc
3. dada

错序列表

2. awfa
5. awef
25. dfaf

* ### 嵌套列表

> 语法：
```
无序
+ a
  + a1
  + a2
+ ba
+ c

有序
1. a
   1. adac
      1. adaw
   2. adfsda
2. ad
3. sad
```
> <span style="color:red">效果</span>

无序

+ a
  + a1
  + a2
+ ba
+ c

有序

1. a
   1. adac
      1. adaw
   2. adfsda
2. ad
3. sad

## 3、引用块

> 语法：
```
引用
> 引用1
引用1 引用1

嵌套引用
> 嵌套引用1
>> 嵌套引用1
```
> <span style="color:red">效果</span>

引用
> 引用1
引用1 引用1

嵌套引用
> 嵌套引用1
>> 嵌套引用1

## 4、代码块

> 语法：
```

代码块
// code`code`code

多行代码块儿
// ```
// code
// code
// code
// ```

```
> <span style="color:red">效果</span>

代码块
code`code`code

多行代码块儿

```
code
code
code
```

## 5、链接

> 语法：
```
链接
[百度1](www.baidu.com)
```
> <span style="color:red">效果</span>

链接
[百度1](www.baidu.com)

## 6、图片

> 语法：
```
![图片](https://note.youdao.com/favicon.ico)
```
> <span style="color:red">效果</span>

![图片](https://note.youdao.com/favicon.ico)

## 7、分割线

> 语法：
```
分割线

---
- - -
-------
*****
* * *
____
```
> <span style="color:red">效果</span>

分割线

---
- - -
-------
*****
* * *
____


## 8、表格

> 语法：
```
表格1
|123|234|345|
|:-|:-:|-:|
|abc|bcd|cde|
|abc|bcd|cde|
|abc|bcd|cde|
|abc|bcd|cde|
|abc|bcd|cde|
表格2
|123|234|345|
|:---|:---:|---:|
|abc|bcd|cde|
|abc|bcd|cde|
|abc|bcd|cde|
表格3
123|234|345
:-|:-:|-:
abc|bcd|cde
abc|bcd|cde
abc|bcd|cde
```
> <span style="color:red">效果</span>

表格1
|123|234|345|
|:-|:-:|-:|
|abc|bcd|cde|
|abc|bcd|cde|
|abc|bcd|cde|
|abc|bcd|cde|
|abc|bcd|cde|
表格2
|123|234|345|
|:---|:---:|---:|
|abc|bcd|cde|
|abc|bcd|cde|
|abc|bcd|cde|
表格3
123|234|345
:-|:-:|-:
abc|bcd|cde
abc|bcd|cde
abc|bcd|cde

## 9、复选框

> 语法：
```
- [ ] 复选框
- [x] 选中状态
```
> <span style="color:red">效果</span>

- [ ] 复选框
- [x] 选中状态

## 10、其他

> 语法：
```
斜体
*md*

粗体
**md**

斜体
_md_

斜体
__md__

转义
\+

删除线
~~删除~~
```
> <span style="color:red">效果</span>

斜体
*md*

粗体
**md**

斜体
_md_

粗体
__md__

转义
\+

删除线
~~删除~~