## 目录

1. **[理解 ECMAScript 和 JavaScript 的关系](#ES&JS)**
1. **[掌握 JavaScript 提供的全局对象、全局函数、全局属性](#global)**
1. **[应用 map、reduce、filter 等高阶函数解决问题](#)**
1. **[setInterval 需要注意的点，使用 settimeout 实现 setInterval](#)**
1. **[JavaScript 提供的正则表达式 API、可以使用正则表达式解决常见问题](#)**
1. **[JavaScript 异常处理的方式，统一的异常处理方案](#)**

### <h3 id="ES&JS">理解 ECMAScript 和 JavaScript 的关系<h3>

- **Ecma International**
  - 一个制定技术标准的组织
- **ECMA-262**
  - 由 Ecma International 发布。它包含了脚本语言的标准。
  - 不妨把 ECMA-262 看做 ECMAScript 的编号。
- **ECMAScript**
  - 由 ECMA-262 制定的标准，用于实现通用的脚本语言。
  - ECMAScript 提供了脚本语言需要遵守的规则、细节和规范
- **JavaScript**
  - 通用脚本编程语言，它遵循了 ECMAScript 标准
    - 换句话说，JavaScript 是 ECMAScript 的方言。
- **JavaScript 引擎**
  - 理解并执行 JavaScript 代码的解释器
  - 浏览器中会有 JavaScript 引擎，比如 Chrome 有 V8，Firefox 有 SpiderMonkey，Edge 有 Chakra。JavaScript 引擎处理 JavaScript 代码，类似于人对语言的处理。
- **浏览器性能差异**
  - 两个浏览器都可以理解 JavaScript 代码，但是其中一个浏览器会快一些，因为它的 JavaScript 引擎的实现方式更加高效。
- **浏览器支持差异**
  - 尽管浏览器的 JavaScript 引擎都能理解 JavaScript，但是有些浏览器的理解能力更强 ，它们对 JavaScript 的支持是不一样的。
- **ECMAScript 6**
  - ECMA-262 的第六个版本(同义词：ES6、ES2015andECMAScript 2015)
- **先有鸡还是先有蛋**
  - JavaScript 是 1996 年创造的，它在 1997 年提交给 Ecma International，因此才有了 ECMAScript。同时 JavaScript 遵循 ECMAScript 标准，因此 JavaScript 是 ECMAScript 的实例。
  - 因此：ECMAScript 是基于 JavaScript 的，而 JavaScript 也是基于 ECMAScript 的，两个密不可分。

[:arrow_up:返回目录](#目录)

### <h3 id="global">掌握 JavaScript 提供的全局对象、全局函数、全局属性<h3>

**JavaScript全局对象**
``全局属性和函数可用于所有内建的JavaScript对象。``

**全局对象的描述**
> 1. 全局对象是预定义的对象，作为 JavaScript 的全局函数和全局属性的占位符。通过使用全局对象，可以访问所有其他所有预定义的对象、函数和属性。全局对象不是任何对象的属性，所以它没有名称。

> 2. 在顶层 JavaScript 代码中，可以用关键字 this 引用全局对象。但通常不必用这种方式引用全局对象，因为全局对象是作用域链的头，这意味着所有非限定性的变量和函数名都会作为该对象的属性来查询。例如，当JavaScript 代码引用 parseInt() 函数时，它引用的是全局对象的 parseInt 属性。全局对象是作用域链的头，还意味着在顶层 JavaScript 代码中声明的所有变量都将成为全局对象的属性。

> 3. 全局对象只是一个对象，而不是类。既没有构造函数，也无法实例化一个新的全局对象。

> 4. 在 JavaScript 代码嵌入一个特殊环境中时，全局对象通常具有环境特定的属性。实际上，ECMAScript 标准没有规定全局对象的类型，JavaScript 的实现或嵌入的 JavaScript 都可以把任意类型的对象作为全局对象，只要该对象定义了这里列出的基本属性和函数。例如，在允许通过 LiveConnect 或相关的技术来脚本化 Java 的 JavaScript 实现中，全局对象被赋予了这里列出的 java 和 Package 属性以及 getClass() 方法。而在客户端 JavaScript 中，全局对象就是 Window 对象，表示允许 JavaScript 代码的 Web 浏览器窗口。

#### 总结：
1. 全局环境的this会指向全局对象window，此时this===window;
1. 全局变量会挂载在window对象下，会成为window下的一个属性。
1. 如果你没有使用严格模式并给一个未声明的变量赋值的话，JS会自动创建一个全局变量。