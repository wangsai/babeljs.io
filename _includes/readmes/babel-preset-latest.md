# babel-preset-latest

> Babel preset 包括 es2015, es2016, es2017.

## 安装

```sh
npm install --save-dev babel-preset-latest
```

## 使用

### 通过 `.babelrc` (推荐)

**.babelrc**

```json
{
  "presets": ["latest"]
}
```

### 通过 CLI

```sh
babel script.js --presets latest
```

### 通过 Node API

```javascript
require("babel-core").transform("code", {
  presets: ["latest"]
});
```

### 选项

### `es2015`

`boolean`, 默认为 `true`.

可以切换来自包括 [es2015 preset](https://babeljs.io/docs/plugins/preset-es2015/) 的插件.

```json
{
  "presets": [
    ["latest", {
      "es2015": false
    }]
  ]
}
```

你也可以传递 `es2015` preset 的选项.

```json
{
  "presets": [
    ["latest", {
      "es2015": {
        "modules": false
      }
    }]
  ]
}
```

**注意:** 这也适用于下面其他 preset-year 的选项.

### `es2016`

`boolean`, 默认为 `true`.

可以切换来自包括 [es2016 preset](https://babeljs.io/docs/plugins/preset-es2016/) 的插件.

### `es2017`

`boolean`, 默认为 `true`.

可以切换来自包括 [es2017 preset](https://babeljs.io/docs/plugins/preset-es2017/) 的插件.
