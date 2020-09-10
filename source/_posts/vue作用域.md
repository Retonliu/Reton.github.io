---
title: vue作用域
date: 2020-8-27 14:16:00
tags: 
- vue
- 前端
---
>前置知识：new一个vue的时候，把new的时候挂载的el看作是一个根组件，所以new的时候传进去的数据看作是根组件的选项

组件里，模板可以访问到的变量是当前组件data中所定义的propetry。**而在父组件的模板里面的子组件，可以访问到的数据就是父组件的prepetry,因为此时子组件相当于父组件的模板的一部分，如果子组件里面的模板想要引用父组件的propetry,则需要在子组件里声明props。**props中声明得到的变量就可以当作子组件自身data里面的proprtry使用。同时在父组件的模板里面需要绑定props所需要的数据。绑定分为静态绑定和动态绑定两种方法。
+ 静态绑定:
&lt;blog-component title="vue作用域"&gt;&lt;/button-component&gt;
静态绑定不需要使用v-bind，直接声明即可。注意声明的内容不可以是变量。
+ 动态绑定:
&lt;blog-component :title="post.title"&gt;&lt;/button-component&gt;
post是blog-component所在域的父组件的propetry。

>注意，**组件访问的数据应该是其所在模板的父组件。**如果一个组件不是当前模板的根，即使在该组件中声明了插槽，放入插槽的子组件也无法访问该组件的内容。

例如声明了一个子组件:
```
Vue.component('son-component', {
    props: ['msg'],
    template: 
            `
            <span>{{ msg }}</span>
            `
})
```
以及一个父组件:
```
Vue.component('father-component', {
    data: function(){
        return {
            msg: "父组件"
        }
    },
    template: `
            <div>
                <slot></slot>
            </div>
        `
})
```
最后声明根组件:
```
var app = new Vue({ el: '#wrap',  //new的时候的data才是父级组件的
    data: function() {
        return {
            
        }
    } 
});
```
在html中声明如下:
```
<div id="wrap">
            <father-component>
                <son-component :msg="msg"></son-component>
            </father-component>
        </div>
```
此时son-component是无法访问到msg的，会出现msg is not defined的报错。而如果在根组件的data中声明
    msg: "根组件"
则可以在界面中看到msg变为根组件字符串。**所以除非把son-component放在father-component的模板当中，不然son-component是没办法访问到father-component的msg变量的。**虽然在代码中看起来father-component好像是son-component的父组件，但是此时son-component需要拿的数据应该来自所处模板的根组件（app）。**除了data之外，methods等其他选项也是同理。**