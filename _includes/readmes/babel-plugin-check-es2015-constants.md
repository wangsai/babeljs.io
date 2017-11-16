# babel-plugin-check-es2015-constants

验证 ES2015 常量 (防止重新定义 const 变量).

## 例子

**输出**

```js
const a = 1;
a = 2;
```

**输出**

```bash
repl: "a" is read-only
  1 | const a = 1;
> 2 | a = 2;
    | ^
```


## 安装

```sh
npm install --save-dev babel-plugin-check-es2015-constants
```

## 使用

### 通过 `.babelrc` (推荐)

**.babelrc**

```json
{
  "plugins": ["check-es2015-constants"]
}
```

### 通过 CLI

```sh
babel --plugins check-es2015-constants script.js
```

### 通过 Node API

```javascript
require("babel-core").transform("code", {
  plugins: ["check-es2015-constants"]
});
```

## 注意

这个检查只会验证const常量。如果你需要把它编译为 `var` ，你需要安装和使用 [`transform-es2015-block-scoping`](http://babeljs.io/docs/plugins/transform-es2015-block-scoping/).
