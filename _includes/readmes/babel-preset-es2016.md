# babel-preset-es2016

> Babel预设了所有的ES2016插件.

## 安装

```sh
npm install --save-dev babel-preset-es2016
```

## 使用

### 通过 `.babelrc` (推荐)

**.babelrc**

```json
{
  "presets": ["es2016"]
}
```

### 通过 CLI

```sh
babel script.js --presets es2016
```

### 通过 Node API

```javascript
require("babel-core").transform("code", {
  presets: ["es2016"]
});
```
