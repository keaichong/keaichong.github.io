---
title: axios封装
date: 2019-07-11 16:15:17
tags: axios
---

## axios 封装 api 模块化 vuex

- https://juejin.im/post/5c3c544c6fb9a049d37f5903

- 在 src 目录下创建 utils/， 并创建 request.js 用来封装 axios，上代码：

```js
import axios from "axios";

// 创建axios 实例
const service = axios.create({
  baseURL: process.env.BASE_API, // api的base_url
  timeout: 10000 // 请求超时时间
});

// request 拦截器
service.interceptors.request.use(
  config => {
    // 这里可以自定义一些config 配置
    return config;
  },
  error => {
    //  这里处理一些请求出错的情况
    console.log(error);
    Promise.reject(error);
  }
);

// response 拦截器
service.interceptors.response.use(
  response => {
    const res = response.data;
    // 这里处理一些response 正常放回时的逻辑
    return res;
  },
  error => {
    // 这里处理一些response 出错时的逻辑
    return Promise.reject(error);
  }
);

export default service;
```

- 如何使用？ 我比较建议在 src/下创建 api 目录，用来统一管理所有的请求，比如下面这样：

```js
import request from "@/utils/request";
export default {
  //登陆
  login(data) {
    return request({
      url: "/login",
      method: "post",
      data
    });
  },
  //获取用户信息
  getuserInfo() {
    return request({
      url: "/userInfo",
      method: "get"
    });
  }
};
```

- 这样的好处是方便管理、后期维护，还可以和后端的微服务对应，建立多文件存放不同模块的 api。剩下的就是你使用到哪个 api 时，自己引入便可。
