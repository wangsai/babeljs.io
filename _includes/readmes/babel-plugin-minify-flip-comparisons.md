# babel-plugin-minify-flip-comparisons

**备注:** 虽然这个插件没有以任何方式缩短输出，但它对基于重复的压缩算法(如gzip)进行优化。

## 示例

**输入**

```javascript
const foo = a === 1;
if (bar !== null) {
  var baz = 0;
}
```

**输出**

```javascript
const foo = 1 === a;
if (null !== bar) {
  var baz = 0;
}
```

## Installation

```sh
npm install babel-plugin-minify-flip-comparisons
```

## 使用

### 通过 `.babelrc` (Recommended)

**.babelrc**

```json
{
  "plugins": ["minify-flip-comparisons"]
}
```

### 通过 CLI

```sh
babel --plugins minify-flip-comparisons script.js
```

### 通过 Node API

```javascript
require("babel-core").transform("code", {
  plugins: ["minify-flip-comparisons"]
});
```
