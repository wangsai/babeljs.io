# babel-preset-stage-1

> 包含 stage 1 特性的一组插件的 Babel preset。

Stage 1 的要点是：

> **Stage 1**: 提案
>
> **它是什么？** 一个新特性的正式提案。
>
>**要求是？** 提案需要确定一个负责人 (称为 champion) 来跟进。负责人或联合负责人必须是 [TC39](https://github.com/tc39/ecma262/blob/master/FAQ.md) 的成员。提案要解决的问题必须描述清楚，提出的解决方案中必须包含示例、API 以及相关的语义和算法。最后，必须明确提案的潜在障碍，例如与其他特性的交互或实现可能面临的挑战。就实现而言，polyfill 和 demo 也是必须的。
>
> **下一阶段是？** 当一个 stage 1 的提案被接受后，TC39 会宣布愿意审查、讨论及促成该提案。接下来的过程中，该提案可能发生大的改变。

## 安装

```sh
npm install --save-dev babel-preset-stage-1
```

## 使用

### 通过 `.babelrc` 文件 (推荐)

**.babelrc**

```json
{
  "presets": ["stage-1"]
}
```

### 通过 CLI

```sh
babel script.js --presets stage-1
```

### 通过 Node API

```javascript
require("babel-core").transform("code", {
  presets: ["stage-1"]
});
```

## 参考
- Axel Rauschmayer 的文章《Exploring ES2016 and ES2017》中 [The TC39 process for ECMAScript features](http://exploringjs.com/es2016-es2017/ch_tc39-process.html) 相关章节。
