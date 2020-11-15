---
title: js中的两种特殊数据类型：undefined和null
date: 2020-11-15 09:53
tags:
- javascript
---

1. undefined类型只有一个值，就是特殊值undefined。**用于表示未初始化的变量**。当使用var或者let声明一个变量但是没有初始化的时候，就相当于给这个变量赋予了undefined值。
```
let foo; 
相当于 
let foo = undefined;
```
>一般来说不需要显示的给某个变量声明undefined值。  

需要注意的是,*使用typeof操作符的时候，声明但是为初始化的变量会返回undefined，但是**未声明的变量也会返回undefined***。所以最好的实践方法，就是在声明一个变量的同时，最好初始化为一个非undefined的值。这样当使用typeof操作符得到undefined的时候，就可以知道这个变量是没有声明的。
*undefined可以当作假值使用*。

2. null类型也只有一个值，就是特殊值null。**null用于表示一个空对象指针**。  
>当定义了一个要用来保存对象的变量，但是还没有对象可以保存的时候，**应该使用null来显示初始化**。

对null变量使用typeof操作符的时候，会返回object。因为null变量表示的就是一个空对象指针。  
*null可以作为假值使用。*

结论：
* null和undefined的联系：
当使用 双等于号==操作符比较null和undefined的时候会返回true。两者都可以当作假值使用。

* null和undefined的区别：
undefined用于表示未初始化变量(非object变量)，而null用于表示空对象指针。