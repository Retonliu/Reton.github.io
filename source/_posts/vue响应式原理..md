---
title: vue2响应式原理
date: 2020-12-01 22:26
tags:
- vue
---
**每一个data有一个dep**
dep类是被观察者类
dep种的subs就是它的观察者列表。
target用于表示正在进行注册的观察者（当前时间内一次只能有一个被观察者被评估）

当data被get的时候就会注册观察者

每一个组件都会注册一个观察者类，使自己变为观察者的身份。
注册watcher之后，会调用组件的getter方法，这个方法最后就是调用render方法，而render方法会去访问data里面的属性。而被render方法get到的属性，就会把这个watcher注册到自己的观察者列表当中（依赖收集）。