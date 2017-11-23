---
layout: docs
title: 最新 preset
description: 编译所有 ES2015+ 的内容
permalink: /docs/plugins/preset-latest/
package: babel-preset-latest
---

<blockquote class="babel-callout babel-callout-warning">
  <h4>preset-latest 已弃用</h4>
  <p>
    <code>
      { "presets": ["latest"] } === { "presets": ["env"] }
    </code>
  </p>
</blockquote>

> 请使用 [preset-env](/docs/plugins/preset-env/) 代替。

这是一个包含所有年度 preset 的特殊 preset ，因此用户不需要单独指定每个 preset 。

目前包括:

- [es2017](/docs/plugins/preset-es2017/)
- [es2016](/docs/plugins/preset-es2016/)
- [es2015](/docs/plugins/preset-es2015/)

{% include package_readme.html %}
