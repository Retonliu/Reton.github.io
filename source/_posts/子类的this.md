---
title: es5和es6子类的this初始化区别
date: 2020-9-6 12:15
tags: 
- es6
- javascript
---
在es5中，在创建子类的时候，会新建子类的实例对象this，然后再把父类的属性添加到实子类上面。
在es6中，会先创建父类的实例对象this，然后再用子类的构造函数加工this。