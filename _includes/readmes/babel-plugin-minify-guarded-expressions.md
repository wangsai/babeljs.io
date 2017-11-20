# babel-plugin-minify-guarded-expressions

## 示例

**输入**

```javascript
!x && foo();
alert(0 && new Foo());
```

**输出**

```javascript
x || foo();
alert(0);
```

## 安装

```sh
npm install babel-plugin-minify-guarded-expressions
```

## 使用

### 通过 `.babelrc` (Recommended)

**.babelrc**

```json
{
  "plugins": ["minify-guarded-expressions"]
}
```

### 通过 CLI

```sh
babel --plugins minify-guarded-expressions script.js
```

### 通过 Node API

```javascript
require("babel-core").transform("code", {
  plugins: ["minify-guarded-expressions"]
});
```
