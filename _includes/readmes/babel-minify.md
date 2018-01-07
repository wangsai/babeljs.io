# babel-minify

Node API 和 CLI

[![npm](https://img.shields.io/npm/v/babel-minify.svg?maxAge=2592000)](https://www.npmjs.com/package/babel-minify)

如果你还没有使用 babel (作为 preset) 或想要独立运行它，你可以使用 `babel-minify` 。

## 安装

```sh
npm install babel-minify --save-dev
```

## 使用

### Node API

```js
const minify = require("babel-minify");

const {code, map} = minify("input code", {
  mangle: {
    keepClassName: true
  }
});
```

### CLI

```sh
minify input.js --out-file input.min.js --mangle.keepClassName
```

## Node API

```js
const minify = require("babel-minify");

minify(input, minifyOptions, overrides)
```

### minify 选项

请参阅 [babel-preset-minify options](https://github.com/babel/minify/tree/master/packages/babel-preset-minify#options)

### 重写

+ `babel`: 自定义 babel
+ `minifyPreset`: 自定义 minify preset
+ `inputSourceMap`: 输入 Sourcemap
+ `sourceMaps`: [Boolean]

## CLI 选项

```
minify input.js [options]
```

### 单一 preset 选项

对于单一选项来说，你可以在 CLI 中使用 `--optionName` 。

请参阅 [preset's 1-1 options](https://github.com/babel/minify/tree/master/packages/babel-preset-minify#1-1-mapping-with-plugin) 详细列表

例如：

```
minify input.js --mangle false
```

### 嵌套 preset 选项

使用： `--optionName.featureName`

例如：

```sh
minify input.js --mangle.keepClassName --deadcode.keepFnArgs --outFile input.min.js
```

请参阅相应的插件了解其对应所需的选项列表。

### IO 选项

+ `--out-file path/to/file.min.js`: 输出文件名。只能在从标准输入/单输入文件读取时使用。
+ `--out-dir path/to/dir`: 输出路径。
