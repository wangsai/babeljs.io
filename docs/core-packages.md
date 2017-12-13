---
layout: docs
title: Babel 的核心依赖包
description: Babel 项目是作为一个 monorepo 来进行管理的，它由无数 npm 包组成
permalink: /docs/core-packages/
package: babel-core
---

## 其他依赖包

* [Babel-types](babel-types/): Babel Types 是一个为 AST 节点提供的 lodash 类的实用程序库
* [Babel-register](/docs/usage/babel-register/): require 钩子会将自己绑定到 node 的require 上并且能自动即时编译
* [Babel-template](babel-template/): 从一个字符串模板中生成 AST
* [Babel-helpers](babel-helpers/): Babel 转换的帮助函数集合
* [Babel-code-frame](babel-code-frame/): 生成指向源位置包含代码帧的错误
* [Babylon](babylon/): Babylon 是一个用于 Babel 的 JavaScript 解析器

## Core

{% include package_readme.html %}
