# Es5 中的类

## 最简单的类
```
function Person (name, age) { // 构造函数
  this.name = name; // 属性
  this.age = age;
}
var p = new Person('张三', 25); // 实例化对象，p 为 Person 的一个实例
console.log(p.name);
```
函数名首字母大写，函数内用 this 处理的函数称为构造函数。

用 new 关键字实例化构造函数的变量是该构造函数的实例。

## 类定义属性和方法
可以在构造函数和原型链上定义属性和方法。
```
function Person (name, age) {
  // 构造函数内定义属性和方法
  this.name = name; // 实例属性
  this.age = age;

  this.run = function () { // 实例方法
    console.log(this.name + '在运动');
  }
}
// 原型链上定义属性和方法
Person.prototype.sex = '男';
Person.prototype.work = function () {
  console.log(this.name + '在工作');
}

var p = new Person('张三', 25);
p.run(); // 调用实例方法
p.work();
```
原型链上面的属性会被多个实例共享，构造函数里的属性不会

## 类的静态属性和方法
直接给构造函数设置属性和方法，不需要实例化即可获得的。

构造函数内的属性和方法，原型链上的属性和方法都需要实例化之后才可获得。

```
function Person (name, age) {
  // 构造函数内定义属性和方法
  this.name = name; // 属性
  this.age = age;

  this.run = function () { // 方法
    console.log(this.name + '在运动');
  }
}

// 静态属性、方法
Person.address = 'xxx';
Person.getInfo = function () {
  console.log('静态方法');
}
// 调用
console.log(Person.address);
Person.getInfo();
Person.run(); // 错误，只有实例对象才可调用

var p = new Person();
p.run();
```

## 继承：对象冒充实现
对象冒充可以继承构造函数里面的属性和方法，但是没法继承原型链上面的属性和方法
```
// 父类
function Person (name, age) {
  this.name = name;
  this.age = age;

  this.run = function () {
    console.log(this.name + '在运动');
  }
}
Person.prototype.sex = '男';
Person.prototype.work = function () {
  console.log(this.name + '在工作');
}

// 子类继承父类
function Child () {
  Person.call(this); // 对象冒充实现继承
}


var c = new Child('张三', 25);
c.run();
c.work(); // 错误，没有 work 方法
```

## 继承：原型链实现
原型链继承：可以继承构造函数里面的属性和方法，也可以继承原型链上面的属性和方法。但是实例化子类的时候没法给父类传参。
```
// 父类
function Person (name, age) {
  this.name = name;
  this.age = age;

  this.run = function () {
    console.log(this.name + '在运动');
  }
}
Person.prototype.sex = '男';
Person.prototype.work = function () {
  console.log(this.name + '在工作');
}

// 子类继承父类
function Child (name, age) {

}
Child.prototype = new Person(); // 原型链实现继承

var c = new Child('张三', 25);
c.run(); // undefined 在运动
c.work(); // undefined 在工作
```

## 继承：原型链+对象冒充的组合继承模式
原型链继承：可以继承构造函数里面的属性和方法，也可以继承原型链上面的属性和方法。但是实例化子类的时候没法给父类传参。
```
// 父类
function Person (name, age) {
  this.name = name;
  this.age = age;

  this.run = function () {
    console.log(this.name + '在运动');
  }
}
Person.prototype.sex = '男';
Person.prototype.work = function () {
  console.log(this.name + '在工作');
}

// 子类继承父类
function Child (name, age) {
  Person.call(this, name, age); // 对象冒充继承，实例化子类可以给父类传参
}
Child.prototype = new Person(); // 原型链实现继承，继承原型链上的属性和方法
// 或者
// Child.prototype = Person.prototype; // 原型链实现继承，继承原型链上的属性和方法

var c = new Child('张三', 25);
c.run(); // 张三在运动
c.work(); // 张三在工作
```