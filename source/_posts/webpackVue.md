---
title: 基于webpack的vue项目踩坑经验
date: 2020-11-30 22：22
tags:
- webpack
- vue
- 前端
---

1. 使用webpack-dev-server之后浏览器报错无法找到特定id的节点。原来是打包之后的index.html中没有我的index.js中的new Vue挂载的节点。在webpack.config.js中给HtmlWebpackPlugin中添加template指定html文件加入指定节点就可以了