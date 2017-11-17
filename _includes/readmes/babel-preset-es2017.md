# babel-preset-es2017

> Babel预设了所有的ES2017插件.

## 安装

```sh
npm install --save-dev babel-preset-es2017
```

## 使用

### 通过 `.babelrc` (Recommended)

**.babelrc**

```json
{
  "presets": ["es2017"]
}
```

### 通过 CLI

```sh
babel script.js --presets es2017
```

### 通过 Node API

```javascript
require("babel-core").transform("code", {
  presets: ["es2017"]
});
```
