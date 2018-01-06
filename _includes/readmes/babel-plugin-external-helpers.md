# babel-plugin-external-helpers

## 安装

```sh
npm install --save-dev babel-plugin-external-helpers
```

## 使用

### 通过 `.babelrc` (推荐)

**.babelrc**

```json
{
  "plugins": ["external-helpers"]
}
```

### 通过 CLI

```sh
babel --plugins external-helpers script.js
```

### 通过 Node API

```javascript
require("babel-core").transform("code", {
  plugins: ["external-helpers"]
});
```
