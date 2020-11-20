---
title: js二维数组
date: 2020-11-18 20:38
tags:
- javascript
---

最近在写算法题的时候，需要用到二维数组，但是javascript不同于我学过的java和C语言，没有现成的办法直接定义一个二位数组，所以就想到了通过循环生成一维数组的方式来生成二维数组。

第一种方法：
```
let arr = new Array(4);
for (let i = 0; i < arr.length; i++) {
    arr[i] = new Array(4);
}
这里在生成每一个小的一维数组的时候也可以使用fill进行初始化。

生成二维数组:
[
  [ <4 empty items> ],
  [ <4 empty items> ],
  [ <4 empty items> ],
  [ <4 empty items> ]
]
```

第二种方法：
```
let arr = new Array(4).fill(0).map(item => new Array(4));  
这里在生成每一个小的一维数组的时候也可以使用fill进行初始化。

生成二维数组：
[
  [ <4 empty items> ],
  [ <4 empty items> ],
  [ <4 empty items> ],
  [ <4 empty items> ]
]
```

踩坑：
1. 使用for...of 来生成二维数组：
```
let arr = new Array(4);
for (let a of arr) {
    a = new Array(4).fill(0);
}

生成数组如下：
[ <4 empty items> ]
```
也就是说for...of没办法生成二维数组。

2. 使用没有初始化的map方法
```
let arr = new Array(4).map(item => new Array(4));  

生成数组如下：
[ <4 empty items> ]
```
所以map方法如果没有先对大的一维数组进行初始化的话，是没办法生成二维数组的。
于是，我又做了如下的两个实验：
针对第一个坑的实验：
```
let arr = [undefined, undefined, undefined, undefined];
for (let a of arr) {
    a = new Array(4);
}

生成结果如下：
[ undefined, undefined, undefined, undefined ]
```
**第一个实验结果来看，for...of循环**  (待补充)  
针对第二个坑实验：
```
let dp1 = [undefined, undefined];
let dp2 = new Array(2);
let dp3 = [, ,];
let arr1 = dp1.map(item => 1);
let arr2 = dp2.map(item => 1);
let arr3 = dp3.map(item => 1);

结果arr1和arr2的输出结果分别如下：
[ 1, 1 ]   //arr1
[ <2 empty items> ] //arr2
[ <2 empty items> ] //arr3
```
**从第二个实验的结果可以看出来，new Array是相当于使用数组字面量方法定义了空位元素。**
而对于数组中的空位，ECMScript文档中是这样说明，数组的空位会反映在length属性。但是这个位置的值是未定义的，即不存在。如果进行读取，则读取到的值就是undefined。而map方法遍历成员时，如果发现元素是空位就会直接跳过，不会进入回调函数。  
  

**总结就是： 要生成二维数组的时候，使用new Array和map方法，应该先对生成的大的一维数组先进行初始化，防止map方法直接跳过了所有元素。**




