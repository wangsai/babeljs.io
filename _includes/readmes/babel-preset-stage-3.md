# babel-preset-stage-3

> 包含 stage 3 特性的一组插件的 Babel preset。

Stage 3 的要点是：

> **Stage 3**: 候选提案
>
> **它是什么?** 该提案大部分已经完成，接下来需要收集实现和使用者的反馈，从而取得新的进展。
>
> **要求是？** 规范文本必须完整。指定的审阅者（由 TC39 指定，而非负责人）和 ECMAScript 规范的编者必须在规范上签名。必须至少有两个符合规范的实现（无需默认启用）。
>
> **下一阶段是？** 此后，只有在实现和使用过程中出现了重大问题才能修改。


## 安装

```sh
npm install --save-dev babel-preset-stage-3
```

## 使用

### 通过 `.babelrc` 文件(推荐)

**.babelrc**

```json
{
  "presets": ["stage-3"]
}
```

### 通过 CLI

```sh
babel script.js --presets stage-3
```

### 通过 Node API

```javascript
require("babel-core").transform("code", {
  presets: ["stage-3"]
});
```

## 参考

- Axel Rauschmayer 的文章 “Exploring ES2016 and ES2017” 中 "[The TC39 process for ECMAScript features](http://exploringjs.com/es2016-es2017/ch_tc39-process.html)" 相关章节。
