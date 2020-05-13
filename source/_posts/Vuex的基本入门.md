---
title: Vuex的基本入门
date: 2019-02-26 00:17:05
tags: vue
---

## vuex 流程
>vuex就像一个无形的仓库，公共的状态我们会抽离出来放进里面

1. state->声明数据(组件可以用,响应式)
2. actions->和后台交互(ajax 请求)->返回新结果
3. mutations->修改 state,接收 actions 传递的结果
4. dispatch：含有异步操作，例如向后台提交数据，写法： this.$store.dispatch('action方法名',值)
5. commit：同步操作，写法：this.$store.commit('mutations方法名',值)

```shell
state:声明数据(响应式数据)->组件的computed

getters:声明复杂数据将state中的某个状态进行过滤然后获取新的状态->组件的computed

mutations:修改state的方法(同步方法)->组件的methods   

actions:异步操作获取新数据(和后台交互->ajax) ->通过commit的方法把新数据交给mutations->组件的methods

modules顾名思义，就是当用这个容器来装这些状态还是显得混乱的时候，我们就可以把容器分成几块，把状态和管理规则分类来装。这和我们创建js模块是一个目的，让代码结构更清晰。
```

> https://segmentfault.com/a/1190000015782272

<!-- more -->

```js
  // actions:方法->异步
  actions: {
    fnac1(context) {
      // context就是仓库
      // 异步代码
      setTimeout(() => {
        const numNew = 200
        // 在异步有结果的位置,把结果提交给mutations的方法
        context.commit('setNum', numNew)
      }, 1000)
    }
  }
```

> app.vue

```js
methods:{

    fn2(){

        this.$store.dispatch("fnac1")
        ...mapActions(["fnac2"])
    }
}
```
