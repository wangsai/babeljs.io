# babel-plugin-minify-infinity

## 示例

**输入**

```javascript
Infinity;
```

**输出**

```javascript
1 / 0;
```

## 安装

```sh
npm install babel-plugin-minify-infinity
```

## 使用

### 通过 `.babelrc` (推荐)

**.babelrc**

```json
{
  "plugins": ["minify-infinity"]
}
```

### 通过 CLI

```sh
babel --plugins minify-infinity script.js
```

### 通过 Node API

```javascript
require("babel-core").transform("code", {
  plugins: ["minify-infinity"]
});
```
