---
title: css实现爱心桃
date: 2020-10-5 21:43
tags: 
- css
- 前端
---

实现爱心桃的基本思路就是先定义一个矩形父元素作为容器，然后左上角和右上角各自放置一个圆形，*注意两个圆形之间要有重叠部分*，然后在矩形容器中心放置一个正方形，正方形使用变形效果实现翻转45度。三个图形重叠即可实现一个爱心。

html代码如下:
```
<div class="praise">
    <div class="disc1"></div>
    <div class="disc2"></div>
    <div class="square"></div>
</div>
```
其中praise是矩形容器，disc1是左上角的圆形，disc2是右上角的圆形，square是放置在中心的正方形。
css代码如下：
```
.praise {
    cursor: pointer;
    position: relative;
    width: 15px;
    height: 15px;
    .disc1 {
        position: absolute;
        left: 0;
        top: 0;
        width: 9px;
        height: 9px;
        border-radius: 50%;
        background-color: #CD3333;
    }
    .disc2 {
        position: absolute;
        right: 0;
        top: 0;
        width: 9px;
        height: 9px;
        border-radius: 50%;
        background-color: #CD3333;
    }
    .square {
        position: absolute;
        left: 50%;
        top: 50%;
        width: 9px;
        height: 9px;
        margin-left: -4.5px;
        margin-top: -4.5px;
        transform: rotate(45deg);
        background-color: #CD3333;
    }
}
```
1. 首先设置矩形容器praise的宽度和高度，我是都设置了15px。
2. 给disc1设置为绝对定位（注意praise要设置为非静态定位），然后top和left都设置为0。让它处于左上角，同时宽度和高度要略大于praise的二分之一。我是都设置了9px。
3. disc2同理，不过是放在右上角。
4. 正方形square设置为绝对定位，通过调整位置和外边距让正方形处于praise的正中心，然后使用rotate让正方形旋转45度，正好成为爱心向下的那一角。
效果如下：
![](1.png)
*旁边的白色是背景颜色*
