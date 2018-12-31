# Typescript 中的函数

## 函数的定义

- ES5 函数定义：函数声明、匿名函数、传参

```
// 函数声明
function fn1 () {
    return 123;
}
fn1(); // 调用

// 匿名函数
let fn2 = function () {
    console.log(456);
}
fn2();

// 传参
function fn3 (name, age) {
    return `姓名：${name}，年龄：${age}`;
}
fn3('张三', 25);
```

- ts 函数定义：函数声明、匿名函数、传参

```
// 函数声明
function fn1 ():number { // number 是函数返回值类型，没有返回值为 void
    return 123;
}
fn1();

// 匿名函数
let fn2 = function ():void {
    console.log(456);
}
fn2();

// 传参
function fn3 (name:string, age:number):string {
    return `姓名：${name}，年龄：${age}`;
}
fn3('张三', 25);
```

## 可选参数

ES5 里面方法的实参和行参可以不一样，但是 ts 中必须一样，如果不一样就需要配置可选参数。

**注意**：可选参数必须配置到参数的最后面

```
function getInfo (name:string, age?:number):string { // age 为可选参数
    if (age) {
        return `姓名：${name}，年龄：${age}`;
    } else {
        return `姓名：${name}，年龄：保密`;
    }
}
console.log(getInfo('张三', 23));
console.log(getInfo('李四'));
```

```
// 错误的写法
function getInfo (name?:string, age:number):string { // name 为可选参数
    if (name) {
        return `姓名：${name}，年龄：${age}`;
    } else {
        return `姓名：不知道，年龄：${age}`;
    }
}
console.log(getInfo('李四', 23));
```

## 默认参数

ES5 里面没法设置默认参数，ES6 和 ts 中都可以设置默认参数。

```
function getInfo (name:string, age:number=25):string { // age 默认为25
    if (age) {
        return `姓名：${name}，年龄：${age}`;
    } else {
        return `姓名：${name}，年龄：保密`;
    }
}
console.log(getInfo('张三', 23)); // 姓名：张三，年龄：23
console.log(getInfo('李四')); // 姓名：李四，年龄：25
```

## 剩余参数

ES6 中的三点运算符

```
function sum (a:number, b:number, ...nums:number[]):number {
    let sum = a + b;
    nums.forEach((n) => {
        sum += n;
    });
    return sum;
}
console.log(sum(1, 2, 3, 4, 5, 6)); // 21
```

## 函数重载

java 中方法的重载：重载指的是两个或者两个以上同名函数，但它们的参数不一样，这时会出现函数重载的情况。

Typescript 中的重载：通过为同一个函数提供多个函数类型定义来实现多种功能的目的。

ts 为了兼容 ES5 以及 ES6 重载的写法和 java 中有区别。

ES5 中出现同名方法，下面的会替换上面的方法。

```
function getInfo (name) {

}
function getInfo (name, age) {

}
```

ts 中的重载

```
// 单个参数，不同类型
function getInfo (name:string):string;
function getInfo (age:number):string;
function getInfo (str:any):any {
  if (typeof str === 'string') {
    return `姓名：${str}`;
  } else {
    return `年龄：${str}`;
  }
}
getInfo('张三');
getInfo(25);
getInfo(true); // 错误的写法
```

```
// 多个参数，可选参数
function getInfo (name:string):string;
function getInfo (name:string, age:number):string;
function getInfo (name:string, age?:number):string {
  if (age) {
    return `姓名：${str}，年龄：${str}`;
  } else {
    return `姓名：${str}`;
  }
}
getInfo('张三');
getInfo(25); // 错误
getInfo('李四', 26);
```

## 箭头函数

同 ES6 中一样，修复 this 指向的问题，箭头函数里面的 this 指向上下文，即外层第一个不为箭头函数的 this。
