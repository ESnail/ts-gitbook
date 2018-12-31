# Typescript 中的数据类型

## 前言

typescript中为了使编写的代码更规范，更有利于维护，增加了类型校验，写 ts 代码必须指定类型。

在typescript中主要给我们提供了以下数据类型:

- boolean（布尔类型）
- number（数字类型）
- string（字符串类型）
- array（数组类型）
- tuple（元组类型）
- enum（枚举类型）
- any（任意类型）
- null 和 undefined 类型
- void 类型
- never 类型
- object 对象类型

## boolean（布尔类型）
- ES5 的写法：
```
var flag = true;
flag = 456;
```
- ts 写法：以上的 ES5 写法到了 ts 中就变成了错误的写法，因为将一个 number 类型值赋给了一个 Boolean 的变量。
```
let flag:boolean = true;
// flag = 123; // 错误
flag = false;  //正确
```

## number（数字类型）
- ES5 的写法：
```
var num = 123;
num = 456;
```
- ts 写法：
```
let num:number = 123;
// num = '456'; // 错误
num = 456;  //正确
```

## string（字符串类型）
- ES5 的写法：
```
var str = 'this is ts';
str = 'test';
```
- ts 写法：
```
let str:string = 'this is ts';
str = 'test';
```

## array（数组类型）
- ES5 的写法：
```
var arr = ['12', '23'];
arr = [34, 45];
```
- ts 写法1：
```
let arr:string[] = ['12', '23'];
arr = ['45', '56'];
```
- ts 写法2：
```
let arr:Array<number> = [1, 2];
arr = ['45', '56'];
```

## tuple（元组类型）:属于数组的一种
```
let tupleArr:[number, string, boolean] = [12, '34', true];
```
赋值的类型、位置、个数需要和定义（生明）的类型、位置、个数一致。

## enum（枚举类型）

随着计算机的不断普及，程序不仅只用于数值计算，还更广泛地用于处理非数值的数据。
例如：性别、月份、星期几、颜色、单位名、学历、职业等，都不是数值数据。在其它程序设计语言中，一般用一个数值来代表某一状态，这种处理方法不直观，易读性差。

如果能在程序中用自然语言中有相应含义的单词来代表某一状态，则程序就很容易阅读和理解。
也就是说，事先考虑到某一变量可能取的值，尽量用自然语言中含义清楚的单词来表示它的每一个值，
这种方法称为枚举方法，用这种方法定义的类型称枚举类型。

定义：
```
enum 枚举名 { 
    标识符[=整型常数], 
    标识符[=整型常数], 
    ... 
    标识符[=整型常数]
};  
```

举例：
```
enum statusCode {
  success,
  fail,
  pending
};
let res:statusCode = statusCode.success;
console.log(res); // 0，如果标识符没有赋值，它的值就是下标，默认从 0 开始
```
```
enum statusCode {
  success = 2,
  fail,
  pending
};
let res1:statusCode = statusCode.success;
console.log(res1) // 2，指定的值
let res3:statusCode = statusCode.fail;
console.log(res1) // 3，若没指定，从指定的往后开始
```
```
enum statusCode {
  success = 2,
  fail = 1,
  pending = 3
};
let res1:statusCode = statusCode.success;
console.log(res1) // 2，指定的值
let res3:statusCode = statusCode.fail;
console.log(res1) // 1，指定的值，可随意指定
```

## any（任意类型）

表示可以指定任何类型的值。一般用于声明 dom 节点。

```
let num:any = 123;
num = 'str';
num = true;
```
```
let boxEl:object = document.getElementById('box'); // 错误，dom 节点不是真正的对象
let boxEl:any = document.getElementById('box'); // 正确
boxEl.style.color = 'pink';
```

## null 和 undefined 类型

默认情况下null和undefined是所有类型的子类型。 就是说你可以把 null 和 undefined 赋值给 number 类型的变量。

一般用于可能为 undefined 或 null 的变量。

- undefined: 定义没有赋值就是 undefined

```
let num:number;
console.log(num); // 输出：undefined 报错

let num:undefined;
console.log(num); // 输出：undefined 正确
```

```
let num:number | undefined; // | 表示或者
console.log(num); // 正确
num = 123;
console.log(num); // 正确
```

- null
```
let num:null;
num = null;
```

- 一个变量可能是 number 类型，可能是 null，可能是 undefined
```
let num:number | null | undefined;
num = 1234;
```

## void 类型

typescript 中的 void 表示没有任何类型，一般用于定义方法的时候方法没有返回值。

- ES5 的写法：
```
function fn () {
  console.log('fn');
}
fn();
```

- ts 的写法：

无返回值
```
function fn ():void { // 正确的写法
  console.log('fn);
}
fn();

function fn ():undefined { // 错误的写法
  console.log('fn);
}
fn();
```
函数没有返回值的时候，只能为 void，不能为 undefined。

有返回值
```
function fn ():number {
  return 123;
}
console.log(fn());
```

## never 类型

typescript 中的 never 是其他类型 （包括 null 和 undefined）的子类型，可以赋值给任何类型，代表从不会出现的值。但是没有类型是 never 的子类型，这意味着声明 never 的变量只能被 never 类型所赋值。

never 类型一般用来指定那些总是会抛出异常或根本就不会有返回值的函数表达式或箭头函数表达式的返回值类型。

```
let a:never;
a = 123; // 错误的写法

a = (() => { // 正确的写法
  throw new Error('错误');
})()
```

## object 对象类型

```
let obj:object;
obj = {name: 'Wang', age: 25};
```