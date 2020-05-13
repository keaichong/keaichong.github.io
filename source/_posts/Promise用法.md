---
title: Promise用法
date: 2019-02-28 10:01:47
tags: js
---

## promise 用法

参考:

1. E:\北京顺义黑马前端与移动开发基础 62 期\就业班 品优购前台\day02\03-加密视频 07 20 分钟详细说明了 promise
2. http://www.ruanyifeng.com/blog/2015/05/async.html 阮一峰微博
   > Promise 的构造函数接收一个参数，是函数，并且传入两个参数：resolve，reject，分别表示异步操作执行成功后的回调函数和异步操作执行失败后的回调函数,在异步操作成功时调用，并将异步操作的结果作为参数传递出去
   > 我们用 Promise 的时候一般是包在一个函数中，在需要的时候去运行这个函数，

- 用法:在一个函数内部 return 一个 promise 对象,再调用这个函数的时候就得到了 promise 对象,就可以用 promise 的.then 方法,then 方法可以接受两个回调函数作为参数,一个回调函数的参数是 promise resolve 的结果,第二个回调函数可选,参数是 reject 的结果

## 链式操作的用法

从表面上看，Promise 只是能够简化层层回调的写法，而实质上，Promise 的精髓是“状态”，用维护状态、传递状态的方式来使得回调函数能够及时调用，它比传递 callback 函数要简单、灵活的多。所以使用 Promise 的正确场景是这样的：

<!-- more -->

```js
function runAsync1() {
  return new Promise(function(resolve, reject) {
    //做一些异步操作
    setTimeout(function() {
      console.log("异步任务1执行完成");
      resolve("随便什么数据1");
    }, 1000);
  });
}

function runAsync2() {
  return new Promise(function(resolve, reject) {
    //做一些异步操作
    setTimeout(function() {
      console.log("异步任务2执行完成");
      resolve("随便什么数据2");
    }, 1000);
  });
}

function runAsync3() {
  return new Promise(function(resolve, reject) {
    //做一些异步操作
    setTimeout(function() {
      console.log("异步任务3执行完成");
      resolve("随便什么数据3");
    }, 1000);
  });
}

runAsync1()
  .then(function(data) {
    console.log(data);
    return runAsync2();
  })
  .then(function(data) {
    console.log(data);
    return runAsync3();
  })
  .then(function(data) {
    console.log(data);
  });
```

结果

```shell
异步任务1执行完成
随便什么数据1
异步任务2执行完成
随便什么数据2
异步任务3执行完成
随便什么数据3
```

在 then 方法中，你也可以直接 return 数据而不是 Promise 对象，在后面的 then 中就可以接收到数据了，比如我们把上面的代码修改成这样：

```js
runAsync1()
.then(function(data){
    console.log(data);
    return runAsync2();
})
.then(function(data){
    console.log(data);
    return '直接返回数据';  //这里直接返回数据
})
.then(function(data){
    console.log(data);
```

```shell
异步任务1执行完成
随便什么数据1
异步任务2执行完成
随便什么数据2
直接返回数据
```

## catch 的用法

Promise 对象除了 then 方法，还有一个 catch 方法,它和 then 的第二个参数一样，用来指定 reject 的回调，用法是这样：

```js
getNumber()
.then(function(data){
    console.log('resolved');
    console.log(data);
})
.catch(function(reason){
    console.log('rejected');
    console.log(reason);
```

效果和写在 then 的第二个参数里面一样。不过它还有另外一个作用：在执行 resolve 的回调（也就是上面 then 中的第一个参数）时，如果抛出异常了（代码出错了），那么并不会报错卡死 js，而是会进到这个 catch 方法中。并把错误的原因传入 reason 参数中,请看下面的代码：

```js
getNumber()
.then(function(data){
    console.log('resolved');
    console.log(data);
    console.log(somedata); //此处的somedata未定义
})
.catch(function(reason){
    console.log('rejected');
    console.log(reason);
```

## Promise.all

用 Promise.all 来执行，all 接收一个数组参数，里面的值最终都算返回 Promise 对象,会等待最慢的一个异步任务执行完成之后返回结果,等到它们都执行完后才会进到 then 里面, 返回结果按照传入的顺序存在一个数组之中

```js
Promise.all([runAsync1(), runAsync2(), runAsync3()]).then(function(data) {
  console.log(data);
});
```

{% asset_img promise.png  %}
有了 all，你就可以并行执行多个异步操作，并且在一个回调中处理所有的返回数据，是不是很酷？有一个场景是很适合用这个的，一些游戏类的素材比较多的应用，打开网页时，预先加载需要用到的各种资源如图片、flash 以及各种静态文件。所有的都加载完后，我们再进行页面的初始化。

## try...catch

await 命令后面的 Promise 对象，运行结果可能是 rejected，所以最好把 await 命令放在 try...catch 代码块中

```js
async function myFunction() {
  try {
    await somethingThatReturnsAPromise(); //等待返回一个promise对象
  } catch (err) {
    console.log(err);
  }
}
// 另一种写法
async function myFunction() {
  await somethingThatReturnsAPromise().catch(function(err) {
    console.log(err);
  });
}
```

## async 函数简单用法

async 的用法，它作为一个关键字放到函数前面，用于表示函数是一个异步函数，因为 async 就是异步的意思， 异步函数也就意味着该函数的执行不会阻塞后面代码的执行。 写一个 async 函数

```js
async function timeout() {
  return "hello world";
}
console.log(timeout());
// 控制台打印
//Promise {<resolved>: "hello world"}
```

原来 async 函数返回的是一个 promise 对象，如果要获取到 promise 返回值，我们应该用 then 方法， 继续修改代码

```js
async function timeout() {
  return "hello world";
}
timeout().then(result => {
  console.log(result);
});
console.log("虽然在后面，但是我先执行");
//控制台打印
//虽然在后面，但是我先执行
//hello world
```

现在写一个函数，让它返回 promise 对象，该函数的作用是 2s 之后让数值乘以 2

```js
// 2s 之后返回双倍的值
function doubleAfter2seconds(num) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve(2 * num);
    }, 2000);
  });
}
```

再写一个 async 函数，从而可以使用 await 关键字， await 后面放置的就是返回 promise 对象的一个表达式，所以它后面可以写上 doubleAfter2seconds 函数的调用

```js
async function testResult() {
  let result = await doubleAfter2seconds(30);
  console.log(result);
}
//调用
testResult();
//控制台打印
//2s后打印 60
```

## 注意点

https://www.jianshu.com/p/fe0159f8beb4

> 注意:promise 的 then()和 catch(err=>err)的回调结果都会走 return 之后的下一个 promise 的点 then 方法里面,如果需要把第一个 promise 里面的错误抛出给下一个 promise 的 catch 接收,第一个 promise 的 catch 要写这样 .catch(err => Promise.reject(err)) ,Promise.reject()是快速的获取一个拒绝状态的 Promise 对象
> 使用静态 Promise.reject()方法

```js
//then 方法可以接受两个回调函数作为参数,一个回调函数的参数是 promise resolve 的结果,第二个回调函数可选,参数是 reject 的结果
//方法一
Promise.reject("Testing static reject").then(
  function(reason) {
    // 未被调用
  },
  function(reason) {
    console.log(reason); // "Testing static reject"
  }
);
//方法二等价方法一(主动创建的reject会走promise的catch也就是第二个回调数)
Promise.reject("Testing static reject")
  .then(function(reason) {
    // 未被调用
  })
  .catch(function(reason) {
    console.log(reason); // "Testing static reject"
  });
```

结论:

1. 虽然 await 会阻塞 async 异步函数，但是并没有阻塞主线程。
2. 虽然 await 阻塞异步函数向后执行，看起来像是同步的，但是它本质还是异步的，我们同样可以并行执行。而同步函数不能并行执行。
