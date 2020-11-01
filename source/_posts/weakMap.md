---
title: weakMap如何解决内存泄漏
date: 2020-10-28 20:07
tags:
- es6
- javascript
- 前端
---

>内存泄漏是指某部分内存被占用，使用完之后却没有正确释放掉，导致后续程序都无法使用这一块内存。

weakMap可以很好的解决内存泄漏的问题。因为weakMap对于存储在其里面的对象是弱引用的，weakMap不会影响到垃圾回收机制的引用计数。所以如果weakMap的**键名**消失之后，键值对会自动被垃圾回收机制消去，所以也就不存在内存泄漏的事情。由于DOM树经常会发生变更，所以weakMap很适合用来存放DOM节点。一旦DOM节点消失，存放在weakMap中的对应引用也就跟着消失，无需手动删除引用来触发垃圾回收机制。如果使用的是普通的map(其他非weak数据结构同理）。例如：
```
const m = new Map();
const node = document.getElementById("header");
m.set(node, 'head');
如果node节点从dom树中被删除的话，那么就需要手动来删除这个引用。
m.delete(node); //删除引用
```
如果没有delte引用，那么会导致内存泄漏。
而weakMap可以省去delete这个步骤，引用会随着dom消失自动删去。