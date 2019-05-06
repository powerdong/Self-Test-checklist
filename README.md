# Self-Test-checklist
本文引自掘金大神的自检清单问题，小白自行归纳总结

## 一、JavaScript基础
详情请点击[JavaScript 的数据类型及其检测](http://note.youdao.com/noteshare?id=90745a65f3ab66d6383c4c2174682017&sub=6EE107F89A5D46D19362566E68D39FAB "点击查看")  
  
Javascript 有两种数据类型，分别是基本数据类型和引用数据类型。其中基本数据类型包括 Undefined、Null、Boolean、Number、String、Symbol (ES6 新增，表示独一无二的值)，而引用数据类型统称为 Object 对象，主要包括对象、数组和函数。

### 基础数据类型
#### 1.值是不可变的
#### 2.存放在栈区
#### 3.值的比较

### 引用数据类型
#### 1.值是可变的
#### 2.同时保存在栈内存和堆内存
#### 3.比较是引用的比较

### 检验数据类型
#### 1.typeof
  typeof 返回一个表示数据类型的字符串，返回结果包括：number、boolean、string、symbol、object、undefined、function 等 7 种数据类型，但不能判断 null、array 等
  数组和对象返回的都是 object，这时就需要使用 instanceof 来判断
  ```
  typeof Symbol(); // symbol 有效
  typeof ''; // string 有效
  typeof 1; // number 有效
  typeof true; //boolean 有效
  typeof undefined; //undefined 有效
  typeof new Function(); // function 有效
  typeof null; //object 无效
  typeof [] ; //object 无效
  typeof new Date(); //object 无效
  typeof new RegExp(); //object 无效
  ```
#### 2.instanceof
  instanceof 是用来判断 A 是否为 B 的实例，表达式为：A instanceof B，如果 A 是 B 的实例，则返回 true,否则返回 false。instanceof 运算符用来测试一个对象在其原型链中是否存在一个构造函数的 prototype 属性。
  ```
  [] instanceof Array; //true
  {} instanceof Object;//true
  new Date() instanceof Date;//true
  new RegExp() instanceof RegExp//true
  ```
关于数组的类型判断，还可以用 ES6 新增Array.isArray()
  ```
  Array.isArray([]);   // true
  ```
#### 3.严格运算符===
  只能用于判断 null 和 undefined，因为这两种类型的值都是唯一的。
  undefined 还可以用 typeof 来判断
#### 4.constructor
  constructor 作用和 instanceof 非常相似。但 constructor 检测 Object 与 instanceof 不一样，还可以处理基本数据类型的检测。
