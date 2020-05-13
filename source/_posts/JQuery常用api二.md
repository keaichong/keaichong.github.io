---
title: JQuery常用api二
date: 2019-02-03 22:52:51
tags: JQuery
---

## 核心知识点

- jQuery 操作元素的尺寸
- jQuery 操作元素的位置
- jQuery 事件操作（注册、移除、事件委托、触发）

## jQuery 操作元素的尺寸

### width 和 height 方法

> 操作的大小仅仅是内容部分

- 设置：

  - 语法：jQuery 对象.width(数字);

- 获取：

  - 语法：jQuery 对象.width();

- 代码：

  ```javascript
  // 获取
  var w = $("div").width();
  console.log(w);
  // 设置
  $("div").width(300);
  ```

### innerWidth 和 innerHeight 方法

> 操作的大小是内容部分 + padding
<!-- more -->
- 设置：

  - 语法：jQuery 对象.innerWidth(数字);

- 获取：

  - 语法：jQuery 对象.innerWidth();

- 代码：

  ```javascript
  // 获取
  var w = $("div").innerWidth();
  console.log(w);
  // 设置
  $("div").innerWidth(300);
  ```

### outerWidth 和 outerHeight 方法

> 操作的大小是内容部分 + padding + border

- 设置：

  - 语法：jQuery 对象.outerWidth(数字);

- 获取：

  - 语法：jQuery 对象.outerWidth();

- ```javascript
  // 获取
  var w = $("div").outerWidth();
  console.log(w);
  // 设置
  $("div").outerWidth(300);
  ```

## jQuery 操作元素的位置

### 获取元素距离文档的位置

- 语法：jQuery 对象.offset(); 返回一个对象，对象中包含了元素的位置

- 注意：

  > offset()方法获取的元素的位置，永远参照文档。和定位没有关系

- 代码：

  ````javascript
  var o = $(".s").offset();
  console.log(o);
  console.log(o.top);
  ````

### 获取元素距离上级定位元素的位置

- 语法：jQuery 对象.position(); 返回的一个对象，对象中包含了元素的位置

- 注意：

  > position()方法获取的元素的位置,参照最近的定位元素（和定位有关系）

- 代码：

  ```javascript
  var o = $(".s").position();
  console.log(o);
  console.log(o.top);
  ```

### 操作卷去的页面间距

- 获取

  - 语法：jQuery 对象.scrollTop(); 返回数字

- 设置

  - 语法：jQuery 对象.scrollTop(数字);

- 代码：

  ```javascript
  $("div").scroll(function() {
    // 获取被卷起的间距
    var v = $(this).scrollTop();
    console.log(v);
  });

  $("button").click(function() {
    // 设置卷起的间距
    $("div").scrollTop(0);
  });
  ```

## jQuery 事件操作

### 简单方式注册事件

- 语法：jQuery 对象.事件名(事件处理程序);

  ![](media/01.png)

  ​

### on 方法注册事件

- 注册简单事件语法：jQuery 对象.on('事件名',事件处理程序);

- 事件委托的实现：jQuery 对象.on('事件名','选择器',事件处理程序);

  - 选择器：子孙元素
  - 注意：在事件处理程序中，this 代表的是子孙元素（所点最先触发的）

- 代码：

  ```javascript
  // 注册简单的事件
  $("button").on("click", function() {
    alert(1);
  });

  // 【JQ方式实现事件委托-把li委托给ul】
  $("ul").on("click", "li", function() {
    // this 是谁？ 当前点击的li
    console.log(this);
    alert($(this).text());
  });
  ```

### off 方法移除事件

- 解绑简单的事件：jQuery 对象.off('click',事件处理程序名称)

- 解绑事件委托注册的事件：jQuery 对象.off('click',‘选择器’,事件处理程序名称)

- 代码：

  ```javascript
  // 解绑按钮的事件处理程序：fn1和fn2
  $("button").off("click", fn1);
  $("button").off("click", fn2);

  // 解绑通过事件委托给p注册的事件处理程序 fn2
  $("div").off("click", "p", fn2);
  ```

### 触发事件

- 语法：jQuery 对象.trigger('事件名');

- 代码：

  ```javascript
  $("button").trigger("click");
  ```

### 事件对象

> 如何获取事件对象？
>
> ​ 事件处理程序的第一个形参-e

- 鼠标事件对象相关的属性
  - 事件对象.clientX/Y 参照浏览器
  - 事件对象.pageX/Y 参照文档
  - 事件对象.offsetX/Y 参照元素
- 键盘事件对象相关的属性
  - 事件对象.keyCode 返回键码数字
  - 事件对象.alt/shift/ctrlKey 返回是布尔值。 检测是否按下（true）
- 公共的属性或方法
  - 属性
    - 事件对象.target;
  - 方法：
    - 事件对象.preventDefault(); 阻止默认行为
    - 事件对象.stopPropagation(); 阻止事件冒泡
