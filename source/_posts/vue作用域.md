---
title: vue作用域
date: 2020-8-27 14:16:00
tags: vue
---
>前置知识：new一个vue的时候，把new的时候挂载的el看作是一个根组件，所以new的时候传进去的数据看作是根组件的选项

组件里，模板可以访问到的变量是当前组件data中所定义的propetry。**而在父组件的模板里面的子组件，可以访问到的数据就是父组件的prepetry,因为此时子组件相当于父组件的模板的一部分，如果子组件里面的模板想要引用父组件的propetry,则需要在子组件里声明props。**props中声明得到的变量就可以当作子组件自身data里面的proprtry使用。同时在父组件的模板里面需要绑定props所需要的数据。绑定分为静态绑定和动态绑定两种方法。
+ 静态绑定:
&lt;blog-component title="vue作用域"&gt;&lt;/button-component&gt;
静态绑定不需要使用v-bind，直接声明即可。
+ 动态绑定:
&lt;blog-component :title="post.title"&gt;&lt;/button-component&gt;
post是blog-component所在域的父组件的propetry。

