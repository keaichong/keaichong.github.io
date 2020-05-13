---
title: PS切图
date: 2019-06-27 16:14:46
tags:
---

### 切图

1. 选择工具栏矩形选框工具
2. 顶栏样式选择固定大小
3. 选中切图区域后标注辅助线
4. ctrl+c 复制选中图层
5. ctrl+n 新建图层
6. ctrl+v 粘贴图层
7. ctrl+shift+alt+s 保存剪切好的图层到指定位置

## js 原生添加样式

1. document.getElementById("d1").style.cssText = "color:red; font-size:13px;";
2. document.getElementById("myDIV").classList.add("mystyle");

## less 的&用法

1. - p+p 兄弟选择器,某元素后相邻的兄弟元素,p 后面的 p 样式
2.

## startswith 和 endswith

- 定义: startsWith() 方法用于检测字符串是否以指定的子字符串开始。如果是以指定的子字符串开头返回 true，否则 false。startsWith() 方法对大小写敏感。

1. string.startsWith(searchvalue, 开始索引)

```js
let str1 = "file:///C:/Users/iTAze/Desktop/1.html.png";
let str2 = "https://mp.csdn.net/postedit.jpg";
console.log(str1.endsWith(".png")); // true;
console.log(str1.endsWith(".jpg")); // false;
console.log(str2.endsWith(".png")); // false;
console.log(str2.endsWith(".jpg")); // true;
```

## if 后面不加大括号 只执行第一句

  <!-- more -->

## Object.keys()

- Object.keys() 方法会返回一个由一个给定对象的自身可枚举属性组成的数组，数组中属性名的排列顺序和使用 for...in 循环遍历该对象时返回的顺序一致 。如果对象的键-值都不可枚举，那么将返回由键组成的数组。

- Object.keys 返回一个所有元素为字符串的数组，其元素来自于从给定的 object 上面可直接枚举的属性。这些属性的顺序与手动遍历该对象属性时的一致。(不包括方法)

- 如果你只要获取到可枚举属性，查看 Object.keys 或用 for...in 循环（还会获取到原型链上的可枚举属性，不过可以使用 hasOwnProperty()方法过滤掉）。

```js
var obj = { name: "song", age: 20, address: "重庆", post: "844746@qq.com" };
Object.keys(obj);
// ["name", "age", "address", "post"]
var arr = ["a", "b", "c"];
console.log(Object.keys(arr)); // console: ['0', '1', '2']
```

## jQuery 遍历 - is() 方法

- is() 根据选择器、元素或 jQuery 对象来检测匹配元素集合，如果这些元素中至少有一个元素匹配给定的参数，则返回 true。

```html
<ul>
  <li>list <strong>item 1</strong></li>
  <li><span>list item 2</span></li>
  <li>list item 3</li>
</ul>
```

```js
$("ul").click(function(event) {
  var $target = $(event.target);
  if ($target.is("li")) {
    $target.css("background-color", "red");
  }
});
```

## 判断页面是否是微信浏览器打开

```js
var is_weixin = (function() {
  return navigator.userAgent.toLowerCase().indexOf("micromessenger") !== -1;
})();
if (is_weixin) {
  return true;
} else {
  return false;
}
```

## data-\*属性

```
<input id='inp' type="text" name="FirstName" data-id="3" data-name="王二小" data-age="32岁" value="Bill" /><br />

```

## vscode 快捷键

1. 选中一段文字，按 shift+alt+i，可以在每行末尾出现光标
2. 光标放在一个地方，按 ctrl+shift+L 或者 ctrl+f2，可以在页面中出现这个词的不同地方都出现光标。有时候这个快捷键的作用和 f2 重命名变量类似，但是它更加广泛，因为还可以对比如字符串相同的非同一变量或函数类的东西修改。

## vue 计算属性 computed

1. computed 如果依赖了 data 里的数据，当依赖变化就会触发 computed 的更新，前提是 computed 里的值必须要在模板里使用才行,否则也不会触发 computed

## 作用域插槽|带数据的插槽

- 参考 https://segmentfault.com/a/1190000012996217
- 参考优先 https://www.bbsmax.com/A/nAJvP0Xndr/

1. slot-scope='scope' scope 是一个对象

```html
匿名插槽
<slot></slot>
具名插槽
<slot name="up"></slot>
```

1. 作用域插槽，实际上，对比前面两种插槽，我们可以叫它带数据的插槽。作用域插槽要求，在 slot 上面绑定数据。也就是你得写成大概下面这个样子。

```js
<slot name="up" :data="data"></slot>
 export default {
    data: function(){
      return {
        data: ['zhangsan','lisi','wanwu','zhaoliu','tianqi','xiaoba']
      }
    },
}
```

2. 插槽最后显示不显示是看父组件有没有在 child 下面写模板，像下面那样。

```html
<child>
  html模板
</child>
```

## slice 和 concat 对数组的深拷贝

- slice,concat 方法的局限性,slice 和 concat 这两个方法，仅适用于对不包含引用对象的一维数组的深拷贝

```js
//深拷贝不会改变原数组
var arr1 = ["1", "2", "3"];
var arr2 = arr1.slice();
var arr3 = arr1.concat();
arr2[1] = "9";
arr3[1] = "5";
//arr1 = ["1","2","3"];
//arr2 = ["1","9","3"];
//arr3 = ["1","5","3"];
```

## ES6 数组 set 方法去重

- ES6 提供了新的数据结构 Set，它类似于数组，但是成员的值都是唯一的，没有重复的值。Set 本身是一个构造函数，用来生成 Set 数据结构

```js
// 数组去重函数
function unique(array) {
  return Array.from(new Set(array));
}
```

- Set 轻松实现并集，交集，和差集

```js
// set有has方法 返回ture和false
let a = new Set([1,2,3])
let b = new Set([4,3,2])
//并集
let union = new Set([...a,...b]);
// Set{1,2,3,4}
// 交集
let intersect = new Set([...a].filter(x=>b.has(x)))；
//函数内容只有一行可以省略return
//Set{2，3}
// 差集
let difference = new Set([...a].filter(x=>！b.has(x)))；
//Set{1}
//
```

## 获取表单中所有具有 name 属性的值

- 获取表单中所有具有 name 属性的值 包括
- var formData = \$('#edit_form').serialize();

## js 判断字符串长度

```js
String.prototype.gblen = function() {
  var len = 0;
  for (var i = 0; i < this.length; i++) {
    if (this.charCodeAt(i) > 127 || this.charCodeAt(i) == 94) {
      len += 2;
    } else {
      len++;
    }
  }
  return len;
};
```

## 表单序列化

- 表单序列化的三种方式
- https://www.cnblogs.com/tanzq/p/9857213.html

```json
<script type="text/javascript">
$(document).ready(function(){
  $("button").click(function(){
    $("div").text($("form").serialize());
  });
});
</script>
<form action="">
First name: <input type="text" name="FirstName" value="Bill" /><br />
Last name: <input type="text" name="LastName" value="Gates" /><br />
</form>
//最终序列化出的结果就是:FirstName=Bill&LastName=Gates
```

## js 选中 select 下拉框的值

```html
<select name="select1" id="select1">
  <option id="pg" value="pg" name="pg">苹果</option>
  <option value="xj" name="xj">香蕉</option>
  <option value="jz" name="jz">橘子</option>
  <option value="xg" name="xg">西瓜</option>
</select>
```

```js
//获取选择框select1
var select1 = document.getElementById("select1");

//选择框选中的value
//var select1_value = select1.value;

//select1的改变事件,输出选中的选项的value
select1.onchange = function() {
  console.log(select1.value);
};
//机械获取选择框里的选项的value
var option_value1 = select1.options[0].value; //"pg"
var option_value2 = select1.options[1].value; //"xj"
var option_value3 = select1.options[2].value; //"jz"
var option_value4 = select1.options[3].value; //"xg"

//获取当前被选中选项的index值
var Index = select1.selectedIndex; //比如选中西瓜,select1.selectedIndex=3

//拿到选中项options的value
myselect.options[select1.selectedIndex].value;

//拿到选中项options的text：
select1.options[select1.selectedIndex].text;
```

## 文件图片上传显示

- https://www.cnblogs.com/gr07/p/9628523.html

```html
<div>
  <form id="form1" enctype="multipart/form-data" method="post" name="fileinfo">
    <input
      type="file"
      id="file"
      @change="sendImg"
      multiple
      accept="image/*"
    /><br />
  </form>
  <button>上传图片</button>
  <img src="" alt="" />
</div>
```

```js
var btn = document.getElementsByTagName("button")[0];
var img = document.getElementsByTagName("img")[0];
var form1 = document.getElementById("form1");
var file = document.getElementById("file");
//文件发生改变时候触发
file.onchange = function(event) {
  let file = event.target.files[0];
  console.log(file, "file");
  let reader = new FileReader();
  console.log(reader);
  // 调用reader.readAsDataURL()方法，把图片转成base64(必须)
  reader.readAsDataURL(file);
  // 监听reader对象的onload事件，当图片加载完成时，把base64编码賦值给预览图片
  reader.onload = function() {
    img.src = this.result;
  };
};
```

## 聊天对话信息展示用 pre 标签包裹

1. pre 这是预格式文本。它保留空格和换行。
2. pre 标签很适合显示计算机代码：

for i = 1 to 10
print i
next i

## 父组件获取子组件 data

```js
this.$refs.form.age;
```

## url 地址栏路径的问题

- E:\前端与移动开发基础\就业班 node.js\09-nodejs\视频\23\_路径的问题

## 谷歌 f12 看不到 vue 的 devtools 图标

1. 先刷新 f5,在按 f12
2. 看一下引用的 vue 是 vue.js 还是 vue.min.js , vue.min.js 是生产下用的， 所以 devtools 是没有用

## forEach 和 map 比较

1. 区别：map 的回调函数中支持 return 返回值；return 的是啥，相当于把数组中的这一项变为啥（并不影响原来的数组，只是相当于把原数组克隆一份，把克隆的这一份的数组中的对应项改变了）
2. map 速度比 foreach 快

3. map 会返回一个新数组，不对原数组产生影响,foreach 不会产生新数组，

4. map 因为返回数组所以可以链式操作，foreach 不能

```js
var arr = [1, 2, 3, 4, 5];

var r = arr.map((v, i) => {
  return v * 2;
});
//r=[2,4,5,8,10] arr= [1,2,3,4,5]
//把map换为forEach 因为foreach没有返回值所以把undefined赋值给了r
```

## 块级元素居中显示 css3 属性

1. 使用 css3 样式属性 display:flex 设定水平垂直居中，父元素样式属性 display:flex;子元素使用 margin:auto;未知子元素高度的时候依然可以使用。
2. 一般 chrome 和火狐都能很好地支持。ie 不支持

## bit 位和 Byte 字节

1. bit(位) 一个数字 0 或者一个数字 1;代表一位
2. Byte(字节) 1 Byte = 8bit ;是数据存储的最小单位

- 假设我们的宽带是 100Mbps, 第二个 b 就是 bit;但是下载网速是 12.5MB/S; 第二个 B 代表的 Byte;所以要用 100%8 才会是我们下载的理论大小速度

## java

1. jvm java 虚拟机
2. jre java 运行环境(封装有 jvm) 运行 java 代码
3. jdk java 工具包 (封装有 jre) 开发 java 代码

## url(image/1.png?v=1) a.css?v=f02bc2

- 向图片传参本身不会对图片有任何影响,一般是为了避免缓存才这么干，可能是由于这张图片经常更换，但又必须实时显示的缘故
- css 文件后缀传参 利用 数据摘要要算法 对文件求摘要信息，摘要信息与文件内容一一对应，就有了一种可以精确到单个文件粒度的缓存控制依据了 (摘要算法又称哈希算法，它表示输入任意长度的数据，输出固定长度的数据，相同的输入数据始终得到相同的输出，不同的输入数据尽量得到不同的输出。)

## js 对时间进行排序

```js
const arr = [
  { id: 1, value: "value1", date: "2018-08-08", time: "15:27:17" },
  { id: 2, value: "value2", date: "2018-08-09", time: "12:27:17" },
  { id: 3, value: "value3", date: "2018-08-10", time: "17:27:17" },
  { id: 4, value: "value4", date: "2018-08-10", time: "01:27:17" },
  { id: 5, value: "value5", date: "2018-08-10", time: "09:27:17" },
  { id: 6, value: "value6", date: "2018-08-10", time: "23:27:17" },
  { id: 7, value: "value7", date: "2018-08-10", time: "16:27:17" },
  { id: 8, value: "value8", date: "2018-08-11", time: "10:27:17" }
];
//time: "2019-06-13" 这种日期格式也可以升序降序
// 升序
arr.sort(
  (a, b) => a.date.localeCompare(b.date) || a.time.localeCompare(b.time)
);
// 降序
arr.sort(
  (a, b) => b.date.localeCompare(a.date) || b.time.localeCompare(a.time)
);
console.log(arr);
```

## 取消事件的方法

1. event.preventDefault()
2. event.stopPropagation()

- 这两种是在 JS 中的常用取消事件的方法，但是其实还有一种用纯 css 就能实现取消事件响应的方法，pointer-events，使用起来更加简单，它可以：

1. 阻止用户的点击动作产生任何效果

2. 阻止缺省鼠标指针的显示

3. 阻止 CSS 里的 hover 和 active 状态的变化触发事件

4. 阻止 JavaScript 点击动作触发的事件

## 内存泄漏

- http://www.ruanyifeng.com/blog/2017/04/memory-leak.html

```js
var arr = [1, 2, 3, 4];
// "引用计数"（reference counting）：语言引擎有一张"引用表"，保存了内存里面所有的资源（通常是各种值）的引用次数。如果一个值的引用次数是0，就表示这个值不再用到了，因此可以将这块内存释放。
//数组[1,2,3,4]是一个值,会占用内存,arr是对这个数组的引用,因为引用次数为1,所以不会被系统释放掉,可以增加一行代码,接触对这个数值的引用
var arr = null;
//arr重置为null，就解除了对[1, 2, 3, 4]的引用，引用次数变成了0，内存就可以释放出来了。
//因此，并不是说有了垃圾回收机制，程序员就轻松了。你还是需要关注内存占用：那些很占空间的值，一旦不再用到，你必须检查是否还存在对它们的引用。如果是的话，就必须手动解除引用。
```

## 非对称加密

- 加密和解密需要两把钥匙 一把公钥 一把私钥
- 公钥是公开的，任何人都可以获取。私钥是保密的，只有拥有者才能使用。他人使用你的公钥加密信息，然后发送给你，你用私钥解密，取出信息。反过来，你也可以用私钥加密信息，别人用你的公钥解开，从而证明这个信息确实是你发出的，且未被篡改，这叫做数字签名

## vue 三元运算符

- gender: userInfo.gender == 'F' ? '2' : userInfo.gender == 'M' ? '1' : '0', 可以判断男女其他

## vue 钩子函数 updated 触发条件

- 由于数据更改导致的虚拟 DOM 重新渲染和打补丁，在这之后会调用该钩子。
- 无论是组件本身的数据变更，还是从父组件接收到的 props 或者从 vuex 里面拿到的数据有变更，都会触发虚拟 DOM 重新渲染和打补丁，并在之后调用 updated。

## div 居中三种方法

```css
div {
            width: 100px;
            height: 100px;
            background: red;
            position: absolute;
            top: 0;
            left: 0;
            bottom: 0;
            right: 0;
            margin: auto;
        }
div {
            width: 100px;
            height: 100px;
            background: red;
            position: absolute;
            top: 50%;
            left: 50%;
            margin-top: -50px;
            margin-left: -50px;
    }
父元素display:flex
子元素margin:auto 子元素居中
```
