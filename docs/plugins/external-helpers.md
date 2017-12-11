---
layout: docs
title: 外部 helpers
description:
permalink: /docs/plugins/external-helpers/
package: babel-plugin-external-helpers
---

## 详情

Babel 有一些 helper 函数，如果需要的话，它将被放置在生成的代码的顶部，所以在整个文件中不会内联多次。如果你有多个文件，这可能会成为一个问题，特别是把文件发送到浏览器。gzip缓解了大部分问题，但仍然不理想。

你可以告诉 Babel 不要在你的文件的顶部放置任何声明，相反只需在外部 helper 中引用他们。

### 获取外部 helpers

你需要使用 `babel-cli` 来构建helpers. 你可以安装 `babel-cli` ：

```sh
npm install babel-cli --save-dev
```

将在你的.bin文件中添加 `babel-external-helpers`。

你可以使用下列语句来输出这个文件。

```sh
./node_modules/.bin/babel-external-helpers [options] > helpers.js
```

您需要在执行代码之前导入/注入此文件（以下说明）。

#### 选项

| 选项                        | 默认              | 描述                                 |
| -------------------------- | -------------------- | ------------------------------------------- |
| `-t, --output-type [type]` | `global`             | 设置输出格式: `global`, `umd` 或者 `var` |
| `-l, --whitelist`          |                      | 只包括helpers的白名单        |

### 输出格式

#### global

通过添加 `babelHelpers` 到 `global` or `self`， `global` 输出格式将设置 helpers 为全局变量。

#### umd

`umd` 输出格式用UMD封装 helpers 用以兼容浏览器，CommonJS 和 AMD。

#### var

`var` 输出变量 `babelHelpers` (`var babelHelpers = {}`) 和 helpers 来给它赋值。这种输出格式适合于进一步的处理。

### 注入外部helpers

#### Node

```js
require("babel-core").buildExternalHelpers();
```

将外部 helpers 注入 `global`。

#### 浏览器

```html
<script type="application/javascript" src="your-path-to/babel/external-helpers.js"></script>
```

在浏览器环境中，您可以使用 `<script>` 标签，将 `babelHelpers` 注入 `window` 对象中。

{% include package_readme.html %}
