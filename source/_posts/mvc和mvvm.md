---
title: mvc和mvvm
date: 2019-02-04 01:55:02
tags:
---

{% asset_img 01.MVC和MVVM的关系图解.png  MVC和MVVM的关系图解%}

<!-- more -->

{% asset_img vue.png  vue图解%}

## Vue-项目-重点

### day07-项目-重点

#### 01-项目-准备-vue-cli 创建项目结构

1. 来到项目所希望的目录->打开 cmd

2. vue init webpack 项目名

   1. 是否安装 vue-router -> Y
   2. 是否 use ESLint -> Y
   3. 编译方式 -> for most users
   4. unit tests->N
   5. e2e -> N
   6. npm/yarn -> npm

3. cd 项目目录

4. npm run dev 启动开发模式

   > 注意: 默认不会打开浏览器

#### 02-项目-准备-项目目录说明

1. .eslintignore -> ESLint 检查 js 代码排除忽略文件
2. eslintrc-> ESLint 配置文件
3. .gitignore -> git 排除忽略文件
4. build/ -> webpack 打包(src)的产物
5. conf/ -> 配置服务器 index.js autoOpenBrowser: true, -> npm run dev
6. src/main.js 和之前不一样 之前是 render-> 现在是 template 和 components

#### 03-项目-准备-代码规范-自定义指令-lintfix

> ESlint 自动检查 js 代码规范
>
> 一键调整代码规范

1. package.json->scripts->自定义指令

   > "lintfix": "eslint --ext .js,.vue src --fix",

2. npm run dev 让配置文件生效

3. npm run lintfix (对于未使用的变量 不能修复)

4. npm run dev

> 建议: 先感受 ESLint , 项目第三天 教如何禁用 eslint

#### 04-项目-准备-element-ui-文档分析

> vue 使用第三方 UI 库 饿了么 element-ui
>
> vuePC 项目:element-ui / iView
>
> vue 移动端项目: mint-ui

#### 05-项目-准备-element-ui-安装-引入

> npm i element-ui

`main.js`

```js
import ElementUI from "element-ui";
import "element-ui/lib/theme-chalk/index.css";
Vue.use(ElementUI);
```

> 在所有的.vue 文件 template 中就可以使用组件了!

#### 06-项目-准备-项目模板简化-调整

> 简化代码

#### 07-项目-准备-git-版本控制

> git 管理项目代码
>
> gitbash-> git 指令可以任何 cmd 中执行->git 报错->git 是无效指令->
>
> 1. 找到 git 软件安装路径 bin
> 2. 找到计算机管理/属性//环境变量 path -> 修改编辑 path -> 把上一步路径放在 path 里面
> 3. 可以在任意 cmd 中 git 指令
> 4. 重启电脑
>
> [网址](https://blog.csdn.net/shanshan_blog/article/details/53645358)
>
> 继续 gitbash 软件

```shell
git init
git add .
git commit -m "注释"
// github新建仓库
// 关联仓库
git push -u origin master
```

> 后续再 git

```shell
git add .
git commit -m "完成了功能1-登录"
git push
```

#### 08-项目-准备-git-分支管理

> 前提 git 管理代码/协同开发

> 项目 2 个人
>
> A 人->新建子分支 login->编写代码 ->git add. commit->把代码 A 合并到主分支 master
>
> B 人->新建子分支 home->编写代码 ->git add. commit->把代码 B 合并到主分支 master
>
> 在 master 主分支->git push

```shell
// 查看分支
git branch
// 新建分支并且切换到分支
git checkout -b 分支dev-login
// git branch
// 结果: 接下来所有的操作(代码编写/add/commit)在当前的dev-login进行操作的->开发login功能
```

#### 09-项目-登录-新建分支-login 组件-配置路由

> 当前开发 login 登录 当前分支 dev-login

1. 新建 login.vue 组件
2. 配置路由 router.js

```shell
// 在子分支完成小功能后,在子分支上
git add .
git commit -m "注释"
// 功能完成
// 切换到master
git checkout master
// 把dev-login分支写的代码合并到master
// git branch
git merge dev-login
// 在master主分支推送
git push
```

#### 10-项目-登录-引入表单组件

> 切换回 dev-login

1. 引入 el-form
2. 添加类名
3. 提供组件要用的数据

```shell
git branch
git status
git add .
git commit -m "引入登录组件"
```

> 合并代码 不需要每次都做,可以完成一大功能 最后一起合并和推送

#### 11-项目-登录-样式调整

```css
.login-wrap {
  /* 注意: 百分比布局 父元素height */
  height: 100%;
  background-color: #324152;
  display: flex;
  justify-content: center;
  align-items: center;
}
.login-form {
  background-color: #ffffff;
  border-radius: 5px;
  /* 开发 */
  width: 400px;
  padding: 30px;
}
.login-btn {
  width: 100%;
}
```

> 1. 百分比布局
>    1. base.css html,body{height:100%}
>    2. App.vue #app{height:100%}
> 2. vue 项目重点不是 css 只要能写出来就可以

#### 12-项目-登录-axios 插件

1. npm i axios
2. main.js 挂载原型 axios
3. 配置 baseUrl
4. this.\$http 发送请求了

#### 13-项目-登录-发送登录请求

```js
this.$http
  .post(`login`, this.formdata)
  .then(res => {
    console.log(2);

    console.log(res);
  })
  .catch(err => {
    console.log(err);
  });
```

> 服务器 cmd 卡死-> 回车->激活它

#### 14-项目-登录-引入提示框组件

```js
this.$http.post(`login`, this.formdata).then(res => {
  console.log(res);
  const {
    data: {
      data,
      meta: { msg, status }
    }
  } = res;
  if (status === 200) {
    console.log("success----");
  } else {
    // 提示框 -> UI
    this.$message.error(msg);
  }
});
```

> 提示: 对象解构赋值

#### 15-项目-登录-登录成功-进入 home 组件

> 登录成功->渲染 home.vue

#### 16-项目-登录-简化登录请求代码-async 和 await

> 目的:让异步代码看起来像同步,好处没有函数嵌套

```js
const res = await this.$http.post(`login`, this.formdata);
```

1. 找异步代码
2. 在异步代码前面加 await 同时接受异步的结果
3. 在异步代码外层最近的函数前面加 async

#### 17-项目-登录-保存 token 值

> 将来在其他组件中使用用户的数据信息中 token 数据->保存 token->
>
> login.vue 有了 token -> xxoo.vue 使用 token->
>
> A 页面有数据 a -> B 页面使用 a->
>
> 要把 token 数据永久存储-> cookie/session/sessionStorage/localStorage 等->
>
> 使用 Html5 新特性 localStorage 保存 token

```js
// 把正确的用户的token保存起来
// 存值
localStorage.setItem("token", token);
// 取值
// const aa = localStorage.getItem("token");
// console.log(aa);
```

> 浏览器调试->application->cookie/localStorage 保存的数据

#### 18-项目-首页-布局容器-使用-样式调整

> 引入布局容器

```html
<el-container class="container">
  <el-header>Header</el-header>
  <el-container>
    <el-aside class="aside" width="200px">Aside</el-aside>
    <el-main class="main">Main</el-main>
  </el-container>
</el-container>
```

> 调整样式

```css
.container {
  height: 100%;
  background-color: red;
}
.aside {
  background-color: yellow;
}

.main {
  background-color: green;
}
```

#### 19-项目-首页-头部-样式调整

> 引入 layout 布局(24 份)
>
> el-row 一行
>
> el-col 一列

```html
<el-row>
  <el-col :span="4">
    <img src="@/assets/logo.png" alt="图片加载失败" />
  </el-col>
  <el-col :span="19" class="middle">
    <h2>电商后台管理系统</h2>
  </el-col>
  <el-col :span="1">
    <a href="#" class="logout">退出</a>
  </el-col>
</el-row>
```

#### 20-项目-合并代码-登录

```shell
// 子分支
git add .
git commit -m ""
// 切到主分支
git checkout master
// 合并代码
git merge dev-login
// 在master写代码
git status
git add .
git commit -m "test"
// 推送
git push
```

> 仓库地址链接
>
> 1. 下载
> 2. 使用 git 指令克隆项目仓库 git clone 项目网址https://github.com/LL-1214/shopmanager64.git

### day08-项目-重点

#### 01-项目-首页-侧边栏-导航组件-文档

> el-menu

1. router : 点击时 path 的值 index 值
2. unique-opened 控制是否只有一个子菜单打开
   > el-submenu 子菜单

#### 02-项目-首页-侧边栏-引入导航组件-调整

```html
<el-menu
  :unique-opened="true"
  :router="true"
  default-active="2"
  class="el-menu-vertical-demo"
>
</el-menu>
```

#### 03-项目-首页-进入首页的权限验证

> 必须先登录,才显示 home.vue

```js
beforeMount() {
    if (!localStorage.getItem("token")) {
      this.$router.push({
        name: "login"
      });
      this.$message.warning("请先登录");
    }
  },
```

#### 04-项目-首页-头部-退出功能

```js
// 退出
    handleLoginout() {
      // 1. 清除token
      localStorage.clear();
      // 2. 来到登录
      this.$router.push({
        name: "login"
      });
      // 3. 提示
      this.$message.warning("退出成功");
    }

```

#### 05-项目-首页-合并分支-新建用户分支

```shell
git checkout -b dev-users
git checkout master
// 复习
// 合并分支
git merge 分支名
```

#### 06-项目-用户管理-用户列表-新建组件-路由配置

> 嵌套路由
> 提供单独的 router-view
> users.vue 是在 home.vue 里面显示的

#### 07-项目-用户管理-用户列表-面包屑和搜索框

> 面包屑

```html
<el-breadcrumb separator-class="el-icon-arrow-right">
  <el-breadcrumb-item :to="{ path: '/' }">首页</el-breadcrumb-item>
  <!-- 首页/用户管理/用户列表 -->
  <el-breadcrumb-item>用户管理</el-breadcrumb-item>
  <el-breadcrumb-item>用户列表</el-breadcrumb-item>
</el-breadcrumb>
```

> el-card 带默认样式 div
> el-row 行>el-col 列

#### 08-项目-用户管理-用户列表-引入表格组件

```html
<el-table :data="tableData" style="width: 100%">
  <el-table-column prop="date" label="日期" width="180"></el-table-column>
  <el-table-column prop="name" label="姓名" width="180"></el-table-column>
  <el-table-column prop="address" label="地址"></el-table-column>
</el-table>
```

> el-table 表格 data 绑定数据[]
> el-table-column 控制的是列

1. label 控制的是当前列的表头
2. prop 控制的是当前列单元格的数据,prop 的值来源于外层 data 绑定的数据 tableData 数组中对象的 key 名

#### 09-项目-用户管理-用户列表-表头处理

```html
<el-table :data="list" style="width: 100%">
  <el-table-column prop="name" label="#" width="80"></el-table-column>
  <el-table-column prop="name" label="姓名" width="120"></el-table-column>
  <el-table-column prop="name" label="邮箱" width="140"></el-table-column>
  <el-table-column prop="name" label="电话" width="140"></el-table-column>
  <el-table-column prop="name" label="创建日期" width="140"></el-table-column>
  <el-table-column prop="name" label="用户状态" width="140"></el-table-column>
  <el-table-column prop="name" label="操作" width="200"></el-table-column>
</el-table>
```

#### 10-项目-用户管理-用户列表-请求数据

> 获取表格的数据

```js

 async getTableData() {
      // 除了登录请求.其他所有请求都需要授权->
      // 在发送请求之前,先设置请求头{Authorization:token值}
      // 设置请求头headers -> 发送请求用的是axios->找axiosAPI有没有可以设置请求头->看文档
      // {
      //   ContentType:text/html,
      //   Authorization:?
      // }

      const AUTH_TOKEN = localStorage.getItem("token");
      this.$http.defaults.headers.common["Authorization"] = AUTH_TOKEN;

      const res = await this.$http.get(
        `users?query=${this.query}&pagenum=${this.pagenum}&pagesize=${
          this.pagesize
        }`
      );
      console.log(res);
    }

```

> 接口说明,需要授权 API->除了登录接口,其他所有接口都需要授权,也就是设置头部

#### 11-项目-用户管理-用户列表-渲染数据-一般数据

> 单元格的数据有 2 个不同情况

1. 直接就是 prop 属性值的值 比如 prop="id"
2. 单元格内容不是 prop 的值?

```html
<el-table-column prop="id" label="#" width="80"></el-table-column>
<el-table-column prop="username" label="姓名" width="120"></el-table-column>
<el-table-column prop="email" label="邮箱" width="140"></el-table-column>
<el-table-column prop="mobile" label="电话" width="140"></el-table-column>
<el-table-column
  prop="create_time"
  label="创建日期"
  width="140"
></el-table-column>
```

#### 12-项目-用户管理-用户列表-渲染数据-日期格式处理

1. 全局过滤器
2. 使用过滤器

```html
<el-table-column label="创建日期" width="140">
  <template slot-scope="scope"
    >{scope.row.create_time | fmtdate}</template
  >
</el-table-column>
```

> 前提:当单元格内容不是 prop 控制的

1. 给单元格内容外层加 template
2. 设置 template 的属性 slot-scope="scope"
3. 在单元格内部通过 scope.row.属性 取值
   > 注意: 固定写法, row 固定, "scope"可以随便写

#### 13-项目-用户管理-用户列表-渲染数据-用户状态开关

```html
<el-table-column label="用户状态" width="140">
  <template slot-scope="scope">
    <el-switch
      v-model="scope.row.mg_state"
      active-color="#13ce66"
      inactive-color="#ff4949"
    ></el-switch>
  </template>
</el-table-column>
```

> 和创建日期的处理是一样的情况

1. 加 template
2. slot-scope
3. 使用 scope.row.属性

#### 14-项目-用户管理-用户列表-渲染数据-操作

> 单元格内容不是 prop 的值的值

```html
<el-table-column label="操作" width="200">
  <tempalte slot-scope="scope">
    <el-button
      type="primary"
      icon="el-icon-edit"
      circle
      size="mini"
      plain
    ></el-button>
    <el-button
      type="danger"
      icon="el-icon-delete"
      circle
      size="mini"
      plain
    ></el-button>
    <el-button
      type="success"
      icon="el-icon-check"
      circle
      size="mini"
      plain
    ></el-button>
  </tempalte>
</el-table-column>
```

#### 15-项目-用户管理-用户列表-分页组件-文档-引入

```html
<!-- 分页
    @size-change 每页条数改变时
    @current-change 页码改变时 (当前1页 点击2页 )
    current-page 当前显示第几页 页码
    page-sizes 每页条数的不同情况的数组
    layout 附加功能
    total 一共数据的条数
    -->
<el-pagination
  @size-change="handleSizeChange"
  @current-change="handleCurrentChange"
  :current-page="currentPage4"
  :page-sizes="[100, 200, 300, 400]"
  :page-size="100"
  layout="total, sizes, prev, pager, next, jumper"
  :total="400"
></el-pagination>
```

#### 16-项目-用户管理-用户列表-分页组件-配置数据

```html
<el-pagination
  class="page"
  @size-change="handleSizeChange"
  @current-change="handleCurrentChange"
  :current-page="pagenum"
  :page-sizes="[2, 4,6,8]"
  :page-size="2"
  layout="total, sizes, prev, pager, next, jumper"
  :total="total"
></el-pagination>
```

> total 后台已经返回

#### 17-项目-用户管理-用户列表-分页组件-分页请求

1. 点击页码-> 按照新页码发送请求
2. 点击每页条数 -> 按照新的 pagesize 发送请求

```js

handleSizeChange(val) {
      console.log(`每页 ${val} 条`);

      // 按照新pagesize发送请求
      this.pagenum = 1;

      this.pagesize = val;
      this.getTableData();
    },
    // 当前2页 -> 点击3 ->触发下面的方法 ->val = 3
    handleCurrentChange(val) {
      console.log(`当前页: ${val}`);
      // 按照新页码发送请求
      this.pagenum = val;
      // this.pagemnum = 1 this.pagesize=2 发送请求
      // this.pagenum=3 this.pagesize=2 发送请求
      this.getTableData();
    },
```

> 测试,this.pagenum=1

#### 18-项目-用户管理-用户列表-搜索用户

```js

 // 搜索-清空时获取所有用户
    getAllUsers() {
      this.getTableData();
    },
    // 搜索用户
    searchUser() {
      this.pagenum = 1;
      // 按照query关键字搜索
      // query="admin"
      this.getTableData();
    },
```

> 不要忘记重置 this.pagenum=1

#### 19-项目-用户管理-用户列表-添加用户-显示对话框

```html
<el-dialog title="添加用户" :visible.sync="dialogFormVisibleAdd">
  <!-- 表单 -->
  <el-form label-position="left" label-width="80px" :model="formdata">
    <el-form-item label="用户名">
      <el-input v-model="formdata.username"></el-input>
    </el-form-item>
    <el-form-item label="密码">
      <el-input v-model="formdata.password"></el-input>
    </el-form-item>
    <el-form-item label="邮箱">
      <el-input v-model="formdata.email"></el-input>
    </el-form-item>
    <el-form-item label="电话">
      <el-input v-model="formdata.mobile"></el-input>
    </el-form-item>
  </el-form>

  <div slot="footer" class="dialog-footer">
    <el-button @click="dialogFormVisibleAdd = false">取 消</el-button>
    <el-button type="primary" @click="dialogFormVisibleAdd = false"
      >确 定</el-button
    >
  </div>
</el-dialog>
```

1. 点击按钮->改 bool
2. 引入对话框
3. 配置数据(对话框和 form 数据)
   > 表单数据依据发送 post 请求体

## Vue-项目-重点

### day07-项目-重点

#### 01-项目-准备-vue-cli 创建项目结构

1. 来到项目期望的目录->打开 cmd
2. vue init webpack 项目名
   1. 是否使用路由 -> Y
   2. 是否使用 ESLint(检查代码规范) -> Y
   3. for most users
3. cd 项目名
4. npm run dev(默认不会打开浏览器)

#### 02-项目-准备-项目目录说明

1. build/ webpack 打包的产物/结果
2. config/ 配置服务器 ->
   1. index.js -> autoOpenBrowser: true, -> npm run dev
3. .eslintrc:配置 ESLint
4. .eslintignore: ESLint 忽略文件
5. index.html -> 注意: 不需要引入 build.js

#### 03-项目-准备-代码规范-自定义指令-lintfix

> ESLint 自动检测 js 代码的规范
>
> 1. 结尾没有;
> 2. 必须===
> 3. 单引号
> 4. 不能有未使用变量
> 5. 缩进
> 6. 不能有多余空行
> 7. 等

1. package.json->scripts->自定义指令
2. ​ "lintfix": "eslint --ext .js,.vue src --fix",
3. npm run lintfix(未使用)
4. npm run dev(启动开发模式)

#### 04-项目-准备-element-ui-文档分析

> 饿了么 web 开发团队 vue UI 库 Element
>
> ElementUI 适用于 vue2+项目并且 PC 端项目

> 扩展: vue 移动端 web -> Mint-ui
>
> PC 端 UI 库: iView

#### 05-项目-准备-element-ui-安装-引入

`main.js`

```js
import ElementUI from "element-ui";
import "element-ui/lib/theme-chalk/index.css";
Vue.use(ElementUI);
```

> 可以在任何一个.vue 文件的 template 通过组件名使用组件

#### 06-项目-准备-项目模板简化-调整

> 简化模板

#### 07-项目-准备-git-版本控制

> 第一次使用 git

```shell

//
git init
//
git add .
//
git commit -m "初始化项目"
// 新建远程仓库->关联仓库
git push -u origin master

```

> 完成一个小功能,提交/推送代码

```shell
git add .
git commit -m "注释"
git push
```

> gitbash -> git 指令操作-> 任何 cmd 执行 git 指令->git 是无效指令-> 配置 windows 系统的环境变量
>
> 1. 找到 git 安装位置 2.修改计算技属性->path 全局变量
>
> 注意: 如果不想改全局 path , 可以在 gitbash 中使用 git

> 每完成一个小功能 提交 commit 一次
>
> 每完成大功能 push 一次

#### 08-项目-准备-git-分支管理

> 管理代码-> 合并代码

> 项目 3 个人-> 区分代码是谁写的?->新建分支

> 每个分支管理自己的代码 有默认分支->git branch

> 主分支 master:git push
>
> 新建子分支 A->编写代码->编码完成->add/commit -> 提交 A->
>
> 切换到 master 分支->合并代码 git merge
>
> 新建子分支 B->编写代码->编码完成->add/commit -> 提交 B->
>
> 切换到 master 分支->合并代码 git merge

> 结论: master/ dev-login /dev-users

```shell
// 检查分支
git branch
// 新建分支并且切换到该分支
// dev-login用来实现项目登录功能
git checkout -b 分支名(dev-login)
// 接下来所有代码操作都是在dev-login分支上

```

#### 09-项目-登录-新建分支-login 组件-配置路由

> 在 dev-login 分支上

1. 新建 login.vue 组件
2. 配置路由
3. 新建 home.vue 组件

```shesll
git add .
git commit -m "登录-配置路由"
// 切换master到分支
git checkout master
```

> 在 master 主分支操作(git push)

```shell
// 合并代码: 把dev-login的代码合并到master分支上
git merge dev-login
// 检查状态
git status
// 如果status有问题
git add .
git coimmit -m ""
// 如果status没问题
git push
```

> 推送完, 切换回 dev-login 分支

```shell
git checkout dev-login
```

#### 10-项目-登录-引入表单组件

`login.vue`

1. 找表单组件
2. 复制代码->提供数据 formdata:{}
3. 提供了类名->测试
4. git branch / git status / git add ./ git commit -m "balabala

#### 11-项目-登录-样式调整

1. assets/css/base.css

```css
html,
body,
h2 {
  padding: 0;
  margin: 0;
  height: 100%;
}
```

2. App.vue

```css
#app {
  height: 100%;
}
```

3. login.vue

```css
.login-wrap {
  height: 100%;
  background-color: #324152;
  display: flex;
  justify-content: center;
  align-items: center;
}
.login-form {
  background-color: #ffffff;
  width: 400px;
  border-radius: 5px;
  padding: 30px;
}
.login-btn {
  width: 100%;
}
```

> 注意: css 样式不是重点!
>
> 扩展: 企业开发, 设计图 psd 会有尺寸/字号/色号...

#### 12-项目-登录-axios 插件

1. npm i axios
2. main.js 导入 axios+配置 baseURL
3. login.vue->发送请求

#### 13-项目-登录-发送登录请求

`login.vue`

```js
 handlelogin() {
      this.$http
        .post(`login`, this.formdata)
        .then(res => {
          console.log(res);
          const {
            data: {
              data,
              meta: { msg, status }
            }
          } = res;
          if (status === 200) {
            console.log("login---success----");
          } else {
            console.log("error----");
          }

          // eg
          // const {per} = {per:"abc"}
          // console.log(per)
          // const {name:newname} = {name:'abc'}
          // console.log(newname);
        })
        .catch(err => {
          console.log(err);
        });
    }

```

```shell
git add .
git commit -m "注释"
```

#### 14-项目-登录-引入提示框组件

> username 或者 password 错误 -> 提示框

```js
this.$message.error(msg);
```

#### 15-项目-登录-登录成功-进入 home 组件

`login.vue`

```js
this.$router.push({
  name: "home"
});
```

> 补充: ES6 对象解构赋值
>
> 数组
>
> 对象(const {per:{name} = {per:{name:'abc'}) -> log(name)

#### 16-项目-登录-简化登录请求代码-async 和 await

> async+await 简化代码:把异步代码变得像同步

```js
async handlelogin() {
    // 目前代码: 异步的结果res在一个函数里面获取的
    // 目的: res的获取是同步
    // const res = axios请求返回的结果
    // console.log(res)

    const res = await this.$http.post(`login`, this.formdata)

    }
```

> 步骤

1. 找到异步代码 前面加 await 接收异步结果 const res
2. 找到异步代码最近的外层函数 , 前面加 async

> 目的: 简化代码

#### 17-项目-登录-保存 token 值

> 将来要使用用户 token 数据,把正确用户 token 存储->cookie/session/sessionStorage/localStorage(存储体积大的数据)

```js
localStorage.setItem("token", token);
```

> 浏览器控制台 application->storage

#### 18-项目-首页-布局容器-样式调整

> 引入 UI 库布局容器

```html
<el-container class="container">
  <el-header>Header</el-header>
  <el-container>
    <el-aside class="aside" width="200px">Aside</el-aside>
    <el-main class="main">Main</el-main>
  </el-container>
</el-container>
```

#### 19-项目-首页-头部-样式调整

> el-row(行)>el-col(列) 24 份

```css
.container {
  height: 100%;

  background: #b3c0d1;
}
.middle {
  text-align: center;
  line-height: 60px;
}
.aside {
  background: red;
}
.main {
  background: gray;
}
.loginout {
  line-height: 60px;
  text-decoration: none;
}
```

> 注意

1. 找组件
2. 提供数据
3. 布局
4. 样式

### day08-项目-重点

#### 01-项目-首页-侧边栏-导航组件-文档

> el-menu router 属性
>
> el-submenu index 属性

#### 02-项目-首页-侧边栏-引入导航组件-调整

`home.vue侧边栏`

```html
<el-submenu index="1">
  <template slot="title">
    <i class="el-icon-location"></i>
    <span>用户管理</span>
  </template>
  <el-menu-item index="1-1">
    <i class="el-icon-menu"></i>
    用户列表
  </el-menu-item>
</el-submenu>
```

#### 03-项目-首页-进入首页的权限验证

```js
beforeMount() {
    console.log("beforeMount----");

    if (!localStorage.getItem("token")) {
      this.$router.push({
        name: "login"
      });
    }
  }
```

> 如果登录了->渲染 home.vue
>
> 如果没登录->来到 login.vue->登录

#### 04-项目-首页-头部-退出功能

> 点击头部的退出按钮

```js
 handleLoginout() {
      // 1. 清除token
      localStorage.clear();
      // 2. 跳转到login
      this.$router.push({
        name: "login"
      });
      // 提示
      this.$message.warning("退出成功");
    }
```

#### 05-项目-首页-合并分支-新建用户分支

```shell
git add .
git commit -m ""
// 新功能 新建分支
git checkout -b dev-users
// 接下来 开发新功能

```

#### 06-项目-用户管理-用户列表-新建组件-路由配置

1. 改标识 index='users'
2. 提供容器 router-view(在 home.vue 的 main 位置)
3. 新建 users.vue
4. 配置路由(嵌套路由->在 home 匹配成功之上)
5. 测试

#### 07-项目-用户管理-用户列表-面包屑和搜索框

1. el-card 小容器
2. 面包屑

```html
<el-breadcrumb separator-class="el-icon-arrow-right">
  <el-breadcrumb-item :to="{ path: '/' }">首页</el-breadcrumb-item>
  <el-breadcrumb-item>用户管理</el-breadcrumb-item>
  <el-breadcrumb-item>用户列表</el-breadcrumb-item>
</el-breadcrumb>
```

`搜索框`

```html
<el-row class="searchBox">
  <el-col>
    <el-input class="searchInput" placeholder="请输入内容" v-model="query">
      <el-button slot="append" icon="el-icon-search"></el-button>
    </el-input>
    <el-button type="primary">添加用户</el-button>
  </el-col>
</el-row>
```

#### 08-项目-用户管理-用户列表-引入表格组件

> el-table

```html
<el-table :data="tableData" style="width: 100%">
  <el-table-column prop="name" label="名字222" width="180"></el-table-column>
  <el-table-column prop="name" label="姓名" width="180"></el-table-column>
  <el-table-column prop="address" label="地址"></el-table-column>
</el-table>
```

1. el-table data 属性->控制的该表格的数据
2. el-table-column 控制的是列
   2.1 label 控制的是表头
   2.2 prop 控制的单元格的内容

#### 09-项目-用户管理-用户列表-表头处理

> 调整表头 label 7 列

#### 10-项目-用户管理-用户列表-请求数据

> 接口文档->除了登录之外的所有 API 请求->都需要授权->设置请求头

```js
async getTableData() {
      // query	查询参数	可以为空
      // pagenum	当前页码	不能为空
      // pagesize	每页显示条数	不能为空
      // 设置发送请求时的请求头-> axios库 ->找axios中有没有可以设置headers头部的API->看axios文档
      //
      const AUTH_TOKEN = localStorage.getItem("token");
      // console.log(AUTH_TOKEN);
      this.$http.defaults.headers.common["Authorization"] = AUTH_TOKEN;
      const res = await this.$http.get(
        `users?query=${this.query}&pagenum=${this.pagenum}&pagesize=${
          this.pagesize
        }`
      );
      console.log(res);

    }
```

#### 11-项目-用户管理-用户列表-渲染数据-一般数据

> 单元格中的数据两类

1. 一般数据 prop 的属性值
2. 特殊数据 不是 prop 的属性值 而是一些组件

```html
<el-table-column prop="id" label="#" width="80"></el-table-column>
<el-table-column prop="username" label="姓名" width="100"></el-table-column>
<el-table-column prop="email" label="邮箱" width="140"></el-table-column>
<el-table-column prop="mobile" label="电话" width="140"></el-table-column>
<el-table-column
  prop="create_time"
  label="创建日期"
  width="200"
></el-table-column>
```

#### 12-项目-用户管理-用户列表-渲染数据-日期格式处理

> 日期需要处理 -> 过滤器 -> 两类(全局 Vue.filter 和局部)三步->1. v-bind 后面 2{msg | 名字}
> 前提:如果单元格数据不是 prop 的值,此时

1. 给内容外层加 template
2. 设置 template 的 slot-scope="scope"
3. 内部通过 scope.row.属性名访问数据
   > 注意: "scope"可以随便命名,自动找外层数据 list

```html
<el-table-column label="创建日期" width="200">
  <template slot-scope="scope">
    <!-- 内层 list.row 表示的是list的每个对象-->
    {scope.row.create_time|fmtdate}
  </template>
</el-table-column>
```

#### 13-项目-用户管理-用户列表-渲染数据-用户状态开关

> el-swtich 开关组件 表单元素 v-model=""

```html
<el-table-column label="用户状态" width="120">
  <!-- 前提: 单元格内容是一个组件, 不是porp的值 -->
  <template slot-scope="scope">
    <!-- 内容 -->
    <el-switch
      v-model="scope.row.mg_state"
      active-color="#13ce66"
      inactive-color="#ff4949"
    ></el-switch>
  </template>
</el-table-column>
```

> 当通过页面操作 点击开关->会让 mg_state 的值变化

#### 14-项目-用户管理-用户列表-渲染数据-操作

> 如果单元格内容不是 porp, 加 tempalte 设置 slot-scope

```html
<el-table-column label="操作" width="200">
  <template slot-scope="scope">
    <el-button
      type="primary"
      icon="el-icon-edit"
      circle
      size="mini"
      plain
    ></el-button>
    <el-button
      type="danger"
      icon="el-icon-delete"
      circle
      size="mini"
      plain
    ></el-button>
    <el-button
      type="success"
      icon="el-icon-check"
      circle
      size="mini"
      plain
    ></el-button>
  </template>
</el-table-column>
```

#### 15-项目-用户管理-用户列表-分页组件-文档-引入

> 分页组件 - 文档

1. @size-change 每页条数改变时
2. @current-change 原来是第一页,点击 2 页
3. current-page 当前页码
4. total 总条数

#### 16-项目-用户管理-用户列表-分页组件-配置数据

```html
<el-pagination
  @size-change="handleSizeChange"
  @current-change="handleCurrentChange"
  :current-page="pagenum"
  :page-sizes="[2, 4, 6, 8]"
  :page-size="2"
  layout="total, sizes, prev, pager, next, jumper"
  :total="total"
></el-pagination>
```

> res 中有 total this.total=data.total

#### 17-项目-用户管理-用户列表-分页组件-分页请求

```js
handleSizeChange(val) {
      console.log(`每页 ${val} 条`);
      this.pagenum = 1;
      this.pagesize = val;
      this.getTableData();
    },
    // 当前1页 -> 点击2页 -> 获取第二页数据
    handleCurrentChange(val) {
      console.log(`当前页: ${val}`);
      // 根据新页码发送请求
      this.pagenum = val;
      this.getTableData();
    },

```

> pagenum1 pagesize2 -> 获取数据库中前两条数据
> pagenum=3 pagesize=3 -> 获取数据库中第 7/8/9 条数据

#### 18-项目-用户管理-用户列表-搜索用户

1. 搜索用户
2. 清空
   > 不要忘记 this.pagenum=1

```js

// 清空时获取所有用户
    getAllUsers() {
      // 此时 query查询参数已经是''

      this.getTableData();
    },
    // 搜索用户
    searchUser() {
      // 输入框组件->在组件文本清空时->做一些事儿
      // query数据默认 ''
      this.pagenum = 1;
      this.getTableData();
    },
```

#### 19-项目-用户管理-用户列表-添加用户-显示对话框

> 点击按钮->打开对话框

```html
<el-dialog title="收货地址" :visible.sync="dialogFormVisibleAdd">
  <el-form label-position="left" label-width="80px" :model="formdata">
    <el-form-item label="用户名">
      <el-input v-model="formdata.username"></el-input>
    </el-form-item>
    <el-form-item label="密码">
      <el-input v-model="formdata.password"></el-input>
    </el-form-item>
    <el-form-item label="邮箱">
      <el-input v-model="formdata.email"></el-input>
    </el-form-item>
    <el-form-item label="电话">
      <el-input v-model="formdata.mobile"></el-input>
    </el-form-item>
  </el-form>
  <div slot="footer" class="dialog-footer">
    <el-button @click="dialogFormVisibleAdd = false">取 消</el-button>
    <el-button type="primary" @click="dialogFormVisibleAdd = false"
      >确 定</el-button
    >
  </div>
</el-dialog>
```

> 1. 复制代码 2. 提供/配置属性或者方法 3. 使用

### day09-项目-重点

#### 01-项目-用户管理-用户列表-添加用户-发送请求

> 点击确定->发送请求

```js
 async addUser() {
      // 发送请求
      // this.formdata?
      const res = await this.$http.post(`users`, this.formdata);
      console.log(res);
      const {
        meta: { msg, status }
      } = res.data;
      if (status === 201) {
        // 关闭对话框
        this.dialogFormVisibleAdd = false;
        // 更新表格
        this.getTableData();
      }
    },
```

> 不要忘记清空,打开对话框,this.formdata={}

#### 02-项目-用户管理-用户列表-删除用户-打开确认框

> 引入确认框

```js
this.$confirm("是否把我删掉?", "提示", {
  confirmButtonText: "确定",
  cancelButtonText: "取消",
  type: "warning"
})
  .then(() => {
    this.$message.success("删除成功");
  })
  .catch(() => {
    this.$message.info("取消删除");
  });
```

> 点击确定->执行.then
> 点击取消->执行.catch

#### 03-项目-用户管理-用户列表-删除用户-处理响应

> 点击确定->发送 delete 请求
> 注意:async 位置,距离异步最近的外层函数

#### 04-项目-用户管理-用户列表-编辑用户-显示对话框

> 点击操作中的编辑按钮->显示对话框
> 使用的是之前的 formdata

#### 05-项目-用户管理-用户列表-编辑用户-显示编辑数据

> 在打开对话框时,

```js
this.formdata = user;
```

#### 06-项目-用户管理-用户列表-编辑用户-发送请求

> 点击对话框的确定按钮->发送请求
> 注意: 发请求的参数 id->来源是上一步赋值的结果 this.formdata=user

#### 07-项目-用户管理-用户列表-修改用户状态

> el-switch v-model 绑定 -> 视图操作 View->被绑定数据变化

```js
async changeState(user) {
      // uid->user
      // type -> user
      const res = await this.$http.put(
        `users/${user.id}/state/${user.mg_state}`
      );
      console.log(res);
    },
```

#### 08-项目-用户管理-用户列表-分配角色-功能演示

> 每个用户都有角色
> 每个角色能做的事儿是不同的,
> 可以做的操作称之为权限
> 给用户分配角色

1. 点按钮->打开对话框
2. 显示用户信息(用户名+角色)
3. 点击确定->修改用户角色

#### 09-项目-用户管理-用户列表-分配角色-显示对话框

> 点击操作中的 check 按钮->打开对话框

#### 10-项目-用户管理-用户列表-分配角色-显示对话框-下拉框

> 1. 默认显示请选中->当 v-model 的数据值 selectVal 和 option 的请选择的 value 值相等, 此时显示请选择
> 2. 当选择某个 option 时,v-model 的数据的值等于选中的 label 的 value 值

```js
 <el-select v-model="selectVal" placeholder="请选择角色">
            <el-option label="请选择" :value="1"></el-option>
            <el-option
              v-for="(item,i) in roles"
              :key="item.id"
              :label="item.roleName"
              :value="item.id"
            ></el-option>

            <!-- 将来获取角色名数据->v-for遍历 -->
          </el-select>
```

#### 11-项目-用户管理-用户列表-分配角色-显示当前用户角色

> 角色 id [30,31,34,39,40]
> 每个用户都有角色 v-model="searchVal"

```js
const res2 = await this.$http.get(`users/${user.id}`);
// console.log(res2);
// 给下拉框v-model绑定的selectVal赋值
this.selectVal = res2.data.data.rid;
```

#### 12-项目-用户管理-用户列表-分配角色-修改用户角色

> 点击确定->发送请求

```js
  async setRole() {
      // currUserId
      const res = await this.$http.put(`users/${this.currUserId}/role`, {
        rid: this.selectVal
      });
      // console.log(res);
      const {
        meta: { msg, status }
      } = res.data;
      if (status === 200) {
        // 关闭
        this.dialogFormVisibleRole = false;
      }
    },
```

#### 13-项目-用户管理-用户列表-合并分支-推送

```shell
// 在分支上
git status
git checkout master
// 在主分支
git status
git merge dev-users
git push

```

#### 14-项目-权限管理-新建分支-功能演示

1. git checkout -b dev-rights
   > 功能拆分
   >
   > 1. 权限列表
   > 2. 角色列表
   >    面包屑+表格(展开+check 按钮)

#### 15-项目-权限管理-权限列表-新建组件-路由配置

> rights.vue 组件

#### 16-项目-权限管理-权限列表-自定义面包屑组件

> props 传值

1. 声明 props:[数据 a]
2. 赋值 使用组件时 <abc a="值">
3. 使用 {a}
   > 重复代码->封装组件

#### 17-项目-权限管理-权限列表-获取权限列表数据

> url 中 type=list
> 在当前组件中,没有设置头部,所以此时无法获取数据

```js
const AUTH_TOKEN = localStorage.getItem("token");
this.$http.defaults.headers.common["Authorization"] = AUTH_TOKEN;
const res = await this.$http.get(`rights/list`);
console.log(res);
const {
  data,
  meta: { msg, status }
} = res.data;
if (status === 200) {
  this.list = data;
}
```

#### 18-项目-权限管理-权限列表-axios-封装插件

1. 把头部设置封装起来
2. main.js 有 5 行代码是 axios 的
3. 把 5 行代码提取为 js 模块
4. 把 axios 变成了 Vue 插件
5. 在 main.js 中导入插件并且使用
   > 任何请求头部和 baseUrl 不需要写

```js
import axios from "axios";

const HttpServer = {};

HttpServer.install = function(Vue) {
  axios.defaults.baseURL = "http://localhost:8888/api/private/v1/";
  const AUTH_TOKEN = localStorage.getItem("token");
  axios.defaults.headers.common["Authorization"] = AUTH_TOKEN;
  Vue.prototype.$http = axios;
};

export default HttpServer;
```

#### 19-项目-权限管理-权限列表-axios-拦截器统一设置请求头

// fetch.js 拦截
// axios.js 拦截
// jq \$.ajax 拦截

> axios 请求拦截器

1. 所有请求发起之前,都会自动先进入拦截器
2. 在拦截器筛选请求 config.url=?
3. config.headers[]=token

```js
axios.interceptors.request.use(
  function(config) {
    // 在发送请求之前做些什么
    console.log("请求拦截器被触发了-----");

    // 所有请求发起之后,进行筛选,请求标识是不是login
    // 如果标识是login,不要头部->请求继续发起
    // 当请求标识不是login,先设置头部,再发送请求
    if (config.url !== "login") {
      const AUTH_TOKEN = localStorage.getItem("token");
      // axios.defaults.headers.common["Authorization"] = AUTH_TOKEN;
      config.headers["Authorization"] = AUTH_TOKEN;
      // var per = {};
      // per["Authorization"] = "token";
    }
    // this.$http.get(url) -> 请求拦截处理 ->发请求

    console.log(config);

    return config;
  },
  function(error) {
    // 对请求错误做些什么
    return Promise.reject(error);
  }
);
```

> 结果: 之后再也不用写请求头了

### day10-项目-重点

#### 01-项目-权限管理-权限列表-表格展示

> 把 user.vue 的 el-table->修改
> el-table-column 属性 type="index" 序号从 1 自增

#### 02-项目-权限管理-权限列表-表格展示-层级显示

> res 的数据中 level 是字符'0'

```html
<el-table-column label="层级" width="200">
  <template slot-scope="scope">
    <span v-if="scope.row.level==='0'">一级</span>
    <span v-if="scope.row.level==='1'">二级</span>
    <span v-if="scope.row.level==='2'">三级</span>
  </template>
</el-table-column>
```

#### 03-项目-权限管理-角色列表-新建组件-配置路由

> 新建 roles.vue 组件+配置路由+home.vue 改标识

#### 04-项目-权限管理-角色列表-面包屑和添加按钮

> 自定义面包屑+el-button

#### 05-项目-权限管理-角色列表-获取角色列表数据

> methods 中 getRoles()

#### 06-项目-权限管理-角色列表-表格展示

> 把 user.vue 复制->修改

#### 07-项目-权限管理-角色列表-表格展示-展开行功能分析

> 1. 所有行列布局->for 嵌套->v-for
> 2. el-row>(el-col>el-tag>+el-col>(el-row>(el-col>el-tag+el-col>el-tag)))
> 3. 有颜色的标签 el-tag
> 4. 4:20

#### 08-项目-权限管理-角色列表-表格展示-展开行-一级权限

> 最外层 v-for 的位置是最外层 el-row

#### 09-项目-权限管理-角色列表-表格展示-展开行-二级三级权限

```html
<el-row class="level1" v-for="(item1,i) in scope.row.children" :key="item1.id">
  <el-col :span="4">
    <el-tag closable type="success">{item1.authName}</el-tag>
  </el-col>
  <el-col :span="20">
    <el-row class="level2" v-for="(item2,i) in item1.children" :key="item2.id">
      <el-col :span="4">
        <el-tag closable type="warning">{item2.authName}</el-tag>
      </el-col>
      <el-col :span="20">
        <el-tag
          closable
          type="info"
          v-for="(item3,i) in item2.children"
          :key="item3.id"
          >{item3.authName}</el-tag
        >
      </el-col>
    </el-row>
  </el-col>
</el-row>
```

> 最里层的 v-for 写在 el-tag 位置

#### 10-项目-权限管理-角色列表-展开行-样式调整-处理无权限

1. closeable el-tag X
2. i 标签 class=""
3.

```html
<el-row v-if="scope.row.children.length===0">
  <el-col>
    <span>未分配权限</span>
  </el-col>
</el-row>
```

#### 11-项目-权限管理-角色列表-展开行-取消权限

> 点击 el-tag 的 X->取消权限
> @close="deleRights(scope.row,itemX)"

#### 12-项目-权限管理-角色列表-展开行-取消权限-优化

```js
    // 取消权限
    async deleRights(role, rights) {
      // console.log(role, rights);

      // roleId->角色id
      // rightId->权限id
      const res = await this.$http.delete(
        `roles/${role.id}/rights/${rights.id}`
      );
      console.log(res);
      const {
        meta: { msg, status },
        data
      } = res.data;
      if (status === 200) {
        // 提示
        this.$message.success(msg);
        // 更新
        // this.getRoles();
        // 会返回当前角色的剩余权限
        // 只更新当前的角色权限
        role.children = data;
      }
    },
```

> 取消成功后,res 返回的是当前觉得 rest 权限

#### 13-项目-权限管理-角色列表-修改权限-显示对话框

> 点击操作中 check 按钮->打开对话框

#### 14-项目-权限管理-角色列表-修改权限-树形结构-文档分析

> 1. data 数据源
> 2. node-key 每个节点唯一标识
> 3. default-expanded-keys[] 默认展开
> 4. default-checked-keys [] 默认选中
> 5. props 配置选项{label/children}

> 前提:res 数据格式是树形结构

#### 15-项目-权限管理-角色列表-修改权限-树形结构-配置数据

> 1. treelist 每个权限的唯一标识 id->node-key="id"
> 2. label="authName"
> 3. pid->上一/二级节点 id

#### 16-项目-权限管理-角色列表-修改权限-树形结构-显示已有权限

1. 默认展开 default-expand-all
2. 默认选中
   2.1 获取当前角色有的权限数据 role.children
   2.2 遍历 forEach
   2.3 arrCheck=temp2
   > 注意:只加最里层的 id

#### 17-项目-权限管理-角色列表-修改权限-树形结构-分配权限-分析

> 1. 获取全选 id 数组
> 2. 获取半选 id 数组

```js
const arr1 = this.$refs.treeDom.getCheckedKeys();
console.log(arr1);

// 获取半选节点id -> getHalfCheckedKeys
const arr2 = this.$refs.treeDom.getHalfCheckedKeys();
console.log(arr2);
```

> ref 操作 dom
>
> 1. 给要操作的标签设置 ref 值
> 2. 在 js 中 this.\$refs.ref 值.js 方法()

#### 18-项目-权限管理-角色列表-修改权限-树形结构-分配权限-实现

```js
const res = await this.$http.post(`roles/${this.currRoleId}/rights`, {
  rids: arr.join(",")
});
```

> 1. ...arr 或者 obj
> 2. rids:以,分割的 id 列表 arr arr.join(",")
>    并不是所有数据都是提供好的

#### 19-项目-首页-侧边栏-动态导航

> ESLint 关闭->build/webpack.base.conf.js->42 行->注释
> 效果: 每个不同角色的用户->登录->显示拥有权限的对应导航

```js
    async getMenus() {
      const res = await this.$http.get(`menus`);
      console.log(res);
      const {
        meta: { msg, status },
        data
      } = res.data;
      if (status === 200) {
        this.menus = data;
      }
    },
```

```html
<el-submenu :index="item1.order+''" v-for="(item1,i) in menus" :key="item1.id">
  <template slot="title">
    <i class="el-icon-location"></i>
    <span>{item1.authName}</span>
  </template>

  <el-menu-item
    :index="item2.path+''"
    v-for="(item2,i) in item1.children"
    :key="item2.id"
  >
    <i class="el-icon-menu"></i>
    <span>{item2.authName}</span>
  </el-menu-item>
</el-submenu>
```

> 结果: 在实现之后的功能时,路由配置的 path 不能随便写了!

#### 20-项目-效果演示-不同角色用户登录-显示对应权限

> 1. 不同用户登录后,权限不一样
> 2. 超管登录只能权限管理

```js
```

#### 21-项目-不同角色用户登录-显示对应权限-导航守卫

> 标识改变->路由配置->配置生效前->守卫->next()->配置生效
>
> 1. to->要去的
> 2. from->当前
> 3. next next()->继续执行之前的配置

```js
router.beforeEach((to, from, next) => {
  // 如果要去的是login -> next()
  if (to.name === "login") {
    next();
  } else {
    // 如果要去的不是login ->
    //  2.1 !token -> 去登录
    const token = localStorage.getItem("token");
    if (!token) {
      //提示
      // this.$message.warning("请先登录!");->
      Message.warning("请先登录!");

      //  this.$router.push({name:'login'})
      // $router
      router.push({
        name: "login"
      });
      return;
    }
    //  2.2 token  -> next()
    next();
  }

  // console.log(to, from);

  // next方法
});
```

> 注意: router/index.js 中 this 不是 Vue 实例
>
> 1. this.\$router->rotuer
> 2. 提示框->单独导入 Message
> 3. 之前的 home.vue 的 beforeMount 不用写了

#### 22-项目-权限管理-合并分支-推送-新建分支

### day11-项目-重点

#### 01-项目-商品管理-功能演示-新建分支

1. 列表->添加商品
2. 分类参数->动态+静态参数编辑
3. 商品分类->表格展开后的树形结构

#### 02-项目-商品管理-商品列表-显示(提前准备)

> 02-其他资源/goodslist.vue

1. 面包屑名称 cus-bread
2. fmtdate
3. loading 删掉
4. 配置路由(path 不能随便写了)

#### 03-项目-商品管理-添加商品-新建组件-配置路由-布局

1. 新建组件 goodsadd.vue
2. 配置路由
   > path 可以随便写
3. <el-alert class="alert" title="添加商品信息" type="info" center show-icon></el-alert>

#### 04-项目-商品管理-添加商品-步骤条

```html
<el-steps :active="active*1" align-center>
  <el-step title="基本信息"></el-step>
  <el-step title="商品参数"></el-step>
  <el-step title="商品属性"></el-step>
  <el-step title="商品图片"></el-step>
  <el-step title="商品内容"></el-step>
</el-steps>
```

> active 控制的是当前完成了第几步

#### 05-项目-商品管理-添加商品-tabs 标签

> 标签页:表单元素 v-model 绑定

```html
<el-tabs v-model="active" tab-position="left">
  <el-tab-pane name="1" label="基本信息">基本信息----</el-tab-pane>
  <el-tab-pane name="2" label="商品参数">商品参数----</el-tab-pane>
  <el-tab-pane name="3" label="商品属性">商品属性----</el-tab-pane>
  <el-tab-pane name="4" label="商品图片">商品图片----</el-tab-pane>
  <el-tab-pane name="5" label="商品内容">商品内容----</el-tab-pane>
</el-tabs>
```

#### 06-项目-商品管理-添加商品-基本信息-绑定表单数据

```html
<el-tab-pane name="1" label="基本信息">
  <el-form-item label="商品名称">
    <el-input v-model="form.goods_name"></el-input>
  </el-form-item>
  <el-form-item label="商品价格">
    <el-input v-model="form.goods_price"></el-input>
  </el-form-item>
  <el-form-item label="商品重量">
    <el-input v-model="form.goods_weight"></el-input>
  </el-form-item>
  <el-form-item label="商品数量">
    <el-input v-model="form.goods_number"></el-input>
  </el-form-item>
  <el-form-item label="商品分类">
    <!-- 表单元素 -->
  </el-form-item>
</el-tab-pane>
```

```json
  form: {
        goods_name: "",
        goods_cat: "",
        goods_price: "",
        goods_number: "",
        goods_weight: "",
        goods_introduce: "",
        pics: "",
        attrs: ""
      }
```

#### 07-项目-商品管理-添加商品-基本信息-级联选择器-文档-引入

> 级联选择器表单元素 v-model="数组"
>
> 1. [1,2,3]
> 2. 当选择某个 label->[value 值]

#### 08-项目-商品管理-添加商品-基本信息-级联选择器-获取分类数据

> const res = await this.\$http.get(`categories?type=3`);
> :props="{label/value/children}"

#### 09-项目-商品管理-添加商品-基本信息-级联选择器-配置数据

```html
<el-cascader
  clearable
  expand-trigger="hover"
  :options="options"
  :props="defaultProp"
  v-model="selectedOptions"
  @change="handleChange"
></el-cascader>
```

```js
async getGoodsCate() {
      const res = await this.$http.get(`categories?type=3`);
      console.log(res);
      const {
        meta: { msg, status },
        data
      } = res.data;
      if (status === 200) {
        this.options = data;
      }
    },
```

```json
// label/value/children默认值是同名字符串
defaultProp: {
        label: "cat_name",
        value: "cat_id"
      }
```

#### 10-项目-商品管理-添加商品-商品参数-获取动态参数数据

> 选择第二个 tab&&三级分类->发送请求(获取动态参数)

```js
const res = await this.$http.get(
  `categories/${this.selectedOptions[2]}/attributes?sel=many`
);
```

#### 11-项目-商品管理-添加商品-商品参数-复选框组-文档-引入

> el-checkbox-group->v-model="[]" 表单元素

#### 12-项目-商品管理-添加商品-商品参数-配置复选框

> 处理数据 arrDy->item.attr_Vals""->[]

```html
<el-form-item
  :label="item1.attr_name"
  v-for="(item1,i) in arrDy"
  :key="item1.attr_id"
>
  <el-checkbox-group v-model="item1.attr_vals">
    <el-checkbox
      border
      :label="item2"
      v-for="(item2,i) in item1.attr_vals"
      :key="i"
    ></el-checkbox>
  </el-checkbox-group>
</el-form-item>
```

```js
this.arrDy.forEach(item => {
  item.attr_vals =
    item.attr_vals.trim().length === 0 ? [] : item.attr_vals.trim().split(",");
  console.log(item.attr_vals);
});
```

> 1. border
> 2. v-model="item1.attr_val"

#### 13-项目-商品管理-添加商品-商品属性-获取静态参数数据

> 点击第三个 tab && 分类数组长度===3->发送 only 请求

```js
if (this.active === "3") {
  const res = await this.$http.get(
    `categories/${this.selectedOptions[2]}/attributes?sel=only`
  );
  const {
    meta: { msg, status },
    data
  } = res.data;
  if (status === 200) {
    this.arrStatic = data;
    console.log(this.arrStatic);
  }
}
```

#### 14-项目-商品管理-添加商品-商品属性-布局

```html
<el-tab-pane name="3" label="商品属性">
  <el-form-item
    :label="item.attr_name"
    v-for="(item,i) in arrStatic"
    :key="item.attr_id"
  >
    <el-input v-model="item.attr_vals"></el-input>
  </el-form-item>
</el-tab-pane>
```

#### 15-项目-商品管理-添加商品-图片上传-文档-引入

> 1. action 全路径网址
> 2. headers 请求头

#### 16-项目-商品管理-添加商品-图片上传-配置属性

> 1. action 全路径网址
> 2. headers 请求头
>    之前的只针对 axios

```js
// 图片上传方法
    handleRemove(file, fileList) {
      // console.log("remove----");
      console.log(file);
      //  临时路径
      file.response.data.tmp_path;
    },
    handleSuccess(response, file, fileList) {
      // console.log("success----");

      console.log(response);
      // response.data.tmp_path -> 临时路径
    },
```

#### 17-项目-商品管理-添加商品-商品内容-富文本编辑器

```html
<el-tab-pane name="5" label="商品内容">
  <el-form-item>
    <el-button @click="addGoods()">添加商品</el-button>
    <quill-editor class="quill" v-model="form.goods_introduce"></quill-editor>
  </el-form-item>
</el-tab-pane>
```

```js
import "quill/dist/quill.core.css";
import "quill/dist/quill.snow.css";
import "quill/dist/quill.bubble.css";

import { quillEditor } from "vue-quill-editor";
```

> 1. quill-editor 是表单元素 v-model
> 2. SPA 和 SSR
>    扩展: vue 适合 SPA->缺点之一:不利于 SEO->服务端渲染 SSR<-Nuxt.js

#### 18-项目-商品管理-添加商品-表单数据分析

> 1. goods_cat [1,2,3]->"1,2,3"
> 2. pics:[{pic:临时路径}]
> 3. attrs:[{attr_id:?,attr_value:?}]
>    来源 arrDy 和 arrStatic 中每个对象的 attr_id 和 attr_vals

#### 19-项目-商品管理-添加商品-表单数据处理-分类和图片

> 1. this.form.goods_cat = this.selectedOptions.join(",");

> 2.  处理 this.form.pics

```js

handleRemove(file, fileList) {
      // findIndex(ES6数组新增API)
      const Index = this.form.pics.findIndex(item => {
        // console.log(item);// item.pic
        return item.pic === file.response.data.tmp_path;
      });
      this.form.pics.splice(Index, 1);
      console.log(this.form.pics);
    },
    handleSuccess(response, file, fileList) {

      // response.data.tmp_path -> 临时路径

      this.form.pics.push({
        pic: response.data.tmp_path
      });
      console.log(this.form.pics);
    },
```

#### 20-项目-商品管理-添加商品-表单数据处理-attrs

```js
const arr1 = this.arrDy.map(item => {
  return { attr_id: item.attr_id, attr_value: item.attr_vals };
});
console.log(arr1);

const arr2 = this.arrStatic.map(item => {
  return { attr_id: item.attr_id, attr_value: item.attr_vals };
});
console.log(arr2);

this.form.attrs = [...arr1, ...arr2];
```

#### 21-项目-商品管理-添加商品-发送请求-回到商品列表页

```js
const res = await this.$http.post(`goods`, this.form);
```

> 回到列表

> 解决了 bug

```js
if (this.active === "2") {
  this.arrDy = [];
} else {
  this.arrStatic = [];
}
```

### day12-项目-重点

#### 01-项目-商品管理-分类参数-新建组件-路由配置

> 分类参数.vue
> 级联+tabs+动态 el-tag 编辑(删除/添加)
> cateparams.vue

#### 02-项目-商品管理-分类参数-动态参数-布局-配置级联选择器

> goodsadd.vue 的级联完全一样
> 仅显示最后一级 label :show-all-levels="false"

#### 03-项目-商品管理-分类参数-动态参数-获取动态参数数据

> 点击级联选择器且是三级分类->获取动态参数数组

#### 04-项目-商品管理-分类参数-动态参数-表格渲染

> goodslist 的 el-table->修改

#### 05-项目-商品管理-分类参数-动态参数-动态编辑-文档-引入

> el-tag 文档->动态编辑
> 标签+css+data+js 三个方法

#### 06-项目-商品管理-分类参数-动态参数-动态编辑-配置-完成

> 把动态 tag 编辑的 dynamicTags 换成自己的 arrDy 中每个对象的 attr_vals

#### 07-项目-商品管理-分类参数-动态参数-动态编辑-发送请求

> 删除/添加属性值

```js
const res = await this.$http.put(
  `categories/${this.selectedOptions[2]}/attributes/${obj.attr_id}
        `,
  {
    attr_name: obj.attr_name,
    attr_sel: obj.attr_sel,
    // 以,分割的属性值列表 [].join(",")
    attr_vals: obj.attr_vals.join(",")
  }
);
```

#### 08-项目-商品管理-分类参数-静态参数-布局-获取数据

> 1. 级联选择器@change->获取动态 or 静态
> 2. el-tabs@tab-click->获取动态 or 静态
>    getDyOrStatic()

#### 09-项目-商品管理-商品分类-组件(提前准备)-路由配置

> 02-其他资源/goodscate.vue(商品分类组件)->cus-bread

1. 添加分类
2. 表格的列展开后类树形结构

#### 10-项目-商品管理-商品分类-element-tree-grid-文档-引入

> el-table 展开之后没有类树形结构

1. 不用 element->不好
2. 找一个 element 这个插件的插件 x-table(扩展 el-table)->替换了整个 el-table
3. 找 el-table 的插件->替换 el-table-column->推荐->xxx-table-column
   > npm->element-tree-grid

#### 11-项目-商品管理-商品分类-element-tree-grid-配置

```html
<el-tree-grid
  prop="cat_name"
  width="120"
  label="分类名称"
  treeKey="cat_id"
  parentKey="cat_pid"
  childKey="children"
  levelKey="cat_level"
></el-tree-grid>
```

#### 12-项目-商品管理-商品分类-添加分类-打开对话框

> 获取 type=2 前两级分类

#### 13-项目-商品管理-商品分类-添加分类-发送请求

```js
if (this.selectedOptions.length === 0) {
  this.form.cat_level = 0;
  this.form.cat_pid = 0;
}
// 二级分类->如果级联的数组长度1->cat_pid=上一级id(this.selectoption[0]) cat_level=1
if (this.selectedOptions.length === 1) {
  this.form.cat_level = 1;
  this.form.cat_pid = this.selectedOptions[0];
}
// 三级分类->如果级联的数组长度2->cat_pid=上一级id(this.selectoption[1]) cat_level=2
if (this.selectedOptions.length === 2) {
  this.form.cat_level = 2;
  this.form.cat_pid = this.selectedOptions[1];
}
```

#### 14-项目-合并分支-推送分支-新建分支

> dev-order

#### 15-项目-订单管理-订单列表-组件(提前准备)-路由配置

> 02-其他资源/order.vue 订单组件
> 给级联提供省市区的数据

#### 16-项目-订单管理-订单列表-省市区引入

> 省市区(联动)
> 客户端:网站 web/安卓/苹果->省市区->.json 或者.js
> 在.vue 中可以使用.js 模块
> 比如:wow.js iscroll.js swiper.js 等
> vue-swiper.js

#### 17-项目-数据统计-数据报表-Echarts-文档-引入

> 数据可视化:

1. flash 画图
2. H5->canvas 标签(画布)
   > 3D 建模
3. D3.js
4. three.js
5. WebGL
6. Echarts.js(百度的一个产品)
   > mounted(){方法调用}

#### 18-项目-数据统计-数据报表-Echarts-配置

> url-> "reports/type/1"

#### 19-项目-优化-加载动画

> 动画->img src="xxoo.gif"
> element->el-table v-loading="loading"

#### 20-项目-优化-拦截器统一处理响应

> 统一处理 status 非 200 和 201 的情况->提示框

```js
axios.interceptors.response.use(
  function(response) {
    // 对响应数据做点什么
    const {
      meta: { msg, status }
    } = response.data;
    // 统一处理status非200和201的情况->提示框
    if (status !== 200 && status !== 201) {
      Message.warning(msg);
    }

    return response;
  },
  function(error) {
    // 对响应错误做点什么
    return Promise.reject(error);
  }
);
```

### day13-项目-重点

#### 00-反馈-补充

1. 分类参数.vue->动态 tag 编辑->el-input->同时变
   思路 1:绑定不同的数据->动态 v-model="obj[scope.$index]"赋值
   思路 2:只打开一个

```html
el-table @expand-change="fn"
```

```js
if (expandedRows.length > 1) {
  expandedRows.shift();
}
```

2. 补充:侧边栏刷新时->回到之前激活状态
   > 我是谁?w 我在哪?我要做什么?
   > 侧边栏 home.vue+el-menu(属性方法事件)+记录刷新前点击时路由参数(name/path 等)
   > el-menu :dafault-active="\$route.name"
   > 前提 路由配置中 name 和 path 中

#### 01-项目-补充-nextTick

```js
this.$nextTick(() => {
  // 操作dom的代码
  console.log(this.$refs.txt.innerText);
});
```

#### 02-项目-打包-演示

> 打包前:npm run dev
> vuecli->目录->.vue 文件+.css+.js 等
> 打包后:项目目录(.html+.css+.js+字体)

> webpack:提供了打包的指令
> 来到项目所在目录->npm run build

> 产物
> dist/(index.html+static)
> static/(js+css+font)
> js/

1. app.xxx.js 自己的 js 代码(组件自己的 js+公共的 js)
2. manifest.js 缓存
3. vender.xxx.js 第三方的 js
   > 目前.map 不用关心
   > 小问题 vender.xxx.js 很大->1.99M
   > app.xxx.js->149K

> 项目服务器:把 dist 目录放在服务器路径下

#### 03-项目-优化-路由懒加载

> 目前效果
> 任何组件显示->network->加载了所有资源(app.xxx.js 等)

> 处理之后(router/index.js)

```js
const Login = () => import("@/components/login.vue");
```

> 重新打包 npm run build
> js/

1. app.xx.js ->公共的 js 代码-.变小
2. 序号.xx.js -> 每个组件自己的 js 代码

> 页面中显示某个组件->只加载了对应的.js->SPA 首屏加载变快

#### 04-项目-优化-cdn-配置

> vender.xxx.js->961K
> 第三方.js 在本地 vender.xx.js 中->CDN(网址加载)

1. 找 cdn 资源(官网+bootcdn 网站)->index.html(打包前)多了好多链接
2. 配置 cdn(告诉加载来源 cdn)->webpack->修改 webpack 配置

```json
externals: {
    // jquery: 'jQuery'

    // key->js的包名->package.json
    // value->该包暴露给全局作用域内的变量名
    "vue": "Vue",
    "vue-router": "VueRouter",
    "element-ui": "ELEMENT",
    "axios": "axios",
    "moment": "moment",
    "echarts": "echarts"
  },
```

3. 改变量名-->改为上一步的全局变量名
   3.1 main.js Vue+ELEMENT(改) + element 样式文件引入(删除)
   3.2 router/index.js->VueRouter
   3.3 报表/echarts

> 4 npm run build
> 对比 vender.xx.js 的大小 961K->19.6K

#### 05-项目-打包(优化后)

> npm run build->
> index.html->用户访问的首页
> js/

1. app.xx.js->自己的公共 js
2. 序号.xx.js->组件的对应 js
3. vender.xx.js->第三方的 js
   css/->希望每个组件的 css 代码在当前组件内生效
   > 在.vue 文件的 style 开始标签位置设置 scoped
4. .map 文件作用:用来调试->用户不需要->在打包时通过 webpack 配置
   > 在 webpack.prod.conf.js->注释掉
5. 随机数问题 app.xx.js
   > 1 版本打包->1.xx1.js->用户浏览网页->2 版本打包->1.xx2.js->用户浏览网页 1.xx2.js
6. dist/->放在项目上线服务器 index.html www.xxoo.com/index.html
