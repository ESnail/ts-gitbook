# Typescript 中的接口

> 接口的作用：在面向对象的编程中，接口是一种规范的定义，它定义了行为和动作的规范，在程序设计里面，接口起到一种限制和规范的作用。接口定义了某一批类所需要遵守的规范，接口不关心这些类的内部状态数据，也不关心这些类里方法的实现细节，它只规定这批类里必须提供某些方法，提供这些方法的类就可以满足实际需要。

> Typescrip 中的接口类似于 java，同时还增加了更灵活的接口类型，包括属性、函数、可索引和类等。

> 定义标准。

## 属性类接口
对 对象属性 的约束。

ts 中属性对象传参，对方法传入的对象及属性进行约束。
```
function printLabel (label: {label:string}):void {
  console.log(`print label：${label.label}`);
}
printLabel({label: '标签'}); // 必须传入带有label属性，且属性值是字符串的对象
// printLabel({label: '标签', name: 'text'}); // 错误
// printLabel({name: '标签'}); // 错误
// printLabel('标签'); // 错误
```

接口：行为和动作的规范，对批量方法传入参数进行约束。

用关键字`interface`定义，用分号结束。约定接口名首字母大写。
```
interface FullName {
  firstName:string; // 注意，用分号结束
  secondName:string; 
}

function printName (name:FullName):void {
  // 必须传入对象，且带有属性：firstName，secondName，且属性值都是字符串
  console.log(`${name.firstName} -- ${name.secondName}`);
}
printName({firstName:'张', secondName: '三'}); // 必须带有 firstName，secondName
// printName({firstName:'张', secondName: '三', name: '张三'}); // 错误 只能带有 firstName，secondName

const nameObj = {firstName:'张', secondName: '三', name: '张三', age: 20};
printName(nameObj); // 正确，这种方式，可以传额外的，但是 firstName、secondName 必须有

printName({ // 参数的顺序可以不一样
  secondName: '四',
  firstName: '李'
})

function getName (name:FullName):string {
  return `${name.firstName} -- ${name.secondName}`;
}
getName({firstName:'张', secondName: '三'});
```

接口，可选属性
```
interface FullName {
  firstName:string;
  secondName?:string; // ? 代表可选
}
printName({firstName:'张'});
```

## 函数类型接口
对方法传入的参数以及返回值进行约束，批量约束。

```
interface Encrytp {
  (key:string, val:string):string;
}

let md5:Encrytp = function (key:string, val:string):string {
  // 具体加密省略
  return key + val;
}
console.log(md5('name', 'Jane')); // nameJane

let hash:Encrytp = function (key:string, val:string):string {
  // 具体加密省略
  return key + ' ---- ' + val;
}
console.log(hash('name', 'Jane')); // name ---- Jane
```

## 可索引接口
对数组、对象的约束（不常用）

ts 中数组的两种定义方式：
```
let arr1:Array<number> = [1, 2];
let arr2:string[] = ['12', '23'];
```
ts 中可索引接口，对数组的约束
```
interface userArr {
  [index:number]:string;
}
let arr3:userArr = ['a', 'b'];
console.log(arr3[0]);
// let arr4:userArr = [12, 34]; // 错误
```
ts 中可索引接口，对对象的约束
```
interface userObj {
  [index:string]:string;
}
let obj1:userObj = {name: 'Jane'};
// let obj2:userObj = {age: 12}; // 错误
```

## 类类型接口
对类的约束，和抽象类有点相似。类类型接口实现用关键字`implements`

```
interface Animal {
  name:string;
  eat (food:string):void;
}

class Dog implements Animal { // 类类型接口实现用关键字 implements
  name:string;

  constructor (name:string) {
    this.name = name;
  }

  eat (food:string):void {
    console.log(`${this.name}喜欢吃${food}`);
  }
}
let d = new Dog('小黑');
d.eat('骨头'); // 小黑喜欢吃骨头

class Cat implements Animal {
  name:string;

  constructor (name:string) {
    this.name = name;
  }

  eat (food:string):void {
    console.log(`${this.name}喜欢吃${food}`);
  }
}
let c = new Cat('小白');
c.eat('老鼠'); // 小白喜欢吃老鼠
```

## 接口扩展

接口可以继承接口
```
interface Animal {
  eat ():void;
}
interface Person extends Animal {
  work ():void;
}
class Web implements Person {
  name:string;
  constructor (name:string) {
    this.name = name;
  }
  // 接口 Animal 中的方法必须实现
  eat ():void {
    console.log(`${this.name}喜欢吃甜点`);
  }
  // 接口 Person 中的方法必须实现
  work ():void {
    console.log(`${this.name}在运动`);
  }
}
let w = new Web('小李');
w.eat();
w.work();
```

继承类并实现接口
```
interface Animal {
  eat ():void;
}
interface Person extends Animal {
  work ():void;
}

class Programmer {
  name:string;
  constructor (name:string) {
    this.name = name;
  }

  coding () {
    console.log(`${this.name}在写代码`);
  }
}

class Web extends Programmer implements Person {

  constructor (name:string) {
    super(name);
  }
  // 接口 Animal 中的方法必须实现
  eat ():void {
    console.log(`${this.name}喜欢吃甜点`);
  }
  // 接口 Person 中的方法必须实现
  work ():void {
    console.log(`${this.name}在运动`);
  }
}
let w = new Web('小李');
w.eat();
w.work();
w.coding(); // 小李在写代码
```