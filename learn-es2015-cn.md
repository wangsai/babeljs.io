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

### 待续