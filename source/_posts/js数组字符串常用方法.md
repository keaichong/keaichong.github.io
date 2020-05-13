---
title: js数组字符串常用方法
date: 2019-02-02 21:35:22
tags: "js"
---

## 数组常用方法:

1. push(): 向数组尾部添加一个或多个元素，并返回添加新元素后的数组长度。注意，该方法会改变原数组。

```js
1 var arr = [1,2,3];
2 console.log(arr);        //  [1, 2, 3]
3 var b = arr.push(4);
4 console.log(b);          //  4   //表示当前数组长度
5 console.log(arr);        // [1, 2, 3, 4]
```

pop(): 删除数组的最后一个元素，并返回该元素。注意，该方法会改变原数组。

```js
1 var arr = [1,2,3];
2 console.log(arr);                // [1,2,3]
3 arr.pop();
4 console.log( arr.pop() );　　// [3]　　//返回删除的元素
5 console.log(arr);                // [1,2]
```

2.  unshift():在数组的第一个位置添加元素，并返回添加新元素后的数组长度。注意，该方法会改变原数组。
    <!-- more -->

```js
1 var arr = ['a', 'b', 'c'];
2 arr.unshift('x');        // 4
3 console.log(arr);        // ['x', 'a', 'b', 'c']
```

shift():删除数组的第一个元素，并返回该元素。注意，该方法会改变原数组。

```js
1 var arr = ['a', 'b', 'c'];
2 arr.shift()         // 'a'
3 console.log(arr)     // ['b', 'c']
```

shift()方法还可以遍历并清空一个数组。

```js
1 var list = [1, 2, 3, 4, 5, 6];
2 var item;
3
4 while (item = list.shift()) {
5   console.log(item);
6 }
7
8 console.log(list);     // []
```

3. valueOf():返回数组的本身。

```js
1 var arr = [1, 2, 3];
2 arr.valueOf()     // [1, 2, 3]
```

indexOf():返回指定元素在数组中出现的位置，如果没有出现则返回-1。

```js
1 var arr = ['a', 'b', 'c'];
2
3 arr.indexOf('b') // 1
4 arr.indexOf('y') // -1
```

indexOf 方法还可以接受第二个参数，表示搜索的开始位置。

```js
(1)[("a", "b", "c")].indexOf("a", 1); // -1
```

上面代码从 1 号位置开始搜索字符 a，结果为-1，表示没有搜索到。

toString():返回数组的字符串形式。

```js
1 var arr = [1, 2, 3];
2 arr.toString()     // "1,2,3"
3
4 var arr = [1, 2, 3, [4, 5, 6]];
5 arr.toString()     // "1,2,3,4,5,6"
```

4. join():以参数作为分隔符，将所有数组成员组成一个字符串返回。如果不提供参数，默认用逗号分隔。

```js
1 var arr = [1, 2, 3, 4];
2
3 arr.join(' ')     // '1 2 3 4'
4 arr.join(' | ')     // "1 | 2 | 3 | 4"
5 arr.join()     // "1,2,3,4"
```

5. concat():用于多个数组的合并。它将新数组的成员，添加到原数组的尾部，然后返回一个新数组，原数组不变。

```js
1 var arr = [1,2,3];
2 var b = arr.concat([4,5,6]);
3 console.log(b);        //[1,2,3,4,5,6]
```

6. reverse():用于颠倒数组中元素的顺序，返回改变后的数组。注意，该方法将改变原数组。

```js
1 var arr = ['a', 'b', 'c'];
2
3 arr.reverse() // ["c", "b", "a"]
4 console.log(arr) // ["c", "b", "a"]
```

7. slice():用于截取原数组的一部分，返回一个新数组，原数组不变。
   slice(start,end)它的第一个参数为起始位置（从 0 开始），第二个参数为终止位置（但该位置的元素本身不包括在内）。如果省略第二个参数，则一直返回到原数组的最后一个成员。

```js
 1 var arr = ['a', 'b', 'c'];
 2
 3 arr.slice(0)         // ["a", "b", "c"]
 4 arr.slice(1)         // ["b", "c"]
 5 arr.slice(1, 2)     // ["b"]
 6 arr.slice(2, 6)     // ["c"]
 7 arr.slice()           // ["a", "b", "c"]    无参数返回原数组
 8
 9 arr.slice(-2)          // ["b", "c"]    参数是负数，则表示倒数计算的位置
10 arr.slice(-2, -1)     // ["b"]
```

8. splice():删除原数组的一部分成员，并可以在被删除的位置添加入新的数组成员，返回值是被删除的元素。注意，该方法会改变原数组。
   splice(start,delNum,addElement1,addElement2,...)第一个参数是删除的起始位置，第二个参数是被删除的元素个数,第三个参数代表要替换的元素。如果后面还有更多的参数，则表示这些就是要被插入数组的新元素。

```js
1 var arr = ['a', 'b', 'c', 'd', 'e', 'f'];
2 arr.splice(4, 2)     // ["e", "f"]　　从原数组4号位置，删除了两个数组成员
3 console.log(arr)     // ["a", "b", "c", "d"]
```

```js
1 var arr = ['a', 'b', 'c', 'd', 'e', 'f'];
2 arr.splice(4, 2, 1, 2)     // ["e", "f"]　　原数组4号位置，删除了两个数组成员,又插入了两个新成员
3 console.log(arr)         // ["a", "b", "c", "d", 1, 2]
```

```js
1 var arr = ['a', 'b', 'c', 'd', 'e', 'f'];
2 arr.splice(-4, 2)     // ["c", "d"]    起始位置如果是负数，就表示从倒数位置开始删除
```

```js
1 var arr = [1, 1, 1];
2
3 arr.splice(1, 0, 2)     // []    如果只插入元素,第二个参数可以设为0
4 conlose.log(arr)     // [1, 2, 1, 1]
```

```js
1 var arr = [1, 2, 3, 4];
2 arr.splice(2)     // [3, 4] 如果只有第一个参数，等同于将原数组在指定位置拆分成两个数组
3 console.log(arr)     // [1, 2]
```

9. sort():对数组成员进行排序，默认是按照字典顺序排序。排序后，原数组将被改变。

```js
(1)[("d", "c", "b", "a")].sort();
2; // ['a', 'b', 'c', 'd']
3;
(4)[(4, 3, 2, 1)].sort();
5; // [1, 2, 3, 4]
6;
(7)[(11, 101)].sort();
8; // [101, 11]
9;
(10)[(10111, 1101, 111)].sort();
11; // [10111, 1101, 111]
```

上面代码的最后两个例子，需要特殊注意。sort 方法不是按照大小排序，而是按照对应字符串的字典顺序排序。也就是说，数值会被先转成字符串，再按照字典顺序进行比较，所以 101 排在 11 的前面。

如果想让 sort 方法按照自定义方式排序，可以传入一个函数作为参数，表示按照自定义方法进行排序。该函数本身又接受两个参数，表示进行比较的两个元素。如果返回值大于 0，表示第一个元素排在第二个元素后面；其他情况下，都是第一个元素排在第二个元素前面。

```js
 1 var arr = [10111, 1101, 111];
 2 arr.sort(function (a, b) {
 3   return a - b;
 4 })
 5 // [111, 1101, 10111]
 6
 7 var arr1 = [
 8               { name: "张三", age: 30 },
 9               { name: "李四", age: 24 },
10               { name: "王五", age: 28 }
11            ]
12
13 arr1.sort(function (o1, o2) {
14   return o1.age - o2.age;
15 })
16 // [
17 //   { name: "李四", age: 24 },
18 //   { name: "王五", age: 28 },
19 //   { name: "张三", age: 30 }
20 // ]
```

10. map():对数组的所有成员依次调用一个函数，根据函数结果返回一个新数组。

```js
1 var numbers = [1, 2, 3];
2
3 numbers.map(function (n) {
4   return n + 1;
5 });
6 // [2, 3, 4]
7
8 numbers
9 // [1, 2, 3]
```

上面代码中，numbers 数组的所有成员都加上 1，组成一个新数组返回，原数组没有变化。

11. filter():参数是一个函数，所有数组成员依次执行该函数，返回结果为 true 的成员组成一个新数组返回。该方法不会改变原数组。

```js
1 var arr = [1, 2, 3, 4, 5]
2 arr.filter(function (elem) {
3   return (elem > 3);
4 })
5 // [4, 5]
```

12. arr.forEach(item,index,array){} 遍历，循环 类似 jquery 的 each
    其中的 item 参数是数组中的内容，index 为其索引,array 表示数组本身

```js
var arr = [1, 2, 3, 4, 5];
arr.forEach(function(item, index, array) {});
```

13. 数组去重 ES6 提供了新的数据结构 Set。类似于数组，只不过其成员值都是唯一的，没有重复的值。

```js
//Array.from() 方法从一个类似数组或可迭代对象中创建一个新的数组实例。
console.log(Array.from("foo"));
//  Array ["f", "o", "o"]
var items = new Set([1, 2, 3, 4, 5, 2, 2, 2]);
//items Set(5) {1, 2, 3, 4, 5}
var array = Array.from(items);
//array [1, 2, 3, 4, 5]
```

14. ES6 之 Array.from()方法
    1、类数组对象：所谓类数组对象，最基本的要求就是具有 length 属性的对象。
    2、Array.from()方法就是将一个类数组对象或者可遍历对象转换成一个真正的数组。

```js
//例子1——将类数组转换为数组 (注意array对象必须要有length属性)
let array = {
  0: "name",
  1: "age",
  2: "sex",
  3: ["user1", "user2", "user3"],
  length: 4
};
let arr = Array.from(array);
console.log(arr); // ['name','age','sex',['user1','user2','user3']]
//例子
let array = {
  name: "name",
  age: "age",
  sex: "sex",
  user: ["user1", "user2", "user3"],
  length: 4
};
let arr = Array.from(array);
console.log(arr); // [ undefined, undefined, undefined, undefined ]
//由此可见，要将一个类数组对象转换为一个真正的数组，必须具备以下条件：
// （1）该类数组对象必须具有length属性，用于指定数组的长度。如果没有length属性，那么转换后的数组是一个空数组。
// （2）该类数组对象的属性名必须为数值型
```

15. reduce() 方法接收一个函数作为累加器，数组中的每个值（从左到右）开始缩减，最终计算为一个值。

    > array.reduce(function(total, currentValue, currentIndex, arr), initialValue)

```js
/*
        参数1.prev 上一次返回的值，
        参数2.item 本次的值，
        参数3.代表从数字几开始加
        默认数据是字符串拼接,这时候返回值也就是123456
        如果我们想做到里面的数组迭代相加，那我们在最后的参数传一个数字类型的参数，例如我们传0，这时候就按照数字相加，
        这里还需要注意的就是传的时候不能加" "如果加了引号还认为是字符串的拼接   
        */
let sum = [1, 2, 3, 4, 5, 6].reduce((prev, item) => {
  return prev + item;
}, 1); //sum = 222
```

16. Object.assign() 方法用于将所有可枚举属性的值从一个或多个源对象复制到目标对象。它将返回目标对象。

```js
//语法 Object.assign(target, ...sources) target目标对象 source源对象

const target = { a: 1, b: 2 };
const source = { b: 4, c: 5 };

const returnedTarget = Object.assign(target, source);

console.log(target);
// expected output: Object { a: 1, b: 4, c: 5 }

console.log(returnedTarget);
// expected output: Object { a: 1, b: 4, c: 5 }
//如果目标对象中的属性具有相同的键，则属性将被源对象中的属性覆盖。后面的源对象的属性将类似地覆盖前面的源对象的属性。
```

## 字符串常用方法:

1. substring(start 开始位置的索引,end 结束位置索引) 截取的位置不包含结束位置的字符,只写一个参数表示从开始位置截取到最后

```js
1. var str='abcdefg';
2. str.substring(1) //得到bcdefg  str.substring(1,3) //得到bc
```

2. slice(start 开始位置索引，end 结束位置索引) 基本和 substring 相似,区别在参数为负数時候。

```js
1. var str='abcdefg';
2. str.slice(1)  //bcdefg      str.substring(1,3) // bc
```

3. substr(start 开始位置索引,end 需要返回的字符个数)

```js
1. var str='abcdefg';
2. str.substr(1) //bcdefg      str.substr(1,1) //b
```

4. charAt(index) 方法返回指定索引位置处的字符。如果超出有效范围(0 与字符串长度减一)的索引值返回空字符串.

```js
1. var str='abcdefg';
2. str.charAt(2) // c
```

5. index(string) 返回 String 对象内第一次出现子字符串位置。如果没有找到子字符串，则返回-1

```js
 var str='abcdefga'  str.indexOf('a')  // 0   str.indexOf('h') //-1
```

6. lastIndexOf(string) 倒叙查找
   返回 String 对象内第一次出现子字符串位置。如果没有找到子字符串，则返回-1。

```js
var str='abcdefga'     str.lastIndexOf('a') // 7
```

7. split(str) 将字符串以参数分割为数组

```js
var str='abcadeafg'     str.split('a') //["", "bc", "de", "fg"]
```

8. toLowerCase 方法返回一个字符串，该字符串中的字母被转换成小写。

9. toUpperCase 方法返回一个字符串，该字符串中的所有字母都被转换为大写字母。

10. match() – 方法可在字符串内检索指定的值，或找到一个或多个正则表达式的匹配

11. search 方法返回与正则表达式查找内容匹配的第一个字符串的位置。

12. replace 用来查找匹配一个正则表达式的字符串，然后使用新字符串代替匹配
