---
title: eslint使用方法
date: 2020-10-9 21:45
tags:
- eslint
- 前端
- 工具
---
> eslint是帮助前端工程师规范js代码规范的工具
eslint使用方法:
1. 不依赖构建工具。 npm init 下包。
配置package.json文件如下：
```
"scripts": {
    "test": "react-scripts test --env=jsdom",
    "lint": "eslint src",
    "lint:create": "eslint --init"
}
```
npm run lint:create生成.eslint.js文件。生成.eslint.js文件的配置是通过终端问答式来配置的。
然后就可以创建一个src文件夹，通过使用npm run lint来检验src文件夹下的js文件是否写的规范。
在package.json当中的script的那行"lint": "eslint src"，修改为"lint": "eslint src --fix"，即增加了--fix参数，可以让eslint帮忙修复基础的规范错误。
如果要对一些配置作出修改得话，可以在.eslint.js文件中的rules做出修改。
+ off" 或 0 - 关闭规则
+ "warn" 或 1 - 开启规则，使用警告级别的错误：warn (不会导致程序退出)
+ "error" 或 2 - 开启规则，使用错误级别的错误：error (当被触发的时候，程序会退出)
某些规则具有属性的话（除了以上的开启或者关闭规则，还可以通过查询规则表来进行修改。

2. 

>参考博客：https://www.jianshu.com/p/ad1e46faaea2

