---
title: scale变形理解
date: 2020-10-5 19:23
tags: 
- css
- 前端
---

最近在用css实现点赞功能的时候，用到了scale实现点击的时候爱心会变大，用了css的变形过渡功能。因为我的点赞的图标是用两个圆形和一个正方形实现的爱心状。而scale的只需要加在这三个图形的容器上，所以就在思考scale是会将容器连同容器内的子元素一起变形吗？
于是我就做了个小实验
html代码如下：
```
    <div class="container">
            <div class="first">
                <div class="inner"></div>
            </div>
            <div class="second"></div>
        </div>
```
css代码如下：
```
.container {
    width: 200px;
    height: 200px;
    margin: 100px auto;
    border: 10px solid #000;
    cursor: pointer;
}
.container:active {
    transform: scale(2);
}
.first {
    display: inline-block;
    width: 80px;
    height: 80px;
    border: 1px solid blue;
}
.second {
    display: inline-block;
    width: 80px;
    height: 80px;
    background-color: red;
}
.inner {
    width: 60px;
    height: 60px;
    background-color: yellow;
}
```
点击之前
![](1.png)
点击之后
![](2.png)
可以看到确实是连同容器元素里面的所有元素，不管是否为直接子元素，一律放大同样的倍数。