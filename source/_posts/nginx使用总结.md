---
title: nginx使用总结
date: 2020-10-31 17:30:42
tags:
  - nginx
  - 服务器
categories: 服务器
---

## 使用`nginx`作代理服务器

在做前后端项目分离并部署到生产环境上时，可以选择`nginx`作前端项目的服务器，使用起来还是很方便的。同时，仅需简单的配置即可实现端接口转发，具体操作可以看之前的一篇blog: [vue cli3.0+ 跨域配置](https://jason-we.github.io/2020/10/28/vue-cli3-0-kua-yu-pei-zhi/)

## `nginx`常用命令

```
--nginx 启停命令
start nginx.exe                     //启动nginx
nginx.exe -s stop                   //停止nginx
nginx.exe -s quit                   //优雅停止nginx，有连接时会等连接请求完成再杀死worker进程  
nginx.exe -s reload                //重启，会重新加载nginx的配置文件
（*linux相应命令去掉 ".exe" 后缀即可）
--nginx 其他命令
nginx -v            查看版本  
nginx -t            检查nginx的配置文件
nginx -h            查看帮助信息
nginx -V            详细版本信息，包括编译参数 
nginx  -c filename  指定配置文件
-- Linux 下nginx常用运维命令
ps -ef |grep nginx  查看nginx的进程号
whereis nginx       查看nginx安装路径
配置nginx开机自启动
$ sudo systemctl start nginx #systemd  
OR 
$ sudo service nginx start   #sysvinit 
```

