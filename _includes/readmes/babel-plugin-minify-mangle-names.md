# babel-plugin-minify-mangle-names

Context- 和 scope- 感知变量重命名。

## 示例

**输入**

```javascript
var globalVariableName = 42;
function foo() {
  var longLocalVariableName = 1;
  if (longLocalVariableName) {
    console.log(longLocalVariableName);
  }
}
```

**输出**

```javascript
var globalVariableName = 42;
function foo() {
  var a = 1;
  if (a) {
    console.log(a);
  }
}
```

## 安装

```sh
npm install babel-plugin-minify-mangle-names
```

## 使用

### 通过 `.babelrc` (推荐)

**.babelrc**

```json
// 不包含选项
{
  "plugins": ["minify-mangle-names"]
}
```

```json
// 包含选项
{
  "plugins": ["minify-mangle-names", { "exclude": { "foo": true, "bar": true} }]
}
```

### 通过 CLI

```sh
babel --plugins minify-mangle-names script.js
```

### 通过 Node API

```javascript
require("babel-core").transform("code", {
  plugins: ["minify-mangle-names"]
});
```

## 选项

+ `exclude` - 一个普通的 JS 对象，其中键为标识名，值标明是否排除
+ `eval` - 通过 eval 在可访问作用域中 mangle 标识符
+ `keepFnName` - 防止 mangler 改变函数名称。对于依赖 `fn.name` 的代码有效。
+ `topLevel` - mangle 顶级标识
+ `keepClassName` - 防止 mangler 改变类名
