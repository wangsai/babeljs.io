---
layout: docs
title: Env preset
description: Babel preset，根据您支持的环境自动选择适合您的 Babel plugin。使用 compat-table
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
