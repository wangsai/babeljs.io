---
layout: docs
title: Env preset
description: 根据你支持的环境自动决定适合你的 Babel 插件的 Babel preset。它使用了 compat-table
permalink: /docs/plugins/preset-env/
package: babel-preset-env
package_source: babel-preset-env
---

{% capture readme %}
  {% include readmes/babel-preset-env.md %}
{% endcapture %}

{{ readme
    | newline_to_br
    | split: "<br />"
    | shift | shift | shift | shift
    | join: "<br />"
    | remove: "<br />"
    | markdownify
}}
