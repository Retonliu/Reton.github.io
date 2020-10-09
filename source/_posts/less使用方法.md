---
title: less使用方法
date: 2020-10-9 21:20
tags: 
- less
- 前端
- 工具
---

less使用方法： 
1. 通过npm安装好less，npm install less -g。然后在html当中用link标签引入的是css文件，然使用命令lessc 将less文件转换为css文件。
2. 由于在浏览器中直接引入less文件会引发跨域问题，官方解释是这样的，*Due to the same origin policy of browsers, loading external resources requires enabling CORS*。**在浏览器中打开的文件使用的是文件协议file，所以需要解决跨域问题**，方法就是在本地使用服务器。要在本地使用服务端，方法就是使用nodejs，或者使用基于nodejs的构建工具webpack。
webpack的使用方法如下：
npm下载less-loader。然后配置文件中修改：
```
 {
                test: /\.less$/,
                use: [
                    //'style-loader',
                    MiniCssExtractPlugin.loader,
                    'css-loader',
                    {
                        loader: 'postcss-loader',
                        options: {
                            ident: 'postcss',
                            plugins: () => [
                                //帮助postcss找到package.json中browserslist里面的配置，通过配置加载指定的css兼容性样式
                                require('postcss-preset-env')()
                            ]
                        }
                    },
                    'less-loader',
                ]
            }
```
