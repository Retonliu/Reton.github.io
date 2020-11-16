---
title: js中的特殊值：undefined和null、NaN
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

3. NaN
NaN属于Number类型，NaN表示这个不是数值（Not a Number），用于表示本来要返回数值的操作失败了。**任何设计NaN的操作始终返回NaN，
NaN特殊的地方在于 NaN == NaN 返回false,所以要判断一个数是不是NaN可以使用isNaN函数来判断，isNaN会尝试把参数转为数值，如果这个参数不能转为数值，则isNaN返回true（因为转换不了为数值就转换为NaN）。
ECM规定任何关系操作符跟NaN比较都会返回false。所以就会出现以下的情况：

NaN < 1  //false
NaN >= 1 //false

结论：
* null和undefined的联系：
当使用 双等于号==操作符比较null和undefined的时候会返回true。两者都可以当作假值使用。

* null和undefined的区别：
undefined用于表示未初始化变量(非object变量)，而null用于表示空对象指针。

