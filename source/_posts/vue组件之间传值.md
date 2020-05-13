---
title: vue双绑原理组件之间传值
date: 2019-02-23 22:36:36
tags: vue
---

## 复习

> v-on 指令用于监听 DOM 事件 形式如：v-on:click 缩写为 @click
> v-model 在表单控件或者组件上创建双向绑定
> v-bind 缩写 :）动态地绑定一个或多个特性、或一个组件 prop 到表达式
> 触发事件 this.$emit("事件名",要传的数据shican)   绑定事件this.$on("事件名",要传的数据 xincan)
> 注意，在 Vue 实例中 data 属性其实不一定使用 data() { return {} }的（方法），可以直接用 data: { }（对象）。因为在组件中，如果 data 声明为一个方法，就可以使组件中的数据独立，避免相互影响。
> 子组件的命名无法识别驼峰命名法，当组件作为标签时，需要使用-和小写字母。

## 父传子

1. 声明属性 props:["属性 a"]
2. 赋值 使用组件时 <data-st :msg="父组件data的数据"></data-st>
3. 使用 子组件 template {{a}}

```html
<!-- 子组件页面 -->
<div id="app">
  <div>你好吗</div>
  <data-st :msg="str" class="xx"></data-st>
</div>
```

<!-- more -->

{% asset_img ps.png  %}

```js
Vue.component("DataChild", {
  data() {
    return {
      count: 100
    };
  },
  template: `
            <div>
            <h3 >你好啊---{{msg}}   </h3>
            <div>{{count}}</div>
            </div>`,
  props: ["msg"]
});

new Vue({
  el: "#app",
  data: {
    str: "我是父组件data的数据"
  },
  methods: {}
});
// 选项props
// 1. props是组件的选项
// 2. props的值可以是字符串数组
// 3. props数组里面的元素称之为prop(属性) 属性=?值
// 4. prop的值来源于外部的(组件的外部)
// 5. prop(我们这里是msg)是组件的属性->自定义标签的属性
// 6. prop的赋值位置(在使用组件时,通过标签属性去赋值)
// 7. prop的用法和data中的数据用法一样->{{msg}}
// 补充 : 组件的数据的值来源于自己(内容),此时这个数据的声明写在data中
// 推论-> data的数据的值只能来源于自己->
// 2个组件-> newVue的视图当成整个网页的根组件
// 此时 根组件就是newVue的视图div#app  子组件就是DataChild
```

## 子传父

1. 子组件创建自定义事件，事件的处理函数是父组件的函数，子组件再通过 this.\$emit 触发自定义事件
2. 重点: 主要是通过\$emit 方法来实现传参的方式，第一个参数是自定义事件名称，第二个则是要传的数据
3. 触发事件 this.\$emit("事件名",要传的数据)
4. 在使用组件时绑定自定义事件

```html
<!-- 父组件页面 -->
<div id="app">
  <data-child class="xx" @transfer="parent"></data-child>
</div>
```

{% asset_img sp.png  %}

```js
Vue.component("DataChild", {
  data() {
    return {
      str: "我从子组件data传过来",
      str1: "我是子组件data里面的数据"
    };
  },
  template: `
            <div>
            <h3>右边插值表达式展示子组件data数据--->{{str1}}</h3>
            <button @click="son" >点我传值给父组件</button>
            </div>`,
  methods: {
    son() {
      //触发事件
      this.$emit("transfer", this.str);
    }
  }
});
new Vue({
  el: "#app",
  data: {
    count: 100
  },
  methods: {
    parent(str) {
      alert(str + "---" + this.count);
    }
  }
});
```

## 兄弟组件传值

> b 组件传值给 c 组件
> 方法: eventBus.js(中央事件总线):给其他文件提供了共享/公用的对象(newVue())

1. B 中 触发事件 vm.\$emit("event",值 num)
2. C 中 绑定事件 vm.\$on("event",(argv)=>{argv 就是值 num})

> 注意:先绑定事件,再触发事件 代码写在 created 是为了让事件自动绑定触发

{% asset_img BC.png  %}
argv 就是 B 组件传过来的值 100

> 下面是 eventBus.js

```js
// js代码+实例化vm->具有独立功能的js代码->js模块
import Vue from "vue";
const vm = new Vue();
export default vm;
```

## Vue 中如何在组件内部实现一个双向数据绑定？

> 具体思路：父组件通过 props 传值给子组件，子组件通过 \$emit 来通知父组件修改相应的 props 值，具体实现如下：

```html
<div id="app">
  <comp-one :value="value" @input="value=arguments[0]"></comp-one>
</div>
```

```js
const component = {
  data() {
    return {};
  },
  created() {
    this.getdata();
  },
  props: ["value"],
  template: `<div >   
 <input type ="text" @input="handleInput" :value="value">
 </div>`,
  methods: {
    handleInput(e) {
      this.$emit("input", e.target.value);
    },
    getdata() {
      console.log(this.value);
    }
  }
};
new Vue({
  components: {
    CompOne: component
  },
  el: "#app",
  data() {
    return {
      value: 123
    };
  }
});
```

## 双向绑定原理

- vue 关于数组和对象的更新

1. 由于 JavaScript 的限制，Vue 不能检测以下变动的数组： 一是当你利用索引直接设置一个项时，例如：vm.items[indexOfItem] = newValue 二是当你修改数组的长度时，例如：vm.items.length = newLength
2. 还是由于 JavaScript 的限制，Vue 不能检测对象属性的添加或删除：

```js
var vm = new Vue({
  data: {
    items: ["a", "b", "c"]
  }
});
vm.items[1] = "x"; // 不是响应性的
vm.items.length = 2; // 不是响应性的
// 为了解决第一类问题，以下两种方式都可以实现和 vm.items[indexOfItem] = newValue 相同的效果，同时也将触发状态更新：

// Vue.set
Vue.set(vm.items, indexOfItem, newValue);
// 你也可以使用 vm.$set 实例方法，该方法是全局方法 Vue.set 的一个别名：
vm.$set(vm.items, indexOfItem, newValue);
// Array.prototype.splice
vm.items.splice(indexOfItem, 1, newValue);

// 为了解决第二类问题，你可以使用 splice：
vm.items.splice(newLength);
```

```js
// 对象删除或添加属性 渲染方法一
this.$set(this.userProfile, "age", "18");
//删除或添加属性 渲染方法二
//Object.assign(目标,...源对象) 方法用于将所有可枚举属性的值从一个或多个源对象复制到目标对象。它将返回目标对象。
Object.assign(this.userProfile, {
  book: "三国演义"
});
```

vue 绑定数组里面对象变化无法更新 view
Vue 是通過監測  get, set 來得知數據是否更新，而數組的索引是沒有 get、set 的，所以 Vue 才沒辦法監聽，這是 javascript 語言特性的限制

vue 是通过 ES5 中的 Object.defineProperty()来实现数据劫持的。在 data 中的每一个属性都有一个 get 和 set 方法,get 获取数据 set 设置数据
https://www.cnblogs.com/canfoo/p/6891868.html

```js
var Book = {};
var name = "";
Object.defineProperty(Book, "name", {
  set: function(value) {
    name = value;
    console.log("你取了一个书名叫做" + value);
  },
  get: function() {
    return "《" + name + "》";
  }
});
Book.name = "vue权威指南"; //你取了一个书名叫做vue权威指南
console.log(Book.name); // 《vue权威指南》
```

我们通过 Object.defineProperty( )设置了对象 Book 的 name 属性，对其 get 和 set 进行重写操作，顾名思义，get 就是在读取 name 属性这个值触发的函数，set 就是在设置 name 属性这个值触发的函数，所以当执行 Book.name = 'vue 权威指南' 这个语句时，控制台会打印出 "你取了一个书名叫做 vue 权威指南"，紧接着，当读取这个属性时，就会输出 "《vue 权威指南》"

## Object.defineProperty

https://imweb.io/topic/56d40adc0848801a4ba198ce

> 语法 Object.defineProperty(object, propertyname, descriptor)

> 参数

1. object 必需。 要在其上添加或修改属性的对象。 这可能是一个本机 JavaScript 对象（即用户定义的对象或内置对象）或 DOM 对象。
2. propertyname 必需。 一个包含属性名称的字符串。
3. descriptor 必需。 属性描述符。 它可以针对数据属性或访问器属性
   value 属性的值，默认为 undefined。

- configurable、属性可否删除 enumerable、可枚举 writable 属性可修改 和 value 设置属性值
- enumerable https://segmentfault.com/a/1190000002953364

```js
// defineProperty动态态描述（getter和setter方法）
var o1 = new Object();
o1.a = "o1a";
o1.b = "b";
// 给对象的当前属性添加getter和setter
Object.defineProperty(o1, "b", {
  enumerable: true,
  configurable: true,
  // writable: true,  // 添加getter和setter时不能设置writable和value
  // value: 'chang1 oa.b',
  //get:function(){}对象方法可以简写
  get() {
    console.log("触发了getter");
    return o1.b; //这里的返回值是o1.b 又会调用get()触发
  },
  set(val) {
    console.log("触发了setter");
    o1.b = val;
  }
});

console.log(o1.b); // 啊哦，出现很多次重复调用getter，我的浏览器卡死了-_-!
```

改进方法：效避免被触发多次，将 getter 和 setter 需要修改的值赋值给外部变量

```js
var o1 = new Object();
o1.a = "o1a";
o1.b = "b";
var bVal = "";
Object.defineProperty(o1, "b", {
  enumerable: true,
  configurable: true,
  get() {
    console.log("触发了getter");
    return bVal;
  },
  set(val) {
    console.log("触发了setter");
    bVal = val;
  }
});

o1.b = 322; // 触发了setter
console.log(o1.b); // 触发了getter 322
```

## 组件的 data 为什么是一个带 return 返回值的函数

原型上的 data 方法是一个函数,两个实例都会指向原型的方法,引用类型, 如果 return 出这个对象, 组件 1 会有自己的 data,组件二也会有自己的 data
{% asset_img datareturn.png  %}
