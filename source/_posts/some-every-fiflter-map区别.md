---
title: 'some,every,fiflter,map区别'
date: 2019-02-22 12:57:38
tags: js
---
1. some():返回一个Boolean，判断是否有元素符合func条件
const arr = [1,2,3,4]; arr.some((item)=>{return item>1})

打印结果： true


2. every():返回一个Boolean，判断每个元素是否符合func条件
const arr1 = [1,2,3,4]; arr.every((item)=>{return item>3});
打印结果：
false
<!-- more -->

3. filter():返回一个符合func条件的元素数组

let ages = [33,44,55,66,77]; ages.filter((item)=>{return item>18})
打印结果[33, 44, 55, 66, 77]


4. map（）：返回一个新的array，数组元素由每一次调用函数产生结果组成
const arr =[1,2,3,4,5,6]; arr.map((item)=>{return item*10})
打印结果 [10, 20, 30, 40, 50, 60]