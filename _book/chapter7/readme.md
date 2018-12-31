# Typescript 中的泛型

## 泛型的定义
泛型：软件工程中，我们不仅要创建一致的定义良好的 API，同时也要考虑可重用性。 组件不仅能够支持当前的数据类型，同时也能支持未来的数据类型，这在创建大型系统时为你提供了十分灵活的功能。

在像C#和Java这样的语言中，可以使用泛型来创建可重用的组件，一个组件可以支持多种类型的数据。这样用户就可以以自己的数据类型来使用组件。

通俗理解：泛型就是解决**类**、**接口**、**方法**的复用性、以及对不特定数据类型的支持(类型校验)。

```
function getData (val:string):string {
  return val;
}
```
只能返回string类型的数据，要求能同时返回 string 类型和 number 类型
```
function getData1 (val:string):string {
  return val;
}
function getData2 (val:number):number {
  return val;
}
```
代码冗余，any 类型可以解决这个问题。
```
function getData (val:any):any {
  return val;
}
getData(124);
getData('124');
```
但是 any 相当于放弃了类型检查。没法实现传入什么，返回什么。比如:传入 number 类型必须返回 number 类型，传入 string 类型必须返回 string 类型。
```
function getData (val:any):any {
  return val + '---';
}
getData(124); // 传入 number，返回 string
```

泛型：可以支持不特定的数据类型。要求：传入的参数和返回的参数一致。

`T`表示泛型，具体什么类型是在调用这个方法的时候决定的

## 泛型函数
```
function getData<T> (val:T):T {
  return val;
}
getData<number>(124);
getData<string>('abc');
// getData<number>('abc'); // 错误
```
放回值可以是任意类型
```
function getData<T> (val:T):any {
  return val + '***';
}
getData<number>(124); // 参数必须是数字
getData<string>('abc');
```

## 泛型类
比如有个最小堆算法，需要同时支持返回数字和字符串 a-z 两种类型。通过类的泛型来实现
```
class minClass {
  list:number[] = [];

  add (val:number):void {
    this.list.push(val);
  }

  min ():number {
    let minNum:number = this.list[0];
    for(let i = 0; i < this.list.length; i++) {
      if(minNum > this.list[i]){
          minNum = this.list[i];
      }
    }
    return minNum;
  }
}
let m = new minClass();
m.add(3);
m.add(2);
m.add(23);
console.log(m.min()); // 2
```
正常的类只能实现一种类型。用泛型解决，支持 number 和 string。
```
class minClass<T> {
  list:T[] = [];

  add (val:T):void {
    this.list.push(val);
  }

  min ():T {
    let minNum = this.list[0];
    for(let i = 0; i < this.list.length; i++) {
      if(minNum > this.list[i]){
          minNum = this.list[i];
      }
    }
    return minNum;
  }
}
let m1 = new minClass<number>(); // 实例化类，并且指定了类的 T 代表的类型是 number
m1.add(3);
m1.add(2);
m1.add(23);
console.log(m1.min()); // 2

let m2 = new minClass<string>(); // 实例化类，并且指定了类的 T 代表的类型是 string
m2.add('a');
m2.add('d');
m2.add('f');
console.log(m2.min()); // a
```

## 泛型接口
函数类型接口
```
interface configFn {
  (val1:string, val2:string):string;
}
let setData:configFn = function (value1:string, value2:string):string { // 参数名可以和接口中的不一致，但是参数类型必须一致
  return value1 + value2;
}
setData('1', '2');
```
泛型接口实现方式1：
```
interface configFn {
  <T>(val:T):T;
}
let getData:configFn = function<T> (value:T):T {
  return value;
}
getData<string>('abc');
getData<number>(123);
```
泛型接口实现方式2：
```
interface configFn<T> {
  (val:T):T;
}
let getData:configFn<string> = function<T> (value:T):T {
  return value;
}
getData('abc');
getData(123); // 错误
```