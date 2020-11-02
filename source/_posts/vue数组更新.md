---
title: vue数组更新
date: 2020-11-01 23:14
tags:
- vue
- 前端
---

今天试了一下在vue中使用array[index] = xxx的方式来修改数组数值，但是发现界面没有什么变化，于是在官方文档查了一下，对于以上的做法可以采用Vue.set(vm.items, indexOfItem, newValue)来代替。

vue可以监听到的数组变更方法包括：
+ push()
+ pop()
+ shift()
+ unshift()
+ splice()
+ sort()
+ reverse()