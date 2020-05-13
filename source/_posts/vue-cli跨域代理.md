---
title: vue-cli跨域代理
date: 2019-08-13 09:28:47
tags:  vue
---
{% asset_img 1565659808(1).jpg %}

- 问：proxyTable 里面的pathRewrite里面的‘^/iclient’:'' 什么意思？

1. 答：用代理, 首先你得有一个标识, 告诉他你这个连接要用代理. 不然的话, 可能你的 html, css, js这些静态资源都跑去代理. 所以我们只要接口用代理, 静态文件用本地.

2. '/iclient': {}, 就是告诉node, 我接口只要是'/iclient'开头的才用代理.所以你的接口就要这么写 /iclient/xx/xx. 最后代理的路径就是 http://xxx.xx.com/iclient/xx/xx.

3. 可是不对啊, 我正确的接口路径里面没有/iclient啊. 所以就需要 pathRewrite,用''^/iclient'':'', 把'/iclient'去掉, 这样既能有正确标识, 又能在请求接口的时候去掉iclient.如果本身的接口地址就有'/iclient'这种通用前缀,就可以把pathRewrite删掉.注意这个方式只能在开发环境中使用