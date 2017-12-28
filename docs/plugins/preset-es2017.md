---
layout: docs
title: ES2017 preset
description: 只编译 ES2017 的内容（到 ES2016）
permalink: /docs/plugins/preset-es2017/
package: babel-preset-es2017
---

> 如果你想保持最新版本，请使用 [env preset](/docs/plugins/preset-env/)

这个 preset 包含以下这些插件:

- [syntax-trailing-function-commas](/docs/plugins/syntax-trailing-function-commas/)
- [transform-async-to-generator](/docs/plugins/transform-async-to-generator/)

## 基本配置 (使用 CLI)

> 欲了解更多，请查看 [cli](/docs/setup/) 的设置页面及其[使用](/docs/usage/cli/)相关文档。

安装 CLI 及该 preset

```sh
npm install --save-dev babel-cli babel-preset-es2017
```

用 preset 创建 .babelrc 配置文件

```sh
echo '{ "presets": ["es2017"] }' > .babelrc
```

创建要运行的文件

```sh
echo 'function a(b,) { console.log("hi"); }; a()' > index.js
```

运行它

```sh
./node_modules/.bin/babel-node index.js
```

{% include package_readme.html %}


