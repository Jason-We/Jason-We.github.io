---
title: vue cli3.0+ 跨域配置
date: 2020-10-28 21:29:47
categories: vue
tags: 
  - vue
  - axios
  - nginx
---



### 配置baseURL

根据项目axios的引入方式， 可以分为两种配置方式：

- 如果axios 是npm install 加入的，那可以在在项目的main.js中配置：

  `Axios.defaults.baseURL = '/api'`

- 如果是通过vue@cli  ，即 vue add axios 加入的，则可以在plugins文件夹中的axios.js中配置：

  ```
  let config = {
    baseURL: '/api'
    // baseURL: process.env.baseURL || process.env.apiUrl || ""
    // timeout: 60 * 1000, // Timeout
    // withCredentials: true, // Check cross-site Access-Control
  };
  ```

  

### 配置axios跨域

配置完baseURL后，就可以根据baseURL进行跨域配置了。

- 开发环境

  新建vue.config.js，并在其中配置跨域方案：

  ```
  module.exports = {
    devServer: {   //这里解决开发环境的跨域问题， 生产环境的跨域问题需要再nginx服务器解决
      proxy: {
        '/api': {
          // 此处的写法，目的是为了 将 /api 替换成 http://localhost:8088/
          target: 'http://localhost:8088/',
          // 允许跨域
          changeOrigin: true,
          ws: true,
          pathRewrite: {
            '^/api': ''
          }
        }
      }
    }
  }
  ```

  

- 生产环境

  使用nginx 服务器， 配置文件nginx.conf 中增加server的配置 ：

  ```
  listen       8081;   
  server_name  localhost;
  location / {
     root   html; #这里的html是指 nginx根目录的html文件夹，即你项目打包好的dist目录下的文件全部拷贝至这里，（要先将html目录下的文件删掉）
     index  index.html index.htm;
     try_files $uri $uri/ /index.html;
  }
  location /api/ {               #这里/api/的配置和上面的baseURL的配置是对应的。
     proxy_pass   http://localhost:8088/;   #这里的配置表示将请求都转发至这个地址
  }
  ```

> ok，以上就是使用vue cli 3.0+ 开发vue项目时配置axios跨域的常见解决办法啦。留作备忘！