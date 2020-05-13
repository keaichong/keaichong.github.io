---
title: JQuery常用api一
date: 2019-02-03 22:38:16
tags: JQuery
---

## jQuery 对象和 DOM 对象的区别

- jQuery 对象只能使用 jQuery 对象中提供的属性或方法，不能够使用 DOM 对象中提供的属性或方法
- DOM 对象只能使用 DOM 对象中提供的属性或方法，不能使用 jQuery 对象中提供的属性或方法

## DOM 对象转 jQuery 对象

- 语法： ==\$(dom 对象);==

- 代码：

  ```html
  <div></div>
  <script src="lib/jquery-1.12.4.js"></script>
  <script>
    // 【DOM对象  转  jQuery对象】
    var div = document.querySelector("div");
    // 转换
    var $div = $(div);
    $div.css({
      width: 500,
      height: 500,
      border: "1px solid"
    });
  </script>
  ```
<!-- more -->
## jQuery 对象转 DOM 对象

- 语法：jQuery 对象[索引]; 本质就是从伪数组中取出指定的 dom 对象

- 代码：

  ```html
  <div></div>
  <script>
    // jQuery对象转DOM对象
    var div = $("div")[0];
    div.innerText = "我是文本";
  </script>
  ```

  ## 四.jQuery 操作样式

## 设置样式

- 设置单个样式： jQuery 对象.css(name,value);

- 设置多个样式：

  > jQuery 对象.css({
  >
  > ​ name:value,
  >
  > ​ name:value,
  >
  > ​ name:value,
  >
  > ​ name:value
  >
  > });

- 代码：

  ```html
  <div>我是文字</div>
  <script src="lib/jquery-1.12.4.js"></script>
  <script>
    // 设置单个样式
    $("div").css("width", 500);
    $("div").css("height", 500);
    $("div").css("background", "red");

    // 设置多个样式
    $("div").css({
      border: "10px solid blue",
      background: "pink",
      color: "green"
    });
  </script>
  ```

## 获取样式值

- 语法： jQuery 对象.css('样式属性名');

- 代码：

  ```html
  <style>
    div {
      width: 300px;
      height: 300px;
      position: absolute;
      background-color: red;
      left: 200px;
      top: 100px;
    }
  </style>
  <div></div>
  <script src="lib/jquery-1.12.4.js"></script>
  <script>
    var h = $("div").css("height");
    var l = $("div").css("left");
    console.log(h);
    console.log(l);
  </script>
  ```

## 通过选择器获取 jQuery 对象

### 基本选择器

| 名称       | 用法               | 描述                                 |
| ---------- | ------------------ | :----------------------------------- |
| ID 选择器  | \$('#id')          | 获取指定 ID 的元素                   |
| 类选择器   | \$('.class')       | 获取同一类 class 的元素              |
| 标签选择器 | \$('div')          | 获取同一类标签的所有元素             |
| 并集选择器 | \$('div,p,li')     | 使用逗号分隔，只要符合条件之一就可。 |
| 交集选择器 | \$('div.redClass') | 获取 class 为 redClass 的 div 元素   |

### 层级选择器

| 名称       | 用法          | 描述                                                           |
| ---------- | ------------- | :------------------------------------------------------------- |
| 子代选择器 | \$('ul > li') | 使用>号，获取儿子层级的元素，注意，并不会获取孙子层级的元素    |
| 后代选择器 | \$('ul li')   | 使用空格，代表后代选择器，获取 ul 下的所有 li 元素，包括孙子等 |

### 过滤器选择器

- 这类选择器都带冒号:

| 名称       | 用法                               | 描述                                                                   |
| ---------- | ---------------------------------- | :--------------------------------------------------------------------- |
| :eq(index) | \$('li:eq(2)').css('color', 'red') | 获取到的 li 元素中，选择索引号为 2 的元素，索引号 index**从 0 开始。** |
| :odd       | \$('li:odd').css('color', 'red')   | 获取到的 li 元素中，选择索引号为奇数的元素                             |
| :even      | \$('li:even').css('color', 'red')  | 获取到的 li 元素中，选择索引号为偶数的元素                             |

案例：隔行变色

### 选择器筛选方法

- 筛选选择器的功能与过滤选择器有点类似，但是用法不一样，筛选选择器主要是方法。

| 名称               | 用法                        | 描述                                 |
| ------------------ | --------------------------- | :----------------------------------- |
| children(selector) | \$('ul').children('li')     | 相当于\$('ull > i')，子类选择器      |
| find(selector)     | \$('ul').find('li')         | 相当于\$('ul li'),后代选择器         |
| siblings(selector) | \$('#first').siblings('li') | 查找兄弟节点，不包括自己本身。       |
| parent()           | \$('#first').parent()       | 查找父亲                             |
| eq(index)          | \$('li').eq(2)              | 相当于\$('li:eq(2)'),index 从 0 开始 |
| next()             | \$('li').next()             | 找下一个兄弟                         |
| prev()             | \$('li').prev()             | 找上一次兄弟                         |

## jQuery 操作类名

### 添加类名

- 语法：==jQuery 对象.addClass('类名');==

- 代码：

  ```html
  <div></div>
  <script>
    $("div").addClass("show");
  </script>
  ```

### 移除类名

- 语法：==jQuery 对象.removeClass('类名');== 删除指定的类名

- 语法：jQuery 对象.removeClass(); 不传参数，表示删除所有的类名

- 代码：

  ```html
  <div></div>
  <script>
    $("div").removeClass("show");
  </script>
  ```

  ​

### 检测类名是否存在

- 语法：==jQuery 对象.hasClass('类名');== 返回 true 和 false

- 代码：

  ```html
  <div></div>
  <script>
    var isHas = $("div").hasClass("show");
    console.log(isHas); // false;
  </script>
  ```

  ​

### 类名切换

- 语法：==jQuery 对象.toggleClass('类名');== 若这个类名存在，则会移除该类名。否则添加该类名

- 代码：

  ```html
  <div></div>
  <script>
    $("div").toggleClass("show");
  </script>
  ```

## jQuery 操作标签的属性

### 设置标签的属性

- 语法：jQuery 对象.attr(name,value);

- 代码：

  ```html
  <div></div>
  <script>
    $("div").attr("pid", 10010);
  </script>
  ```

  ​

### 获取标签属性值

- 语法：jQuery 对象.attr(name);

- 代码：

  ```html
  <div></div>
  <script>
    var r = $("div").attr("pid");
  </script>
  ```

### 移除标签的属性

- 语法：removeAttr(name);

- 代码：

  ```html
  <div></div>
  <script>
    $("div").removeAttr("pid");
  </script>
  ```

### prop 方法操作属性

> 针对：selected、checked、disabled

- 获取属性值

  - 语法：\$('input').prop('属性名');

  - 代码：

    ```js
    <input type="checkbox" />
    </script>
      var isC = $('input').prop('checked');
      console.log(isC); // false;
    </script>
    ```

- 设置属性值

  - 语法：\$('input').prop('属性名',值);
  - 代码：
    ```html
    <input type="checkbox" />
    </script>
      $('input').prop('checked',true);
    </script>
    ```

## jQuery 创建元素

- 语法：**`$('<li></li>')`**

## jQuery 追加元素

### 向父元素最后追加

- 语法：新创建 jQuery 对象.appendTo('父元素选择器' 或 父元素 jQuery 对象);

- 语法：父元素 jQuery 对象.apeend(新创建的 jQuery 对象);

- 代码：

  ````html
  <ul>
    <!-- <li>后裔</li> -->
  </ul>
  <script src="lib/jquery-1.12.4.js"></script>
  <script>
    var datas = ["后裔", "安其拉", "鲁班", "小乔", "虞姬"];
    for (var i = 0; i < datas.length; i++) {
      $("<li></li>")
        .text(datas[i])
        .appendTo("ul");
    }
  </script>
  ````

### 向父元素最前面追加

- 语法：新创建 jQuery 对象.prependTo('父元素选择器');

- 语法：父元素 jQuery 对象.prepend(新创建的 jQuery 对象);

- 代码：

  ```html
  <ul>
    <!-- <li>后裔</li> -->
  </ul>
  <script src="lib/jquery-1.12.4.js"></script>
  <script>
    var datas = ["后裔", "安其拉", "鲁班", "小乔", "虞姬"];
    for (var i = 0; i < datas.length; i++) {
      // $('<li></li>')
      // .text(datas[i])
      // .prependTo('ul');

      $("ul").prepend($("<li></li>").text(datas[i]));
    }
  </script>
  ```

## jQuery 删除元素

- 语法：jQuery 对象.remove(); 删谁就让谁调用这个方法

## jQuery 清空元素

- 清空方式 1：==jQuery 对象.empty();== 推荐使用， 清空内部的所有元素及元素相关的事件
- 清空方式 2：jQuery 对象.html(''); 仅仅清空内部的元素，不清清理内中的元素的事件。
