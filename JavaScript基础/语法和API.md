## 目录

1. **[理解 ECMAScript 和 JavaScript 的关系](#理解-ecmascript-和-javascript-的关系)**
1. **[掌握 JavaScript 提供的全局对象、全局函数、全局属性](#掌握-javascript-提供的全局对象全局函数全局属性)**
1. **[应用 map、reduce、filter 等高阶函数解决问题](#应用-mapreducefilter-等高阶函数解决问题)**
1. **[setInterval 需要注意的点,使用 settimeout 实现 setInterval](#setinterval-需要注意的点使用-settimeout-实现-setinterval)**
1. **[JavaScript 提供的正则表达式 API、可以使用正则表达式解决常见问题](#javascript-提供的正则表达式-api可以使用正则表达式解决常见问题)**
1. **[JavaScript 异常处理的方式,统一的异常处理方案](#javascript-异常处理的方式统一的异常处理方案)**

### 理解 ECMAScript 和 JavaScript 的关系

- **Ecma International**
  - 一个制定技术标准的组织
- **ECMA-262**
  - 由 Ecma International 发布。它包含了脚本语言的标准。
  - 不妨把 ECMA-262 看做 ECMAScript 的编号。
- **ECMAScript**
  - 由 ECMA-262 制定的标准,用于实现通用的脚本语言。
  - ECMAScript 提供了脚本语言需要遵守的规则、细节和规范
- **JavaScript**
  - 通用脚本编程语言,它遵循了 ECMAScript 标准
    - 换句话说,JavaScript 是 ECMAScript 的方言。
- **JavaScript 引擎**
  - 理解并执行 JavaScript 代码的解释器
  - 浏览器中会有 JavaScript 引擎,比如 Chrome 有 V8,Firefox 有 SpiderMonkey,Edge 有 Chakra。JavaScript 引擎处理 JavaScript 代码,类似于人对语言的处理。
- **浏览器性能差异**
  - 两个浏览器都可以理解 JavaScript 代码,但是其中一个浏览器会快一些,因为它的 JavaScript 引擎的实现方式更加高效。
- **浏览器支持差异**
  - 尽管浏览器的 JavaScript 引擎都能理解 JavaScript,但是有些浏览器的理解能力更强 ,它们对 JavaScript 的支持是不一样的。
- **ECMAScript 6**
  - ECMA-262 的第六个版本(同义词：ES6、ES2015andECMAScript 2015)
- **先有鸡还是先有蛋**
  - JavaScript 是 1996 年创造的,它在 1997 年提交给 Ecma International,因此才有了 ECMAScript。同时 JavaScript 遵循 ECMAScript 标准,因此 JavaScript 是 ECMAScript 的实例。
  - 因此：ECMAScript 是基于 JavaScript 的,而 JavaScript 也是基于 ECMAScript 的,两个密不可分。

[:arrow_up:返回目录](#目录)

### 掌握 JavaScript 提供的全局对象、全局函数、全局属性

**JavaScript 全局对象**
`全局属性和函数可用于所有内建的JavaScript对象。`

**全局对象的描述**

> 1. 全局对象是预定义的对象,作为 JavaScript 的全局函数和全局属性的占位符。通过使用全局对象,可以访问所有其他所有预定义的对象、函数和属性。全局对象不是任何对象的属性,所以它没有名称。

> 2. 在顶层 JavaScript 代码中,可以用关键字 this 引用全局对象。但通常不必用这种方式引用全局对象,因为全局对象是作用域链的头,这意味着所有非限定性的变量和函数名都会作为该对象的属性来查询。例如,当 JavaScript 代码引用 parseInt() 函数时,它引用的是全局对象的 parseInt 属性。全局对象是作用域链的头,还意味着在顶层 JavaScript 代码中声明的所有变量都将成为全局对象的属性。

> 3. 全局对象只是一个对象,而不是类。既没有构造函数,也无法实例化一个新的全局对象。

> 4. 在 JavaScript 代码嵌入一个特殊环境中时,全局对象通常具有环境特定的属性。实际上,ECMAScript 标准没有规定全局对象的类型,JavaScript 的实现或嵌入的 JavaScript 都可以把任意类型的对象作为全局对象,只要该对象定义了这里列出的基本属性和函数。例如,在允许通过 LiveConnect 或相关的技术来脚本化 Java 的 JavaScript 实现中,全局对象被赋予了这里列出的 java 和 Package 属性以及 getClass() 方法。而在客户端 JavaScript 中,全局对象就是 Window 对象,表示允许 JavaScript 代码的 Web 浏览器窗口。

#### 总结：

1. 全局环境的 this 会指向全局对象 window,此时 this===window;
1. 全局变量会挂载在 window 对象下,会成为 window 下的一个属性。
1. 如果你没有使用严格模式并给一个未声明的变量赋值的话,JS 会自动创建一个全局变量。

[:arrow_up:返回目录](#目录)

### 应用 map、reduce、filter 等高阶函数解决问题

#### 高阶函数 Higher-order function

- 至少满足以下条件：
  - 函数可以作为参数被传递
  - 函数可以作为返回值被输出

常见的高阶函数有：`Map`、`Reduce`、`Filter`、`Sort`;

1. **Map**

```javascript
array.map(function(ele, index, arr) {}, thisValue); //浅克隆
```

> map()不会改变原数组

> 用变量接收返回值,可以用做浅克隆

---

```javascript{.line-number}
/**
 * 深度克隆
 * @param {*} Target 目标对象
 * @param {*} Option 克隆源
 */
function deepClone(Target, Option) {
  if (Option != null) {
    for (var prop in Option) {
      var src = Target[prop];
      var copy = Option[prop];
      if (copy && typeof copy == "object") {
        if (Object.prototype.toString.call(copy) == "[object Array]") {
          src = [];
        } else {
          src = {};
        }
        Target[prop] = deepClone(src, copy);
      } else {
        Target[prop] = copy;
      }
    }
  }
  return Target;
}
```

1. **reduce**

```javascript
array.reduce(function(preValue, ele, index, arr), initialValue)

//initialValue :传初始值;
// 如果不传,第一次pre打印数值第一位,ele是第二位
```

> reduce()对于空数组是不会执行回调函数

> 累加器
> return preValue + ele;

```javascript{.line-number}
/**
*底层实现
/

Array.prototype.Reduce = function(func,init){
    var previous = init,
        k = 0;
    if(init === undefined){
        previous = this[0];
        k = 1; 
    }
    for(k; k<this.length; k++){
        previous = func(previous, this[k], k);
    }
    return previous;
}
```

1. **filter**

```javascript
array.filter(function(ele,index,arr){}, thisValue)
```

> filter()不会改变原始数组

> 筛选出符合条件的项,组成新数组

```javascript{.line-number}
/**
*底层实现
/

Array.prototype.Filter = function(func){
    var arr = [];
    for(var i = 0; i<this.length; i++){
        if(func(this[i], i){
            arr.push(this[i]);
        };
    }
    return arr;
}
```

1. **forEach**

```javascript
array.forEach(function(ele,index,arr){}, thisValue)
```

> 原数组不变,无返回值

> map()与forEach()语法一致,能用forEach()做到的,map()同样可以,但是存在区别。

- 区别：
    - forEach()返回值undefined,不可以链式调用；
    - map()返回一个新数组,原数组不会改变。

```javascript{.line-number}
/**
*底层实现
/

Array.prototype.ForEach = function(func){
    for(var i = 0; i<this.length; i++){
        func(this[i], i){
    }
}
```
[:arrow_up:返回目录](#目录)

### setInterval 需要注意的点,使用 settimeout 实现 setInterval

#### 精准问题
setTimeout的问题在于它并不是精准的,例如使用setTimeout设定一个任务在10ms后执行,但是在9ms后,有一个任务占用了5ms的cpu时间片,再次轮到定时器执行时,时间已经过期了4ms。
setInterval存在两个问题：
  1. 时间间隔可能会跳过
  1. 时间间隔可能小于定时器设定的时间

#### 需要注意的点

- setTimeout有最小时间间隔限制,HTML5标准为4ms,小于4ms按照4ms处理,但是每个浏览器实现的最小间隔都不同
- 因为JS引擎只有一个线程,所以他将会强制异步事件排队执行
- 如果setInterval的回调执行时间长于指定的延迟,setInterval将无间隔的一个接一个执行
- this的指向问题可以通过bind函数,定义变量,箭头函数的方式来解决

#### 区别

setTimeout含义是定时器,到达一定的时间触发一次,但是setInterval含义是计时器,到达一定时间触发一次,并且会持续触发

#### 相互之间的转换

```javascript{.line-numbers}
function run(){
  setTimeout(function(){
    run();
  },1000);
}

setInterval(function(){
  run();
},1000);
```
[:arrow_up:返回目录](#目录)

### JavaScript 提供的正则表达式 API、可以使用正则表达式解决常见问题

详情请点击[正则表达式](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions "点击查看")

[:arrow_up:返回目录](#目录)

### JavaScript 异常处理的方式,统一的异常处理方案

详情请点击[异常处理的方式](https://segmentfault.com/a/1190000011481099 "点击查看")

由于JavaScript引擎是单线程的,因此一旦遇到异常,JavaScript引擎通常会停止执行,阻塞后续代码并抛出一个异常信息,因此对于可预见的异常,我们应该捕捉并正确展示给用户或开发者。

#### Error对象

``throw``和``Promise.reject()``可以抛出字符串类型的异常,而且可以抛出一个``Error``对象类型的异常。
一个``Error``对象类型的异常不仅包含一个异常信息,同时也包含一个追溯栈,这样你就可以很容易通过追溯栈找到代码出错的行数了。

```javascript{.line-numbers}
//创建自己的异常构造函数
function MyError(message){
  var instance = new Error(message);
  instance.name = 'MyError';
  Object.setPrototypeOf(instance, Object.getPrototypeOf(this));
  return instance;
}

MyError.prototype = Object.create(Error.prototype,{
  constructor:{
    value:MyError,
    enumerable:false,
    writable:true,
    configurable:true
  }
});

if(Object.setPrototypeOf) {
  Object.setPrototypeOf(MyError,Error);
}else{
  MyError.__proto__ = Error;
}

export default MyError;
```
#### Try / Catch

``try/catch`` 主要用于捕捉异常。``try/catch``语句包含了一个``try``块,和至少有一个``catch``块或者一个``finally``块。

``try``块中放入可能产生异常的语句或函数

``catch``块中包含要执行的语句,当``try``块中抛出异常时,``catch``块会捕捉到这个异常信息,并执行``catch``块中的代码,如果``try``块中没有异常抛出,这``catch``块将会跳过。

``finally``块在``try``块和``catch``块之后执行。无论是否有异常抛出或者是否被捕获它总是执行。当在``finally``块中抛出异常信息时会覆盖掉``try``块中的异常信息。


#### 统一异常处理

代码中抛出的异常,一种是要展示给用户,一种是展示给开发者。

对于展示给用户的异常,一般使用``alert``或``toast``,对于展示给开发者的异常,一般输出到控制台。

[:arrow_up:返回目录](#目录)
