# babel-plugin-minify-dead-code-elimination

尽可能的内联绑定。尝试评估表达式，并修剪无法到达的结果。

## 示例

**输入**

```javascript
function foo() {var x = 1;}
function bar() { var x = f(); }
function baz() {
  var x = 1;
  console.log(x);
  function unused() {
    return 5;
  }
}
```

**输出**

```javascript
function foo() {}
function bar() { f(); }
function baz() {
  console.log(1);
}
```

## 安装

```sh
npm install babel-plugin-minify-dead-code-elimination
```

## 使用

### 通过 `.babelrc` (Recommended)

**.babelrc**

```json
// without options
{
  "plugins": ["minify-dead-code-elimination"]
}

// with options
{
  "plugins": ["minify-dead-code-elimination", { "optimizeRawSize": true }]
}
```

### 通过 CLI

```sh
babel --plugins minify-dead-code-elimination script.js
```

### 通过 Node API

```javascript
require("babel-core").transform("code", {
  plugins: ["minify-dead-code-elimination"]
});
```

## 可选项

+ `keepFnName` - 防止插件删除函数名。适用于依赖于 `fn.name` 的代码
+ `keepFnArgs` - 防止插件删除函数参数。适用于依赖于 `fn.length` 的代码
+ `keepClassName` - 防止插件删除类名。 适用于依赖于 `cls.name` 的代码
+ `tdz` - TDZ的配置 (Temporal Dead Zone)(暂时性死区)
