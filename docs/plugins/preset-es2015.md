---
layout: docs
title: ES2015 preset
description: 只会将 ES2015 编译为 ES5
permalink: /docs/plugins/preset-es2015/
package: babel-preset-es2015
---

> 如果你想保持最新版本，请使用 [env preset](/docs/plugins/preset-env/)

这个 preset 中包含以下插件:

- [check-es2015-constants](/docs/plugins/check-es2015-constants/)
- [transform-es2015-arrow-functions](/docs/plugins/transform-es2015-arrow-functions/)
- [transform-es2015-block-scoped-functions](/docs/plugins/transform-es2015-block-scoped-functions/)
- [transform-es2015-block-scoping](/docs/plugins/transform-es2015-block-scoping/)
- [transform-es2015-classes](/docs/plugins/transform-es2015-classes/)
- [transform-es2015-computed-properties](/docs/plugins/transform-es2015-computed-properties/)
- [transform-es2015-destructuring](/docs/plugins/transform-es2015-destructuring/)
- [transform-es2015-duplicate-keys](/docs/plugins/transform-es2015-duplicate-keys/) 
- [transform-es2015-for-of](/docs/plugins/transform-es2015-for-of/)
- [transform-es2015-function-name](/docs/plugins/transform-es2015-function-name/)
- [transform-es2015-literals](/docs/plugins/transform-es2015-literals/)
- [transform-es2015-modules-commonjs](/docs/plugins/transform-es2015-modules-commonjs/)
- [transform-es2015-object-super](/docs/plugins/transform-es2015-object-super/)
- [transform-es2015-parameters](/docs/plugins/transform-es2015-parameters/)
- [transform-es2015-shorthand-properties](/docs/plugins/transform-es2015-shorthand-properties/)
- [transform-es2015-spread](/docs/plugins/transform-es2015-spread/)
- [transform-es2015-sticky-regex](/docs/plugins/transform-es2015-sticky-regex/)
- [transform-es2015-template-literals](/docs/plugins/transform-es2015-template-literals/)
- [transform-es2015-typeof-symbol](/docs/plugins/transform-es2015-typeof-symbol/)
- [transform-es2015-unicode-regex](/docs/plugins/transform-es2015-unicode-regex/)
- [transform-regenerator](/docs/plugins/transform-regenerator/)

## 基础设置 (使用 CLI)

> 可以查看 React 文档中的 [快速配置页](https://doc.react-china.org/docs/hello-world.html)

> 欲了解更多，请查看 [cli](/docs/setup/) 配置以及[用法](/docs/usage/cli/)文档。

安装 CLI 和该 preset

```sh
npm install --save-dev babel-cli babel-preset-es2015
```

为 preset 创建 .babelrc 配置文件

```sh
echo '{ "presets": ["es2015"] }' > .babelrc
```

创建要运行的文件

```sh
echo 'console.log([1, 2, 3].map(n => n + 1))' > index.js
```

执行该文件

```sh
./node_modules/.bin/babel index.js
```

{% include package_readme.html %}
