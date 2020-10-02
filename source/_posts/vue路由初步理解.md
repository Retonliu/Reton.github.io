---
title: vue路由初步理解
date: 2020-9-6 12:15
tags: 
- vue
- 前端
---
>前置知识:
![](spa.png)理解单页应用和多页应用的区别。单页应用有一个主页和多个模块组成，在初次加载的时候将全部资源加载完毕。而多页应用则每点击一次链接跳转到别的页面都需要重新加载资源。其中单页应用的核心就是前端路由。通过把各个页面当成模块，然后通过在主页中布置路由即可实现快速的跳转。

# Vue Router
vue Router 做的事情就是把各个组件映射到路由中，通过```<router-link to="/"></router-link>和<router-view></router-view>```配合把被映射的组件渲染到指定位置。其中```<router-link></router-link>```组件用于导航的作用来指定当前的组件链接到to指定的地方，```<router-view></router-view>```就是将```<router-link></router-link>```中to指定的东西渲染出来。

创建一个路由的过程有如下步骤:
1. **定义路由组件。** 从文件中import 进来其他的组件或者在当前页面中const 定义组件模板

2. **定义路由。** 通过在routes数组中用如下语法
```
const routers = [
    { path: '/index', component: Index },
    { path: '/login', component: Login}
]

```
数组中每一个对象就是一个路由，其中的path就是路由路径，比如要导向Index页面的话，在router-link组件中把to属性设置为'/index'，就可以导向这个路由。
3. **创建 router 实例**， 然后把定义的路由传到实例里面
```
const router = new VueRouter({
    routes
})
```

4. **创建和挂载跟实例。** 
```
const app = new Vue({
    router
}).$mount('#app')
```
# 嵌套路由
在定义路由的时候，在路由对象中添加一个children配置。如下：
```
const routers = [
    { 
        path: '/index', 
        component: Index,
        children: [
            {
                path: 'focus',    //路径会被设置为/index/focus,不用手动去写
                component: Focus
            }
        ]
    },
    {   
        path: '/login', 
        component: Login
    }
]

```
*注意使用了children的路由的组件模板中，也要使用```<router-view></router-view>```才能渲染子路由*

