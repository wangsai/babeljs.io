---
layout: docs
title: Babel 的核心依赖包
description: Babel 核心是一个独立的仓库，其余功能由无数 npm 包提供
permalink: /docs/core-packages/
package: babel-core
---

## 其他依赖包

* [Babel-types](babel-types/): Babel Types 是一个为 AST 节点提供的 lodash 类的实用程序库。
* [Babel-register](/docs/usage/babel-register/): 需要钩子的节点会被自动绑定到对应的钩子上，并且能自动即时编译。
* [Babel-template](babel-template/): 从一个字符串模板中生成 AST。
* [Babel-helpers](babel-helpers/): Babel 转换的帮助函数集合。
* [Babel-code-frame](babel-code-frame/): 生成能指向出现错误原因的代码框架
* [Babylon](babylon/): Babylon 是一个用于 Babel 的 JavaScript 解析器。

## Core

{% include package_readme.html %}
