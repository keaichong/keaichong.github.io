---
title: 数据类型判断watch回调
date: 2019-03-26 15:05:34
tags: js
---

1. typeof
2. instanceof
3. constructor
4. Object.prototype.toString
   https://blog.csdn.net/zjy_android_blog/article/details/81023177

个人理解:假设 arr 是一个数组,toString 是 object 的原型里面的方法其返回的是类似 '[object class]'的字符串,但是当我们使用 arr.toString()时，不能进行复杂数据类型的判断，因为它调用的是 Array.prototype.toString，虽然 Array 也继承自 Object，但 js 在 Array.prototype 上重写了 toString，将 toString 改变成转换为字符串的一个方法,而我们通过 toString.call(arr)实际上是改变 object 的 this 指向让 object 的 toString 重新通过原型链调用了 Object.prototype.toString。

<!-- more -->

> JavaScript 中一切都是对象，任何都不例外，对所有值类型应用 Object.prototype.toString.call() 方法结果如下：

```js
console.log(Object.prototype.toString.call(123)); //[object Number]
console.log(Object.prototype.toString.call("123")); //[object String]
console.log(Object.prototype.toString.call(undefined)); //[object Undefined]
console.log(Object.prototype.toString.call(true)); //[object Boolean]
console.log(Object.prototype.toString.call({})); //[object Object]
console.log(Object.prototype.toString.call([])); //[object Array]
console.log(Object.prototype.toString.call(function() {})); //[object Function]

// Object.prototype.toString ( )
// 在toString方法被调用时,会执行下面的操作步骤:
// 如果this的值为undefined,则返回"[object Undefined]".
// 如果this的值为null,则返回"[object Null]".
// 让O成为调用ToObject(this)的结果.
// 让class成为O的内部属性[[Class]]的值.
// 返回三个字符串"[object ", class, 以及 "]"连接后的新字符串.
```

## ES6 高阶箭头函数 函数柯里化

```js
function add(x) {
  return function(y) {
    return y + x;
  };
}
add(2)(3); //5

const adc = x => y => x + y;
adc(2)(3); //5
```

## watch 高级用法

1. watch 和 computed 详解 推荐阅读\*\*\*
   https://segmentfault.com/a/1190000012948175?utm_source=tag-newest
2. watch 高级用法
   https://www.cnblogs.com/forward-wuyi/p/9627962.html

```js
// 监听复杂数据类型需用深度监听
data(){
      return{
        first:{
          second:0
        }
      }
    },
    watch:{
      secondChange:{
        handler(oldVal,newVal){
          console.log(oldVal)  //当改变first.second值为2  打印2
          console.log(newVal)  //当改变first.second值为2  打印2
        },
        deep:true
      }
    },
```

- 问题

1. console.log 打印的结果,发现 oldVal 和 newVal 值是一样的都是修改后的,因为深度监听虽然可以监听到对象的变化,但是无法监听到具体对象里面那个属性的变化
2. oldVal 和 newVal 值一样的原因是它们索引同一个对象/数组。Vue 不会保留修改之前值的副本

```js
// 方法一：可以直接对用对象.属性的方法拿到属性
data(){
          return{
            first:{
              second:0
            }
          }
        },
        watch:{
          'first.second':function(newVal,oldVal){
            console.log(newVal,oldVal);//当改变first.second值为2  打印2和0
          }
        },
// 方法二：watch如果想要监听对象的单个属性的变化,必须用computed作为中间件转化,因为computed可以取到对应的属性值
data(){
      return{
        first:{
          second:0
        }
      }
    },
    computed:{
      secondChange(){
        return this.first.second
      }
    },
    watch:{
      secondChange(){
        console.log('second属性值变化了')
      }
    },
```
### 数据类型转换 toSting 和 valueOf

```js
var obj = {
   a: 1,
   toString: function () {
    console.log('toString')
    return '2'
   },
   valueOf: function () {
    console.log('valueOf')
    return 3
   }
  }
  console.log(obj == '2'); //依次输出 'valueOf' false
  console.log(String(obj));//依次输出 'toString' '2'
var obj = {
   a: 1,
   toString: function () {
    console.log('toString')
    return '2'
   },
   valueOf: function () {
    console.log('valueOf')
    return {} //修改为对象
   }
  }
  console.log(obj == '2'); //依次输出 'valueOf' 'toString' true
  console.log(Number(obj));//依次输出 'valueOf' 'toString' 2
```
- 在相等运算符的操作中，对象会先调用 valueOf 如果返回的值是一个对象, 就会调用 toSting， null除外，然后用返回的值进行比较，第一个例子 相当于 3 == '2' 输出 false， 第二个例子由于执行valueOf 返回的是一个对象， 然后执行 toString， 最后相当于 '2' == '2' 输出true在 Number 和 String 方法中 Number会先调用 valueOf, 后调用 toString， String方法中是相反的。
- 数据类型的转换除了上面的两个例子外，还存在在各种其他操作中，如数值运算，当涉及到引用类型时，都会调用valueOf 或 toString 方法，只要是对象都会继承这两个方法,我们可以重新覆盖这两个方法，从而影响数据类型转换的行为

### vuex state写法
```js
export default {
    get UserToken() {
        return localStorage.getItem('token')
    },
    set UserToken(value) {
        localStorage.setItem('token', value)
    },
    /* 导航菜单是否折叠 */
    isSidebarNavCollapse: false,
    /* 面包屑导航列表 */
    crumbList: []
}
```