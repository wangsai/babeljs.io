# babel-plugin-minify-builtins

迷你的标准内建对象

## 示例

**输入**

```javascript
Math.floor(a) + Math.floor(b)
```

**输出**

```javascript
var _Mathfloor = Math.floor;

_Mathfloor(a) + _Mathfloor(b);
```

## 安装

```sh
npm install babel-plugin-minify-builtins
```

## 使用

### 通过 `.babelrc` (官方推荐)

**.babelrc**

```json
{
  "plugins": ["minify-builtins"]
}
```

### 通过 CLI

```sh
babel --plugins minify-builtins script.js
```

### 通过 Node API

```javascript
require("babel-core").transform("code", {
  plugins: ["minify-builtins"]
});
```

## 可选项

+ `tdz` - TDZ的配置 (Temporal Dead Zone)(暂时性死区)
