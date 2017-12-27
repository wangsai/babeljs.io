# babel-preset-flow

> 所有 Flow 的插件的 Babel preset 。

该 preset 包含以下这些插件:

- [transform-flow-strip-types](https://babeljs.io/docs/plugins/transform-flow-strip-types/)

## 例子

**输入**

```javascript
function foo(one: any, two: number, three?): string {}
```

**输出**

```javascript
function foo(one, two, three) {}
```

## 安装

```sh
npm install --save-dev babel-preset-flow
```

## 使用

### 通过 `.babelrc` (推荐)

**.babelrc**

```json
{
  "presets": ["flow"]
}
```

### 通过 CLI

```sh
babel --presets flow script.js
```

### 通过 Node API

```javascript
require("babel-core").transform("code", {
  presets: ["flow"]
});
```
