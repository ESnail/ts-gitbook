# Typescript 中的类

## 类的定义

- ES5 中定义：

```
function Person (name) {
  this.name=name;
  this.run = function () {
    console.log(this.name)
  }
}

var p = new Person('张三');
p.run();
```

- ts 中定义：
使用`class`关键词。
```
class Person {
  name:string; // 属性，前面省略了 public 关键词
  
  constructor (name:string) { // 构造函数，实例化类的时候触发的方法
    this.name = name;
  }

  run ():void {
    console.log(`${this.name}在运动`);
  }

  getName ():string {
    return this.name;
  }

  setName (name:string):void {
    this.name = name;
  }
}
let p = new Person('李四');
p.run();
p.setName('王五');
console.log(p.getName());
```

## 继承
使用关键词`extends`、`super`。

```
// 父类
class Person {
  name:string; // 属性，前面省略了 public 关键词
  
  constructor (name:string) { // 构造函数，实例化类的时候触发的方法
    this.name = name;
  }

  run ():void {
    console.log(`${this.name}在运动`);
  }
}
let p = new Person('李四');
p.run(); // 李四在运动

// 子类继承父类
class Child extends Person {
  constructor (name:string) {
    super(name); // 初始化父类的构造函数
  }
}
let c = new Child('周六');
c.run(); // 周六在运动
```

父类的方法和子类的方法一致，子类会执行子类自己的方法

```
// 父类
class Person {
  name:string; // 属性，前面省略了 public 关键词
  
  constructor (name:string) { // 构造函数，实例化类的时候触发的方法
    this.name = name;
  }

  run ():void {
    console.log(`${this.name}在运动`);
  }
}
let p = new Person('李四');
p.run(); // 李四在运动

// 子类继承父类
class Child extends Person {
  constructor (name:string) {
    super(name); // 初始化父类的构造函数
  }

  run ():void {
    console.log(`${this.name}在运动--子类`);
  }

  work ():void {
    console.log(`${this.name}工作--子类`);
  }
}
let c = new Child('周六');
c.run(); // 周六在运动--子类
c.work(); // 周六在工作--子类
```

## 类里面的修饰符
Typescript 里面定义属性的时候给我们提供了三种修饰符：
- public：公有，在当前类里面、子类、类外面都可以访问
- protected：保护类型，在当前类里面、子类里面可以访问，在类外部没法访问
- private：私有，在当前类里面可以访问，子类、类外部都没法访问
属性如果不加修饰符，默认就是公有（public）

- public：公有，在当前类里面、子类、类外面都可以访问

```
class Person {
  public name:string; // 公有
  
  constructor (name:string) {
    this.name = name;
  }

  run ():void {
    console.log(`${this.name}在运动`); // 在类里能访问
  }
}
let p = new Person('李四');
p.run();
console.log(p.name); // 在类外面能访问

class Child extends Person {
  constructor (name:string) {
    super(name);
  }

  run ():void {
    console.log(`${this.name}在运动--子类`); // 子类能访问
  }
}
let c = new Child('周六');
c.run(); // 周六在运动--子类
console.log(c.name); // 在类外面能访问
```

- protected：保护类型，在当前类里面、子类里面可以访问，在类外部没法访问

```
class Person {
  protected name:string; // 保护
  
  constructor (name:string) {
    this.name = name;
  }

  run ():void {
    console.log(`${this.name}在运动`); // 在类里能访问
  }
}
let p = new Person('李四');
p.run();
// console.log(p.name); // 报错，在类外面不能访问

class Child extends Person {
  constructor (name:string) {
    super(name);
  }

  run ():void {
    console.log(`${this.name}在运动--子类`); // 子类能访问
  }
}
let c = new Child('周六');
c.run(); // 周六在运动--子类
// console.log(c.name); // 报错，在类外面能访问
```

- private：私有，在当前类里面可以访问，子类、类外部都没法访问

```
class Person {
  private name:string; // 私有
  
  constructor (name:string) {
    this.name = name;
  }

  run ():void {
    console.log(`${this.name}在运动`); // 在类里能访问
  }
}
let p = new Person('李四');
p.run();
// console.log(p.name); // 报错，在类外面不能访问

class Child extends Person {
  constructor (name:string) {
    super(name);
  }

  run ():void {
    // console.log(`${this.name}在运动--子类`); // 报错，子类能访问
  }
}
let c = new Child('周六');
c.run(); // 周六在运动--子类
// console.log(c.name); // 报错，在类外面能访问
```

## 静态属性 静态方法
- ES5

```
function Person (name) {
  this.name = name;
}
Person.age = 24; // 静态属性
Person.run = function () { // 静态方法
  console.log(Person.age);
}
Person.run(); // 静态方法的调用
```

- jquery

```
$('#box').css('color', 'red'); // 实例方法
$.get('url', function () { // 静态方法

})

$(element) { // 实例
  return new Base(element);
}
$.get = function (url, callback) { // 静态方法

}
function Base (element) {
  this.element = element;
  this.css = function (attr, value) {
    this.element.style[attr] = value;
  }
}
```

- ts

```
class Person {
  public name:string; // 公有
  public age:number = 25;

  static sex:string = 'man'; // 静态属性

  constructor (name:string) {
    this.name = name;
  }

  public run ():void { // 公有方法
    console.log(`${this.name}在运动`); // 在类里能访问
  }

  // 静态方法
  static print ():void {
    console.log(`静态方法，性别：${Person.sex}`);
  }
}
// 静态属性和方法的调用
console.log(Person.sex);
Person.print(); // 静态方法，性别：man
```

## 多态
多态：父类定义一个方法不去实现，让继承它的子类去实现，每一个子类有不同的表现。

多态属于继承。

```
class Animal {
  name:string;

  constructor (name:string) {
    this.name = name;
  }

  eat () { // 具体吃什么,不知道。具体吃什么，由继承它的子类去实现，每一个子类的表现不一样
    console.log('吃的方法');
  }
}

class Dog extends Animal {
  constructor (name:string) {
    super(name);
  }

  eat () { // 子类实现父类的 eat 方法
    console.log(`${this.name}喜欢吃骨头`);
  }
}

class Cat extends Animal {
  constructor (name:string) {
    super(name);
  }

  eat () { // 子类实现父类的 eat 方法
    console.log(`${this.name}喜欢吃老鼠`);
  }
}
```

## 抽象类
- Typescript 中的抽象类：它是提供其他类继承的基类，不能直接被实例化。
- 用`abstract`关键字定义抽象类和抽象方法，抽象类中的抽象方法不包含具体实现并且必须在派生类（子类）中实现。
- abstract 抽象方法只能放在抽象类里面。
- 抽象类和抽象方法用来定义标准。比如：标准：Animal 这个类要求它的子类必须包含eat 方法。

```
// 抽象类，标准
abstract class Animal {
  name:string;

  constructor (name:string) {
    this.name = name;
  }

  abstract eat ():any; // 抽象方法不包含具体实现并且必须在派生类中实现。
}
// let animal = new Animal(); // 错误，抽奖类不能被实例化

class Dog extends Animal {
  constructor (name:string) {
    super(name);
  }

  eat () { // 抽象类的子类必须实现抽象类里面的抽象方法
    console.log(`${this.name}喜欢吃骨头`);
  }
}
let dog = new Dog('小黑');
dog.eat();
```
