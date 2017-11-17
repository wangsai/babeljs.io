# babel-preset-es2015

> Babel预设了所有的ES2015插件.

## 安装

```sh
npm install --save-dev babel-preset-es2015
```

## 使用

### 通过 `.babelrc` (推荐)

**.babelrc**

```json
{
  "presets": ["es2015"]
}
```

### 通过 CLI

```sh
babel script.js --presets es2015
```

### 通过 Node API

```javascript
require("babel-core").transform("code", {
  presets: ["es2015"]
});
```

## 选项

### `loose`

`boolean`, 默认 `false`.

为该预设中允许它们的任何插件启用“loose”转换.

### `modules`

`"amd" | "umd" | "systemjs" | "commonjs" | false`, 默认 `"commonjs"`.

启用将es6模块语法转换为另一个模块类型.

将其设置为`false`将不会转换任何模块.

### `spec`

`boolean`, 默认`false`.

为该预设中允许它们的任何插件启用“spec”转换.