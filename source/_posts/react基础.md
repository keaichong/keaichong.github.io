---
title: react基础
date: 2019-03-07 20:39:27
tags: react
---

# react-基础-笔记

- [英文](https://reactjs.org/)-[中文](https://doc.react-china.org/)
- [sublime 语法提示](https://github.com/facebookarchive/sublime-react)
- [sublime 语法高亮](https://github.com/babel/babel-sublime)

## 前端的职责范畴

- 做网站前端（PCWeb 和移动 Web）- jquery
- 做后台开发（Node.js-java-php-python...）
- 做 APP（混合开发-react native）
- 做桌面程序（Electron）
- javascript 有可能在未来一统江湖
  <!-- more -->

## react 事件处理

我们通常建议在构造函数中绑定或使用属性初始化器语法来避免这类性能问题。

```js
//属性初始化绑定回调函数
class LoggingButton extends React.Component {
  // This syntax ensures `this` is bound within handleClick.
  // Warning: this is *experimental* syntax.
  handleClick = () => {
    console.log("this is:", this);
  };

  render() {
    return <button onClick={this.handleClick}>Click me</button>;
  }
}
```

```js
//构造函数中绑定
class Toggle extends React.Component {
  constructor(props) {
    super(props);
    this.state = {isToggleOn: true};

    // This binding is necessary to make `this` work in the callback
    this.handleClick = this.handleClick.bind(this);
  }Markdown Preview Enhanced

  handleClick() {
    this.setState(prevState => ({
      isToggleOn: !prevState.isToggleOn
    }));
  }
```

## React 概述

- 网站开发模式演变过程

  > 静态网站->动态网站（后端渲染）->Ajax->前后端渲染结合->前端渲染（前后端分离）SPA

- 静态资源（网页 HTML 本身、js、css、font、视频、音频...）
- 静态网站缺陷：
  - 可维护性比较低
  - 无法进行交互
- 动态网站
  - 可维护性明显增强
  - 并且可以处理参数，所以方便与客户端进行交互
- ajax 的诞生解决了阻塞问题
  - ajax 请求是异步的，页面不需要阻塞
  - ajax 一般请求的是数据（json）,浏览器通过 ajax 获取到数据之后，在浏览器中进行渲染（前端渲染）
  - 一般这种渲染方式处理的都是页面的局部（局部刷新）
- 所以有了 ajax 之后，一般都是前端渲染与后端渲染结合使用

  - 基于 ajax 进行前端渲染之后，导致前端的业务量明显增加，那么对代码的风格带来了挑战，EXTJS（MVC）、backbone 等这些 mvc 框架解决了代码风格的一些问题，但是并不能从根本上解决（还是需要程序员去操作 DOM）,所以为了从根本上解决前端代码的风格或者开发体验，后来就诞生了更加先进的前端框架：Angular、React、Vue（SPA）---声明式编程（基本上不再需要显示的操作 DOM），解决浏览器历史回退的问题（前端路由）

- React 特性
  - 声明式视图
    - 对于声明式组件，当数据变更的时候，React 低层负责高效更新。这种方式代码更加可预见并且更容易调试。
  - 组件化
    - 封装管理数据的组件，通过组合的方式实现复杂的 UI，组件的逻辑采用 js 实现而不是模板，这样可以保持数据在 DOM 之外。
  - 一次学习，随处编写
    - React 可以进行服务端渲染，也可以用于移动 APP 开发（React Native）

## vue 和 react 对比

`vue和react对比` [百度指数](http://index.baidu.com/?from=pinzhuan#/) [链接 1](https://github.com/HankBass/front-end-frameworks-comparison) [链接 2](https://www.zcfy.cc/article/react-or-vue-which-javascript-ui-library-should-you-be-using-2159.html)

## 辅助工具

1. babel
2. 插件
   - Simple React Snippets
   - JS JSX Snippets
   - jsx-beautify
   - Live Server

## React 之 HelloWorld

- [引入相关的库](https://raw.githubusercontent.com/reactjs/reactjs.org/master/static/html/single-file-example.html)

```JavaScript
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Document</title>
  <script type="text/javascript" src="./lib/react.development.js"></script>
  <script type="text/javascript" src="./lib/react-dom.development.js"></script>
  <script type="text/javascript" src="./lib/babel.min.js"></script>
</head>
<body>
  <div id="root"></div>
  <script type="text/babel" src="src/HelloWorld.js"></script>
</body>
</html>
```

- HelloWorld

```JavaScript
const element = (
  <div>
    {/*必须有根元素*/}
    <h1>Hello, world!</h1>
    <div>测试数据</div>
  </div>
)
ReactDOM.render(
  element,
  document.getElementById('root')
);
```

- 基本步骤
  - 引入 react 库文件 react 和 react-dom
  - 引入 babel 运行时
  - 基于 React 语法进行开发
- 细节分析
  - 运行环境
  - 案例语法

## JSX 基础语法

- 什么是 JSX 元素
  - 区分于元素 DOM 元素，React 元素本质上是普通对象，是组件的基本组成单元
- JSX 特性
  - 元素可以嵌套，但是必须有跟元素，也就是最外层必须有一个元素包裹
  - 标签必须闭合，标签中没有内容也需要闭合，比如<img/>
- JSX 嵌入表达式
  - JSX 本质上也是表达式
- JSX 属性
  - JSX 可以添加自定义属性，并且属性名采用驼峰式
  - 属性添加可以使用延展运算符

## JSX 的本质

- React.createElement(type, props, ...children)

```JavaScript
ReactElement createElement(
  string/ReactClass type,
  [object props],
  [children ...]
}
```

- 参数一为字符串或者为类
- 参数二为元素的属性列表
- 第三个参数表示子节点，可以把子节点单独传递，也可以组合为一个数组来传递
  - var root = React.createElement('ul', { className: 'my-list' }, child1, child2, child3);
  - var root = React.createElement('ul', { className: 'my-list' }, [child1, child2, child3]);
- 分析元素的渲染方式

## 组件化

- 组件化思想分析
  - web components
  - 单一职责
- 创建组件语法
  - 函数方式
  - 类方式
- 组件的状态 state
- 父组件向子组件传值 props
  - 单向数据流
  - 子组件不可以修改 props 数据

## 组件的生命周期

- componentWillMount 组件挂载之前调用，render()之前调用
- componentDidMount DOM 渲染完成后调用，可以用于加载后台数据
- componentDidUpdate 组件更新时触发该方法，初始渲染不调用
- componentWillUnmount 组件被销毁之前一般用于清理工作（定时器 timer、网络请求、订阅事件）

## 事件绑定

- 函数名采用驼峰式
- 函数值采用{函数名称}
- 阻止默认行为不可以使用 return false
- 事件函数中的 this 绑定
  - 构造函数中使用 bind(this)
  - 声明函数时使用箭头函数
- 函数传参

```jsx
<button onClick={(e) => this.deleteRow(id, e)}>Delete Row</button>
<button onClick={this.deleteRow.bind(this, id)}>Delete Row</button>
```

- 子组件向父组件传值

## 条件渲染与循环渲染

- 条件渲染
  - js 形式条件渲染
  - 元素变量
  - 行内条件渲染
  - 阻止组件渲染
- 循环渲染
  - 渲染多个元素
  - key 只在数组上下文中有含义
  - key 在兄弟节点之间必须唯一
  - JSX 中可以嵌入 map 结构

## 表单操作

> 表单元素本身就与别的元素不同，因为天生就包含一些初始状态

- 受控组件与非受控组件
  - 受控组件的数据由 React 组件控制
  - 非受控组件的数据由 DOM 控制

## 直接操作 DOM

- 什么情况需要直接操作 DOM
  - 管理焦点，文本选择或者媒体重放
  - 触发命令式动画
  - 集成第三方 DOM 库
- ref 用法

```
// 构造函数
this.textInput = React.createRef();
// 标签中
<input type="text" ref={this.textInput} />
// 使用
this.textInput.current.focus();
```

## JSX 进阶特性

- 点标记的组件用法<MyComponents.DatePicker color="blue"/>
- 动态组件名称
- props 值操作
- 组件 children

## React 实现原理分析

- 虚拟 DOM 原理
- 响应式编程

## 表单操作

> 表单元素本身就与别的元素不同，因为天生就包含一些初始状态

- 受控组件与非受控组件
  - 受控组件的数据由 React 组件控制
  - 非受控组件的数据由 DOM 控制
- checkbox 与 radio 组件



## 直接操作 DOM

- 什么情况需要直接操作 DOM
  - 管理焦点，文本选择或者媒体重放
  - 触发命令式动画
  - 集成第三方 DOM 库
- ref 用法

```
// 构造函数
this.textInput = React.createRef();
// 标签中
<input type="text" ref={this.textInput} />
// 使用
this.textInput.current.focus();
```

- 文件上传

## React 实现原理分析

- 虚拟 DOM 原理
- 响应式编程
- mvc/mvvm-->mv\*

## React 实现原理分析

- 虚拟 DOM 原理
- 响应式编程(数据驱动的开发模式)

## JSX 进阶特性

- 点标记的组件用法<MyComponents.DatePicker color="blue"/>
- 组件 children
- props 值操作
- 动态组件名称

## 后台数据处理

- [fetch-pollyfill](https://github.com/github/fetch#readme)

### 用法

```javascript
fetch(url, options).then(
  function(response) {
    // handle HTTP response
  },
  function(error) {
    // handle network error
  }
);
```

- 注意：fetch api 返回的是一个 promise 对象
- 参数：options
  - method(String): HTTP 请求方法，默认为 GET
  - body(String): HTTP 的请求参数
  - headers(Object): HTTP 的请求头，默认为{}
  - credentials(String): 默认为 omit,忽略的意思，也就是不带 cookie;还有两个参数，same-origin，意思就是同源请求带 cookie；include,表示无论跨域还是同源请求都会带 cookie
- 第一个 then 函数里面处理的是 response 的格式
- 响应
  - text(): 将返回体处理成字符串类型
  - json()： 返回结果和 JSON.parse(responseText)一样
  - blob()： 返回一个 Blob，Blob 对象是一个不可更改的类文件的二进制数据
  - arrayBuffer()
  - formData()

```javascript
fetch("/abc")
  .then(data => {
    return data.json();
  })
  .then(ret => {
    // 注意这里得到的才是最终的数据
    console.log(ret);
  });
```

### 注意事项

- cookie 传递
  - 必须在 header 参数里面加上 credientials: 'include'，才会如 xhr 一样将当前 cookies 带到请求中
- 错误处理
  - fetch 在服务器返回 4xx、5xx 时是不会抛出错误的，这里需要手动通过，通过 response 中的 ok 字段和 status 字段来判断

### axios

> [axios](https://github.com/axios/axios)：基于 http 客户端的 Promise，用于浏览器和 Node.js。

- axios 特性
  - 从浏览器发送 ajax 请求
  - 从 Node.js 发送 http 请求
  - 支持 Promise API
  - 请求和相应拦截器
  - 转换请求和响应数据
  - 取消请求
  - JSON 数据自动转换
  - 客户端支持防止 XSRF



## webpack 搭建 React 环境

## 官方脚手架

1. npm start
   - 在http://localhost:3000下监视文件，文件修改将自动更新，你可以在控制台中看到检测错误
2. npm test
   - 在交互监视模式下启动测试运行程序。
3. npm run build
   - 在生产环境中编译代码，并放在 build 目录中
4. npm run eject
   - 抽取出项目配置文件，这是一个单向操作，一旦你使用 eject，那么就不能恢复了
   - 使用说明：如果你对 create-react-app 这个构建工具和配置项不满意，你可以在任何时候 eject，从而导出可配置的模板

## react-router

- [react-router](https://github.com/ReactTraining/react-router)
- [doc](https://reacttraining.com/react-router/)

## 前端路由概念分析

- 前端路由与后端路由的区别
  - 后端路由
  - 前端路由

## React-router 之 HelloWorld

> 声明式路由

- 路由使用的基本步骤
  - 配置路由的容器 BrowserRouter
  - 配置路由连接 Link
  - 配置路由填充位置以及路径和组件的映射关系

## 嵌套路由

- 嵌套路由使用步骤
  - 在父路由的组件中配置子路由
  - 子路由同样需要配置 Link 和 Route

## 路由传递参数

- 路由传参指的是在路由的路径中通过【:参数名称】的方式进行传参，该参数在路由匹配的组件中通过【match.params.参数名称】的方式获取

## 路由重定向

- 路由的重定向通过 <Redirect to="目标"/>

## 自定义路由链接

## 编程式路由

## 路由

- 基本用法
- 嵌套路由
- 路由重定向
- 路由参数
- 编程式路由
- 自定义路由连接
