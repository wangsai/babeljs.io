---
layout: docs
title: 学习 ES2015
description: ECMAScript 2015 功能的详细概述. 基于 Luke Hoban's es6features 项目.
permalink: /learn-es2015/
---

<blockquote class="babel-callout babel-callout-info">
  <h3>es6功能</h3>
  <p>
    这个文档最初来自于 Luke Hoban 的杰作
    <a href="https://git.io/es6features">es6features</a> repo. 去github上面给star吧!
  </p>
</blockquote>

<blockquote class="babel-callout babel-callout-info">
  <h4>REPL</h4>
  <p>
    请务必在网上尝试这些功能
    <a href="/repl">REPL</a>.
  </p>
</blockquote>

## 简介

> ECMAScript 2015 是2015年6月被批准的ECMAScript标准。   

ES2015 是该语言的显著更新，也是自2009年ES5标准确定后的第一个重大更新，将会得到主要的JavaScript引擎的[实现](https://kangax.github.io/es5-compat-table/es6/)    

查看 [ES2015版本的完整规范](http://www.ecma-international.org/ecma-262/6.0/index.html)

## ECMAScript 2015 功能

### 箭头函数

箭头函数用 `=>` 来代表一个函数，语法上类似于C#, Java8和CoffeeScript中的相关特性。他支持两种写法: 表达式（Expression bodies）和函数体（Statement bodies）。值得注意的是，与一般的函数不同，函数体内的`this`对象，绑定定义时所在的对象，而不是使用时所在的对象。   

```js
// 表达式 Expression bodies
var odds = evens.map(v => v + 1);
var nums = evens.map((v, i) => v + i);

// 函数体 Statement bodies
nums.forEach(v => {
  if (v % 5 === 0)
    fives.push(v);
});

//  this 对象
var bob = {
  _name: "Bob",
  _friends: [],
  printFriends() {
    this._friends.forEach(f =>
      console.log(this._name + " knows " + f));
  }
};

// arguments 对象
function square() {
  let example = () => {
    let numbers = [];
    for (let number of arguments) {
      numbers.push(number * number);
    }

    return numbers;
  };

  return example();
}

square(2, 4, 7.5, 8, 11.5, 21); // returns: [4, 16, 56.25, 64, 132.25, 441]

```

### 类
ES2015的类只是一个语法糖，通过class关键字让语法更接近传统的面向对象模式，本质上还是基于原型的。使用单一便捷的声明格式，使得类使用起来更方便，也更具互操作性。类支持基于原型的继承，调用父类的构造函数，生成实例，静态方法和构造函数。  

```js
class SkinnedMesh extends THREE.Mesh {
  constructor(geometry, materials) {
    // 调用父类的构造函数 super是父类的实例
    super(geometry, materials);

    this.idMatrix = SkinnedMesh.defaultMatrix();
    this.bones = [];
    this.boneMatrices = [];
    //...
  }
  update(camera) {
    //调用this.update()
    super.update();
  }

  // 静态方法
  static defaultMatrix() {
    return new THREE.Matrix4();
  }
}
```

### 增强的对象字面量

经扩展后的对象字面量，允许在结构中设置原型，简化了`foo: foo`这样的赋值，定义方法和调用父级。这样使得对象字面量更接近类的声明，并且使得基于对象的设计更加房方便。

```js
var obj = {
    // 设置 prototype
    __proto__: theProtoObj,
    // 重复的__proto__属性设置原型或触发错误。
    ['__proto__']: somethingElse,
    // ‘handler: handler’ 简写
    handler,
    // 方法
    toString() {
     // 调用父级方法
     return "d " + super.toString();
    },
    // 设置动态的属性名
    [ "prop_" + (() => 42)() ]: 42
};

```

<blockquote class="babel-callout babel-callout-warning">
  <p>
    <code>__proto__</code> 需要原生支持, 并且在 ECMAScript 版本中被弃用. 现在大多数引擎支持, 但是 <a href="https://kangax.github.io/compat-table/es6/#__proto___in_object_literals">仍有些不支持</a>. 同样, 注意 <a href="http://www.ecma-international.org/ecma-262/6.0/index.html#sec-additional-ecmascript-features-for-web-browsers">web 浏览器</a> 仍然需要支持该属性, 详细请看 <a href="http://www.ecma-international.org/ecma-262/6.0/index.html#sec-object.prototype.__proto__">附录 B</a>. 该属性在node中支持.
  </p>
</blockquote>

### 模版字符串

模版字符串提供了构建字符串的语法糖，类似于Perl，Python等语言中的字符串插值。可以构建一个自定义标签，避免注入攻击或者从字符串内容中构建更加高级的数据结构

```js
// 创建几本的模板字符串
`This is a pretty little template string.`

// 多行字符串
`In ES5 this is
 not legal.`

// 插入变量
var name = "Bob", time = "today";
`Hello ${name}, how are you ${time}?`

// 不使用转义
String.raw`In ES5 "\n" is a line-feed.`

// 创建一个HTTP请求头的模版字符串，通过替换内容来构建请求
GET`http://foo.org/bar?a=${a}&b=${b}
    Content-Type: application/json
    X-Credentials: ${credentials}
    { "foo": ${foo},
      "bar": ${bar}}`(myOnReadyStateChangeHandler);
```

### 解构（Destructuring）

解构允许数组和对象使用模式匹配进行绑定。解构是故障弱化的，类似于标准对象以`foo['foo']`方式查找变量，当没有找到时返回`undefined`。

```js
// 列表（数组）匹配
var [a, , b] = [1,2,3];

// 对象匹配
var { op: a, lhs: { op: b }, rhs: c }
       = getASTNode()

// 对象匹配的简写
// 绑定当前作用域的 `op`, `lhs` 和 `rhs`
var {op, lhs, rhs} = getASTNode()

// 可以用在函数的参数中
function g({name: x}) {
  console.log(x);
}
g({name: 5})

// 弱化解构
var [a] = [];
a === undefined;

// Fail-soft destructuring with defaults
var [a = 1] = [];
a === 1;

// 解构 + 默认参数
function r({x, y, w = 10, h = 10}) {
  return x + y + w + h;
}
r({x:1, y:2}) === 23
```

### 默认参数（Default） + 不定参数（Rest） + 扩展运算符（Spread）

调用具有默认参数的函数，将数组转换为连续的函数参数，将连续的函数参数转换为数组。Rest让我们不再需要`arguments`，并且更直接地解决了一些常见的问题。

```js
function f(x, y=12) {
  // y is 12 if not passed (or passed as undefined)
  return x + y;
}
f(3) == 15
```
```js
function f(x, ...y) {
  // y is an Array
  return x * y.length;
}
f(3, "hello", true) == 6
```
```js
function f(x, y, z) {
  return x + y + z;
}
// Pass each elem of array as argument
f(...[1,2,3]) == 6
```

### Let（局部变量） + Const（常量）

新增块级作用域。`let`是新的`var`。`const`是单赋值（仅允许被赋值一次）。静态限制（Static restrictions ）阻止变量在赋值前被使用。


```js
function f() {
  {
    let x;
    {
      // this is ok since it's a block scoped name
      const x = "sneaky";
      // error, was just defined with `const` above
      x = "foo";
    }
    // this is ok since it was declared with `let`
    x = "bar";
    // error, already declared above in this block
    let x = "inner";
  }
}
```

### 迭代器（Iterators） + For..Of循环

迭代器对象允许像 CLR IEnumerable 或者 Java Iterable 一样自定义迭代器。将`for..in`转换为自定义的基于迭代器的形如`for..of`的迭代，不需要实现一个数组，支持像 LINQ 一样的惰性设计模式。

```js
// 实现斐波那契数列的迭代器
let fibonacci = {
  [Symbol.iterator]() {
    let pre = 0, cur = 1;
    return {
      next() {
        [pre, cur] = [cur, pre + cur];
        return { done: false, value: cur }
      }
    }
  }
}

for (var n of fibonacci) {
  // 循环将在n > 1000 时结束
  if (n > 1000)
    break;
  console.log(n);
}
```

迭代器基于如下的鸭子类型的借口（使用[TypeScript](http://typescriptlang.org) 类型的语法来解析）：

```ts
interface IteratorResult {
  done: boolean;
  value: any;
}
interface Iterator {
  next(): IteratorResult;
}
interface Iterable {
  [Symbol.iterator](): Iterator
}
```

<blockquote class="babel-callout babel-callout-info">
  <h4> 通过 polyfill 支持</h4>
  <p>
    为了使用迭代器你必须引入Babel的 <a href="/docs/usage/polyfill">polyfill</a>.
  </p>
</blockquote>

### Generators

Generator通过使用`function*`和`yield`关键字简化了迭代器的编写。一个通过`function*`声明的函数会返回一个Generators实例。Generator是迭代器包含额外的`next`和`throw`方法的子类型。这些特性使得值可以流回Generator，故`yield`是一个可以返回（或抛出）值的表达式。

标注：也可以用于使用‘await’这样的异步编程，详见ES7 `await` [协议](https://github.com/lukehoban/ecmascript-asyncawait).

```js
var fibonacci = {
  [Symbol.iterator]: function*() {
    var pre = 0, cur = 1;
    for (;;) {
      var temp = pre;
      pre = cur;
      cur += temp;
      yield cur;
    }
  }
}

for (var n of fibonacci) {
  // truncate the sequence at 1000
  if (n > 1000)
    break;
  console.log(n);
}
```

Generator 同样 (使用 [TypeScript](http://typescriptlang.org) 类型的语法解析):

```ts
interface Generator extends Iterator {
    next(value?: any): IteratorResult;
    throw(exception: any);
}
```

<blockquote class="babel-callout babel-callout-info">
  <h4>通过 polyfill 支持</h4>
  <p>
    要使用Generator，你需要在项目中包含Babel的 <a href="/docs/usage/polyfill">polyfill</a>.
  </p>
</blockquote>

### Comprehensions

Babel 6.0 移除了

### Unicode 编码

新增了一系列的扩展来支持完整的unicode编码，其中包括字符串中新的unicode语法格式，正则表达式的`u`模式来处理代码点，新的API也让字符串可以处理21位的代码点（code points）。这些新特性允许我们使用JavaScript构建国际化的应用。

```js
// 和ES5.1相同
"𠮷".length == 2

// 正则表达式新的u模式
"𠮷".match(/./u)[0].length == 2

// 新的unicode格式
"\u{20BB7}" == "𠮷" == "\uD842\uDFB7"

// 新的字符串方法
"𠮷".codePointAt(0) == 0x20BB7

// for of迭代代码点
for(var c of "𠮷") {
  console.log(c);
}
```

### 模块（Modules） 

为了定义组件，从语言层面对模块进行了支持。编写方式借鉴了流行的JavaScript模块加载器（AMD, CommonJS）。由主机定义的默认加载器定义运行时的行为。使用隐式异步模式——在模块可以被获取和加载前不会有代码执行。

```js
// lib/math.js
export function sum(x, y) {
  return x + y;
}
export var pi = 3.141593;
```
```js
// app.js
import * as math from "lib/math";
console.log("2π = " + math.sum(math.pi, math.pi));
```
```js
// otherApp.js
import {sum, pi} from "lib/math";
console.log("2π = " + sum(pi, pi));
```

以及一些额外的功能：`export default` and `export *`:

```js
// lib/mathplusplus.js
export * from "lib/math";
export var e = 2.71828182846;
export default function(x) {
    return Math.exp(x);
}
```
```js
// app.js
import exp, {pi, e} from "lib/mathplusplus";
console.log("e^π = " + exp(pi));
```

<blockquote class="babel-callout babel-callout-info">
  <h4>模块的格式：</h4>
  <p>
    Babel可以将ES2015的模块转换为一下几种格式：Common.js，AMD，System，以及UMD。你甚至可以创建你自己的方式。详见<a href="/docs/plugins/">模块文档</a>.
  </p>
</blockquote>

### 模块加载器（Module Loaders）

<blockquote class="babel-callout babel-callout-warning">
  <h4>非ES2015部分</h4>
  <p>
    并不是ES2015的一部分：这部分ECMAScript 2015规范是由实现定义（implementation-defined）的。最终的标准将在WHATWG的<a href="https://whatwg.github.io/loader/">Loader 规范</a>, 中确定。下面的内容来自于之前的ES2015草稿。
  </p>
</blockquote>

模块加载器支持以下功能：

- 动态加载（Dynamic loading）
- 状态一致性（State isolation）
- 全局空间一致性（Global namespace isolation）
- 编译钩子（Compilation hooks）
- 嵌套虚拟化（Nested virtualization）

你可以对默认的加载器进行配置，新的加载器能构建评估并在独立或受限的上下文中加载代码。

```js
// 动态加载 – ‘System’ 是默认的加载器
System.import("lib/math").then(function(m) {
  alert("2π = " + m.sum(m.pi, m.pi));
});

// 创建执行沙箱 – new Loaders
var loader = new Loader({
  global: fixup(window) // replace ‘console.log’
});
loader.eval("console.log(\"hello world!\");");

// 直接操作模块的缓存
System.get("jquery");
System.set("jquery", Module({$: $})); // WARNING: not yet finalized
```

<blockquote class="babel-callout babel-callout-warning">
  <h4>需要额外的polyfill</h4>
  <p>
    由于Babel默认使用common.js的模块，你需要一个polyfill来使用加载器API。
    <a href="https://github.com/ModuleLoader/es6-module-loader">点击获取</a>.
  </p>
</blockquote>

<blockquote class="babel-callout babel-callout-info">
  <h4>使用模块加载器</h4>
  <p>
    为了使用此功能，你需要告诉Babel使用<code>system</code>模块格式化工具。在此查看
    <a href="https://github.com/systemjs/systemjs">System.js</a>
  </p>
</blockquote>


### Map + Set + WeakMap + WeakSet

为常见算法的实现提供了更有效的数据结构。WeakMaps提供了对对象的弱引用（不会被垃圾回收计数）。

```js
// Sets
var s = new Set();
s.add("hello").add("goodbye").add("hello");
s.size === 2;
s.has("hello") === true;

// Maps
var m = new Map();
m.set("hello", 42);
m.set(s, 34);
m.get(s) == 34;

// Weak Maps
var wm = new WeakMap();
wm.set(s, { extra: 42 });
wm.size === undefined

// Weak Sets
var ws = new WeakSet();
ws.add({ data: 42 });
// 由于传入的对象没有其他引用，故将不会被set保存。
```

<blockquote class="babel-callout babel-callout-info">
  <h4>需要polyfill支持</h4>
  <p>
    为了在所有环境下使用Maps，Sets，WeakMaps和WeakSets，你需要使用Babel的 <a href="/docs/usage/polyfill">polyfill</a>.
  </p>
</blockquote>

### Proxies（代理对象）

代理对象可以创建一个具有目标对象全部行为的对象。可用于拦截，对象的虚拟化，记录/分析等。

```js
// 代理普通对象
var target = {};
var handler = {
  get: function (receiver, name) {
    return `Hello, ${name}!`;
  }
};

var p = new Proxy(target, handler);
p.world === "Hello, world!";
```

```js
// 代理函数对象
var target = function () { return "I am the target"; };
var handler = {
  apply: function (receiver, ...args) {
    return "I am the proxy";
  }
};

var p = new Proxy(target, handler);
p() === "I am the proxy";
```

下面是所有运行级别元操作（meta-operations）中可能出现的traps：

```js
var handler =
{
  // target.prop
  get: ...,
  // target.prop = value
  set: ...,
  // 'prop' in target
  has: ...,
  // delete target.prop
  deleteProperty: ...,
  // target(...args)
  apply: ...,
  // new target(...args)
  construct: ...,
  // Object.getOwnPropertyDescriptor(target, 'prop')
  getOwnPropertyDescriptor: ...,
  // Object.defineProperty(target, 'prop', descriptor)
  defineProperty: ...,
  // Object.getPrototypeOf(target), Reflect.getPrototypeOf(target),
  // target.__proto__, object.isPrototypeOf(target), object instanceof target
  getPrototypeOf: ...,
  // Object.setPrototypeOf(target), Reflect.setPrototypeOf(target)
  setPrototypeOf: ...,
  // for (let i in target) {}
  enumerate: ...,
  // Object.keys(target)
  ownKeys: ...,
  // Object.preventExtensions(target)
  preventExtensions: ...,
  // Object.isExtensible(target)
  isExtensible :...
}
```

<blockquote class="babel-callout babel-callout-danger">
  <h4>不支持的特性</h4>
  <p>
    由于ES5的局限性，Proxies无法被转换或者通过polyfill兼容，查看<a href="https://kangax.github.io/compat-table/es6/#test-Proxy">不同JavaScript引擎</a>.
  </p>
</blockquote>

### Symbols

Symbol对对象的状态进行访问控制。Symbol允许对象的属性不仅可以通过`string（ES5）`命名，还可以通过`symbol`命名。`symbol`是一种基本数据类型。可选的`name`参数用于调试——但并不是他本身的一部分。Symbol是唯一的，但不是私有的，因为他们使用诸如`Object.getOwnPropertySymbols`这样的方法来使用。

```js
(function() {

  // 模块内的 symbol
  var key = Symbol("key");

  function MyClass(privateData) {
    this[key] = privateData;
  }

  MyClass.prototype = {
    doStuff: function() {
      ... this[key] ...
    }
  };

  // 被Bable部分支持，原生环境可以完全实现
  typeof key === "symbol"
})();

var c = new MyClass("hello")
c["key"] === undefined
```

<blockquote class="babel-callout babel-callout-info">
  <h4>通过polyfill部分实现：</h4>
  <p>
    通过Babel的<a href="/docs/usage/polyfill">polyfill</a>.部分实现。由于语言的限制，部分功能不能转换或通过polyfill兼容。您可以查看code.js的 <a href="https://github.com/zloirock/core-js#caveats-when-using-symbol-polyfill">注意事项</a> 获取更多信息.
  </p>
</blockquote>

### 可以创建内建对象的子类

在ES2015中，可以创建内建对象如`Array `，`Date`以及`DOMElement`的子类。

```js
// 创建Array的子类
class MyArray extends Array {
    constructor(...args) { super(...args); }
}

var arr = new MyArray();
arr[1] = 12;
arr.length == 2
```

<blockquote class="babel-callout babel-callout-warning">
  <h4>部分支持</h4>
  <p>
    部分支持：由于ES5引擎的限制，可以创建HTMLElement的子类，但不能创建诸如Array，Date和Error等对象的子类。
  </p>
</blockquote>

### Math + Number + String + Object APIs

新增很多功能，如核心的Math库，数组转换和用于对象复制的Object.assign()。

```js
Number.EPSILON
Number.isInteger(Infinity) // false
Number.isNaN("NaN") // false

Math.acosh(3) // 1.762747174039086
Math.hypot(3, 4) // 5
Math.imul(Math.pow(2, 32) - 1, Math.pow(2, 32) - 2) // 2

"abcde".includes("cd") // true
"abc".repeat(3) // "abcabcabc"

Array.from(document.querySelectorAll("*")) // Returns a real Array
Array.of(1, 2, 3) // Similar to new Array(...), but without special one-arg behavior
[0, 0, 0].fill(7, 1) // [0,7,7]
[1,2,3].findIndex(x => x == 2) // 1
["a", "b", "c"].entries() // iterator [0, "a"], [1,"b"], [2,"c"]
["a", "b", "c"].keys() // iterator 0, 1, 2
["a", "b", "c"].values() // iterator "a", "b", "c"

Object.assign(Point, { origin: new Point(0,0) })
```

<blockquote class="babel-callout babel-callout-warning">
  <h4>通过polyfill有限的支持</h4>
  <p>
    上述许多API都通过polyfill进行了支持，但是部分特性由于多种原因没有被实现（如，String.prototype.normalize需要编写大量额外的代码来实现），你可以在
    <a href="https://github.com/addyosmani/es6-tools#polyfills">这里</a>找到更多的polyfill。
  </p>
</blockquote>

### 二进制和八进制字面量
新增两种数字字面量：二进制`b`和八进制`o`。

```js
0b111110111 === 503 // true
0o767 === 503 // true
```

<blockquote class="babel-callout babel-callout-warning">
  <h4>仅支持字面模式</h4>
  <p>
    Babel仅可以转换0o767，并不能转换Number("0o767")。
  </p>
</blockquote>


### Promises

Promises是一种异步编程的方式。Promises在将来可能会得到支持。目前很多的JavaScript库都使用了Promises。

```js
function timeout(duration = 0) {
    return new Promise((resolve, reject) => {
        setTimeout(resolve, duration);
    })
}

var p = timeout(1000).then(() => {
    return timeout(2000);
}).then(() => {
    throw new Error("hmm");
}).catch(err => {
    return Promise.all([timeout(100), timeout(200)]);
})
```

<blockquote class="babel-callout babel-callout-info">
  <h4>通过polyfill</h4>
  <p>
    要使用Promises，你需要引入Babel的 <a href="/docs/usage/polyfill">polyfill</a>.
  </p>
</blockquote>

### Reflect API

完整的Reflect API使得可以在运行级别对对象进行元操作。它相当与是Proxy API的逆，并允许调用对应的元操作，如proxy traps。这使得它在实现Proxy时非常有用。

```js
var O = {a: 1};
Object.defineProperty(O, 'b', {value: 2});
O[Symbol('c')] = 3;

Reflect.ownKeys(O); // ['a', 'b', Symbol(c)]

function C(a, b){
  this.c = a + b;
}
var instance = Reflect.construct(C, [20, 22]);
instance.c; // 42
```

<blockquote class="babel-callout babel-callout-info">
  <h4>通过polyfill</h4>
  <p>
    要使用Reflect API，你需要引入Babel的 <a href="/docs/usage/polyfill">polyfill</a>.
  </p>
</blockquote>

### Tail Calls

现在递归调用函数不用担心栈无限增长，使得递归算法在面对无限的输入时更加安全。

```js
function factorial(n, acc = 1) {
    "use strict";
    if (n <= 1) return acc;
    return factorial(n - 1, n * acc);
}

// 如今运行这段代码会导致栈溢出
// 但是在ES2015中，即便输入很随意也可以安全运行
factorial(100000)
```

<blockquote class="babel-callout babel-callout-warning">
  <h4>已经被bable6移除</h4>
  <p>
    该特性仅支持直接对自身引用的递归。由于功能本身的复杂性和表现冲突，使得该特性无法在全局下支持。
  </p>
</blockquote>

