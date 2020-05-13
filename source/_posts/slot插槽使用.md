---
title: slot插槽使用
date: 2019-08-12 10:31:20
tags: vue
---
- https://segmentfault.com/a/1190000012996217
## 子组件 Child

```html
<template>
  <div>
    <h3>我是子组件child</h3>
    <!-- // 作用域插槽 -->
    <slot :aa="data" :bb="shuju" cc="这是一首简单的歌"> </slot>
  </div>
</template>

<script>
  export default {
    data() {
      return {};
    },
    // props的值来源于父组件
    props: {
      data: {
        type: Array,
        default: "无数据",
        required: true
      },
      shuju: {
        type: Array,
        default: "无数据",
        required: true
      }
    }
  };
</script>

<style></style>
```
<!-- more -->
## 父组件使用

```html
<template>
  <div id="demo">
    <h2>我是父组件</h2>

    <Child :data="dataprop" :shuju="shuju1">
      <template slot-scope="scope">
        <!-- <template v-slot="scope"> -->
        <!--vue2.6以上语法 v-slot:default="scope" -->
        <!-- scope是一个对象 对象的属性是child组件中<slot>绑定的属性 对象的值是<slot>绑定的值 -->
        <div>下面是scope内容:</div>
        <div>{{scope}}</div>
        <ul>
          <li v-for="(item,index) in scope.aa" :key="index">姓名:{{item}}</li>
        </ul>
        <h3 v-for="(item,index) in scope.bb" :key="index">
          姓名:{{item.name}}-年龄:{{item.age}}
        </h3>
        <h3>歌曲:{{scope.cc}}</h3>
      </template>
    </Child>
  </div>
</template>

<script>
  import Child from "./child.vue";
  export default {
    data() {
      return {
        dataprop: ["zhangsan", "lisi", "wanwu", "zhaoliu", "tianqi", "xiaoba"],
        shuju1: [
          {
            name: "科比",
            age: "29",
            sex: "man"
          },
          {
            name: "欧文",
            age: "30",
            sex: "woman"
          }
        ]
      };
    },
    components: {
      Child
    }
  };
</script>
<style></style>
```
## 页面显示内容

```json
我是父组件
我是子组件child
下面是scope内容:
{ "aa": [ "zhangsan", "lisi", "wanwu", "zhaoliu", "tianqi", "xiaoba" ], "bb": [ { "name": "科比", "age": "29", "sex": "man" }, { "name": "欧文", "age": "30", "sex": "woman" } ], "cc": "这是一首简单的歌" }
姓名:zhangsan
姓名:lisi
姓名:wanwu
姓名:zhaoliu
姓名:tianqi
姓名:xiaoba
姓名:科比-年龄:29
姓名:欧文-年龄:30
歌曲:这是一首简单的歌

```
