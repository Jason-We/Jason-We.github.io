---
title: npm命令记录
date: 2021-01-06 08:59:42
tags: npm
---

## npm install

```
npm install               #(with no args, in package.json dir)
npm install moduleName    # 安装模块到项目目录下
npm install -g moduleName # -g 的意思是将模块安装到全局，具体安装到磁盘哪个位置，要看 npm config prefix 的位置。
npm install --save moduleName   # --save 的意思是将模块安装到项目目录下，并在package文件的dependencies节点写入依赖。
npm install --save-dev moduleName # --save-dev 的意思是将模块安装到项目目录下，并在package文件的devDependencies节点写入依赖。
```

使用原则：项目部署运行时需要的包使用 --save ， 否则使用 --save-dev  

## npm uninstall

使用方法： 和install 一样， 只不过功能不同，uninstall 是卸载项目的依赖包