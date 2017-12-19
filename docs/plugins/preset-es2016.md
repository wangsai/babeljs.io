---
layout: docs
title: ES2016 preset
description: 只编译 ES2016 的内容（到 ES2015）
permalink: /docs/plugins/preset-es2016/
package: babel-preset-es2016
---

> 如果你想保持最新版本，请使用 [env preset](/docs/plugins/preset-env/)

这个 preset 依赖以下这些插件:

- [transform-exponentiation-operator](/docs/plugins/transform-exponentiation-operator/)

## 基本配置 (使用 CLI)

> 欲了解更多，请查看 [cli](/docs/setup/) 的设置页面及其[使用](/docs/usage/cli/)相关文档.

安装 CLI 及该 preset

```sh
npm install --save-dev babel-cli babel-preset-es2016
```

为 preset 创建 .babelrc 配置文件

```sh
echo '{ "presets": ["es2016"] }' > .babelrc
```

创建要运行的文件

```sh
echo 'console.log(2 ** 3)' > index.js
```

运行它

```sh
./node_modules/.bin/babel-node index.js
```

{% include package_readme.html %}
