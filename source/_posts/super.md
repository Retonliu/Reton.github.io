---
title: super关键字
date: 2020-11-10 12:50
tags:
- es6
- javascript
---

super关键字有两种使用方法：
1. 作为函数使用，此时代表父类的构造函数
super作为函数使用的时候，只能用于子类的构造函数当中（注意子类的构造函数第一行一定要出现super(),因为子类的this对象是继承自父类，然后加工过来的），*子类调用super的时候，super的this指向的是子类*。

2. 作为对象使用，此时代表父类的原型对象
注意此时super指向的是父类原型对象，所以定义在父类实例上的方法或者属性是无法访问到的。

例如：
```
class Father {
    constructor() {
        this.a = 1; //父类实例上的属性
    }
}
class Son extends Father{
    outPutA() {
        console.log(super.a);
    }
}
let s = new Son();
s.outPutA(); //undefined

*注意通过子类使用super.foo()调用父类的方法的时候，父类中的foo被调用时，内部的this绑定的是子类*


