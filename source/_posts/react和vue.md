---
title: react和vue
date: 2019-03-15 00:04:32
tags: react
---

#### 路由-vue-router-嵌套路由

> children 用法和 routes 一样

```js
1. $route.params.id  路由配置对象$route -> 获取数据时
2. this.$router.push()  路由实例化对象 ->调方法
```

#### git-介绍安装

> 开发中->管理代码->1 每次记录代码变化 2 协同开发 3 把代码托管到平台(网站) -> git/svn
>
> 版本控制工具(管理代码->合代码):git/svn

1. git 命令行工具

2. git 是软件(git 官网->找系统 32/64->下一步安装)

3. 安装后的结果是: 文件夹->右键->gitbash/git->git 指令

   ```bash
   // 检查git版本
   git --version
   ```
<!-- more -->
#### git-基础概念

> 安装 git 软件->gitbash(小黑框)->使用 git 指令

> 在使用 git 指令之前 .配置邮箱名字

```bash
$ git config --global user.name "xxx"
$ git config --global user.email xxx@example.com
```

> 可以使用 git 版本控制 -> 管理代码->管理流程:

1. 工作区(项目代码所在的文件夹)->暂存区(临时中转) : git add .
2. 暂存区->本地仓库(项目代码所在文件夹中有个文件)
3. 本地仓库的代码->代码托管平台(网站:github/码云)

#### git-基本操作

1. 新建项目目录 04/code/gitdemos
2. gitdemos 右键->gitbash->执行 git 指令

```bash
// 当前gitdemos项目可以使用git去管理了
// 效果: 生成.git文件
git init
// 检查每个文件的状态(未跟踪/已修改)
// git status
// 把工作区代码->暂存区
git add .
// 暂存区-> 本地仓库
git commit -m "注释"
```

> 注意: git init 只需要写一次

#### git-远程仓库

> 代码托管平台(github/码云)

1. 注册
2. 登录
3. 新建远程仓库 (右上角+->new->命名->create)

```bash
// 关联远程仓库
git remote add origin https://github.com/自己的账号/gitdemos64.git
// 推送代码 keaichong:Song.316113
git push -u origin master
```

```bash'
// 开发功能1 -> 完成
git add .
git commit -m "注释1"
// 开发功能2 -> 完成
git add .
git commit -m "注释2"
// 推送代码
git push
```

> git 基本使用-> git 没讲完

#### vue-cli 工具-介绍

> vue 开发项目-> 本地服务器+less 配置+好多辅助开发的工具都需要配置+新建好多文件夹(静态资源的文件/项目入口文件等)->结果: 使用一个 vue 开发时工具帮助我们生成 vue 项目目录->vue-cli 脚手架

1. vue-cli 是 vue 开发时必用工具
2. vue-cli 是全局命令行工具(-g 全局安装)

```bash
// 全局安装脚手架工具(默认安装最新稳定版3+)
npm install -g @vue/cli
// 检查版本
vue --version
```

#### vue-cli-安装和 2-3 版本解释

> 目的:安装 3+版本->使用 2 版本的指令

```bash
// 安装桥接工具
npm install -g @vue/cli-init
// 可以使用2版本的指令
// vue项目根据其复杂程度可以有多种不同的目录
// vue复杂 -> 目录文件多一些
// vue项目简单->少一些文件
// webpack-simple固定写法(简单vue项目目录)
vue init webpack-simple 项目文件所在目录的文件夹名字
//vuecli3
vue create my-project
```

> 注意: 2 和 3 版本的指令不一样

#### vue-cli-创建项目

1. 来到目录 -> 打开 cmd
2. vue init webpack 项目名称

```bash
// 提示
// 项目名
// 描述
// 作者
// 认证
// sass -> N
cd 项目名称目录
npm i
// 启动开发模式:会把生成的vue项目在一个自带的本地服务器进行运行+ 自动打开浏览器
// 拓展: 开发模式/测试/上线(生产)
npm run dev
```

#### vue-cli-项目目录解释

> src

1. main.js 入口文件 : 引入其他包/样式
2. App.vue 根组件: 展示其他组件
   1. 一个.vue 文件就是一个组件
   2. .vue 文件代码三部分:template/script/style
3. assets/静态资源(图片/字体/.css 等)

> index.html 不需要写代码

> .gitignore: git 排除忽略文件

#### 开发-react 脚手架-介绍-安装

> 30 步->基于 webpack->react->可以写 react 代码->

> vue->脚手架快速生成->vuecli
>
> react->脚手架快速生成->create-react-app

1. npm i -g create-react-app

2. 进入期望的项目所在的位置->cd

3. create-react-app 文件夹名字 reactclidemo

   > network 有关->安装失败->再安装->清 npm 产生错误缓存->
   >
   > 1. npm cache clean --force
   > 2. 找到 cache 目录->手动删除

4. cd reactclidemo

5. npm start->猜测?启动项目+open

#### 开发-react 脚手架-目录说明-简化模板

> npm start->1.跑项目 2.自动浏览器

> 目录:
>
> 1. public
>    1. index.html->div#root
>    2. manifest.json->H5 新特性->离线缓存
> 2. **src/**
>    1. index.js->入口->导入根组件
>    2. index.css->针对 index.js 的样式
>    3. App.js->根组件->显示其他.js 组件
>    4. App.css->根组件的样式
>    5. serviceWorker->针对 mainfest 的服务端配置
>
> 指令->readme.md
>
> 1. **npm start**
>
> 2. npm run build
>
> 3. npm test->跑测试用例
>
> 4. npm run eject->暴露出 webpack 配置/服务器配置
>
>    > 不可逆操作!

#### 开发-react 脚手架-业务编写

> tab 切换->在脚手架目录->新建.js 组件->编码

#### 路由-实现原理

> 一 开发 SPA 组成原理:1. 前后端分离 2.**前端路由**
>
> vue 开发 SPA->vue-router->router-link+router-view this.\$router.push()
>
> react 开发 SPA->路由包->react-router-dom(4 版本)
>
> 二:前端路由->js->2 种实现方式
>
> 1. hash(#)
> 2. H5->history(浏览器历史访问记录)
>
> 三:效果:url 标识变化->页面局部内容发生改变->演示(hash/)
>
> 四:react 提供了独立的包->实现路由效果

#### 路由-react-router-dom-体验

> 讲的 4 版本 react-router-dom

1. npm i react-router-dom

2. 新建 router/01.js

3. 导入 react 和 react-router-dom 解构:

   > import { BrowserRouter as Router, Route, Link } from 'react-router-dom'

4. 配置 Router+Link+Route+提供组件

#### 路由 react-router-dom-步骤

1. 安装
2. 导入->as Router + Link +Route
3. return ->Router>(Link*n+Route*n)
4. Router->所有路由标签的最外层容器
5. Router 里面 Link->导航链接->to="/"
6. Router 里面 Route->匹配路由同时提供填充位置->会把匹配到的组件显示在这个位置

> 注意: Router 中只能有一个子元素

#### 路由-react-router-dom-嵌套

> 在一级路由匹配到的组件内容中写 Link+Route

#### 路由-重定向

> 1. 点击 A->显示的是 B
> 2. 所有的 route 没有匹配到->显示已经存在的组件
>
> > 用法
>
> 1. 导入
> 2. 在 Route 末尾增加<Redirect to="/标识">
> 3. 在所有填充位外层包裹 Switch

#### 路由-react-router-dom-嵌套

> 在一级路由匹配到的组件内容中写 Link+Route

#### 路由-重定向

> 1. 点击 A->显示的是 B
> 2. 所有的 route 没有匹配到->显示已经存在的组件
>
> > 用法
>
> 1. 导入
> 2. 在 Route 末尾增加<Redirect to="/标识">
> 3. 在所有填充位外层包裹 Switch
