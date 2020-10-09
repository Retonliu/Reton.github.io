---
title: webpack入门
date: 2020-9-9 09:41
tags: 
- webpack
- 前端
- 工具
---

>前置知识: package.json定义了当前项目所需要的各种模块以及项目的配置信息。当执行npm install 命令的时候就会根据这个配置文件下载所需的内容。

1. 使用npm init          //生成package
2. npm install webpack webpack-cli   //下载webpack相关
webpack 本身就可以处理json和js文件所以不需要引入loder和plugin(打包命令 webpack .src/index.js -o ./build/built.js --mode=development 生产环境则development换成production)
3. 创建webpack配置文件 webpack.config.js
样式文件、图片文件、html文件等需要引入loder和plugin

+ loader: 
1. 下载
2. 使用

+ plugins：
1. 下载
2. 引入
3. 使用