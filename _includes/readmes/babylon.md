<p align="center">
  <img alt="babylon" src="https://raw.githubusercontent.com/babel/logo/master/babylon.png" width="700">
</p>

<p align="center">
  Babylon 是 <a href="https://github.com/babel/babel">Babel</a> 中使用的 JavaScript 解析器。
</p>

 - 默认启用最新的 ECMAScript 版本(ES2017)。
 - 附加注释。
 - 支持 JSX, Flow, Typescript 语法。
 - 支持实验阶段的语法提案(最低支持到 [stage-0](https://github.com/tc39/proposals/blob/master/stage-0-proposals.md) 阶段的 PR).

## 鸣谢

该项目中使用了大量的 [acorn](https://github.com/marijnh/acorn) 和 [acorn-jsx](https://github.com/RReverser/acorn-jsx) 语法，感谢 [@RReverser](https://github.com/RReverser) 和 [@marijnh](https://github.com/marijnh) 出色的工作。

## API

### `babylon.parse(code, [options])`

### `babylon.parseExpression(code, [options])`

`parse()` 将提供的 `code` 解析为完整的 ECMAScript 程序，而 `parseExpression()` 试图解析表达式，并会考虑性能问题。如果有疑问，请使用 `.parse()` 。

### 选项

- **allowImportExportEverywhere**: 默认情况下，`import` 和 `export` 声明只能出现在代码头部。设置该选项为 `true` 时，则允许他们在代码的任何地方使用。

- **allowReturnOutsideFunction**: 默认情况下，顶级的 return 语句会引发错误。设置该选项为 `true` 时，则会接受错误的代码。

- **allowSuperOutsideMethod**: TODO

- **sourceType**: 表明代码应该解析的模式。可以是 `"script"`，`"module"` 或者 `"unambiguous"` 中任意一个。默认为 `"script"`。`"unambiguous"` 将使得 Babylon 尝试根据 ES6 的 `import` 或者 `export` 声明来进行_推测_。具有 ES6 `import` 和 `export` 的文件被认为是 `"module"`，否则被认为是 `"script"` 。

- **sourceFilename**: 将输出的 AST 节点与其源文件名相关联。多用于多个输入文件的 AST 生成代码和 source map 时。

- **startLine**: 默认情况下，解析的第一行代码被视为第 1 行。你可以提供一个行号来作为起始。多用于与其他源工具集成。

- **plugins**: 数组，包含要启用的插件。

- **strictMode**: TODO

- **ranges**: 为每个节点添加 `ranges` 属性: `[node.start, node.end]`

- **tokens**: 将所有解析的 token 添加到 `File` 节点的上的 `tokens` 属性中。

### 输出

Babylon 根据 [Babel AST 的格式][Babel AST format] 生成 AST 。它基于 [ESTree 规范][ESTree spec]，具有以下差别：

> 现在可以使用 `estree` 插件来取消掉这些差别

- [文字][Literal]符号会被替换为[字符串][StringLiteral]，[数字][NumericLiteral]，[布尔][BooleanLiteral]，[Null][NullLiteral]，[正则表达式][RegExpLiteral]
- [属性][Property]符号会被替换为 [ObjectProperty][] 和 [ObjectMethod][]
- [方法定义][MethodDefinition]会被替换为[类方法][ClassMethod]
- [指令][Program]和[语法块][BlockStatement]的 `directives` 字段中包含额外的[指令][Directive]和[指令字符集][DirectiveLiteral]
- [函数表达式][FunctionExpression]中的[类方法][ClassMethod]，[对象属性][ObjectProperty]和[对象方法][ObjectMethod]值属性的属性被强制/带入主方法节点。

JSX 的 AST 代码基于 [Facebook JSX AST][] 添加了一个节点类型:

- `JSXText`

[Babel AST format]: https://github.com/babel/babylon/blob/master/ast/spec.md
[ESTree spec]: https://github.com/estree/estree

[Literal]: https://github.com/estree/estree/blob/master/es5.md#literal
[Property]: https://github.com/estree/estree/blob/master/es5.md#property
[MethodDefinition]: https://github.com/estree/estree/blob/master/es2015.md#methoddefinition

[StringLiteral]: https://github.com/babel/babylon/blob/master/ast/spec.md#stringliteral
[NumericLiteral]: https://github.com/babel/babylon/blob/master/ast/spec.md#numericliteral
[BooleanLiteral]: https://github.com/babel/babylon/blob/master/ast/spec.md#booleanliteral
[NullLiteral]: https://github.com/babel/babylon/blob/master/ast/spec.md#nullliteral
[RegExpLiteral]: https://github.com/babel/babylon/blob/master/ast/spec.md#regexpliteral
[ObjectProperty]: https://github.com/babel/babylon/blob/master/ast/spec.md#objectproperty
[ObjectMethod]: https://github.com/babel/babylon/blob/master/ast/spec.md#objectmethod
[ClassMethod]: https://github.com/babel/babylon/blob/master/ast/spec.md#classmethod
[Program]: https://github.com/babel/babylon/blob/master/ast/spec.md#programs
[BlockStatement]: https://github.com/babel/babylon/blob/master/ast/spec.md#blockstatement
[Directive]: https://github.com/babel/babylon/blob/master/ast/spec.md#directive
[DirectiveLiteral]: https://github.com/babel/babylon/blob/master/ast/spec.md#directiveliteral
[FunctionExpression]: https://github.com/babel/babylon/blob/master/ast/spec.md#functionexpression

[Facebook JSX AST]: https://github.com/facebook/jsx/blob/master/AST.md

### Semver

Babylon 在大多数情况下遵循 semver 。唯一需要注意的是，某些规范遵从性错误的修复可能会在下一个补丁版本中发布。

例如：我们推送了修复早期错误的代码，就像[#107](https://github.com/babel/babylon/pull/107) - 多个文件默认导出多个。这被视为一个错误进行修复，即时它会导致构建失败。

### 案例

```javascript
require("babylon").parse("code", {
  // 以严格模式解析并允许模块声明
  sourceType: "module",

  plugins: [
    // 启用 jsx 和 flow 语法
    "jsx",
    "flow"
  ]
});
```

### 插件

| 插件名 | 代码示例 |
|------|--------------|
| `estree` ([repo](https://github.com/estree/estree)) | n/a |
| `jsx` ([repo](https://facebook.github.io/jsx/)) | `<a attr="b">{s}</a>` |
| `flow` ([repo](https://github.com/facebook/flow)) | `var a: string = "";` |
| `flowComments` ([文档](https://flow.org/en/docs/types/comments/)) | `/*:: type Foo = {...}; */` |
| `typescript` ([repo](https://github.com/Microsoft/TypeScript)) | `var a: string = "";` |
| `doExpressions` | `var a = do { if (true) { 'hi'; } };` |
| `objectRestSpread` ([提案](https://github.com/tc39/proposal-object-rest-spread)) | `var a = { b, ...c };` |
| `decorators` (Stage 1) and `decorators2` (Stage 2 [提案](https://github.com/tc39/proposal-decorators)) | `@a class A {}` |
| `classProperties` ([提案](https://github.com/tc39/proposal-class-public-fields)) | `class A { b = 1; }` |
| `classPrivateProperties` ([提案](https://github.com/tc39/proposal-private-fields)) | `class A { #b = 1; }` |
| `classPrivateMethods` ([提案](https://github.com/tc39/proposal-private-methods)) | `class A { #c() {} }` |
| `exportExtensions` ([提案 1](https://github.com/leebyron/ecmascript-export-default-from)), ([提案 2](https://github.com/leebyron/ecmascript-export-ns-from)) | Proposal 1: `export v from "mod"` Proposal 2: `export * as ns from "mod"` |
| `asyncGenerators` ([提案](https://github.com/tc39/proposal-async-iteration)) | `async function*() {}`, `for await (let a of b) {}` |
| `functionBind` ([提案](https://github.com/zenparsing/es-function-bind)) | `a::b`, `::console.log` |
| `functionSent` | `function.sent` |
| `dynamicImport` ([提案](https://github.com/tc39/proposal-dynamic-import)) | `import('./guy').then(a)` |
| `numericSeparator` ([提案](https://github.com/samuelgoto/proposal-numeric-separator)) | `1_000_000` |
| `optionalChaining` ([提案](https://github.com/tc39/proposal-optional-chaining)) | `a?.b` |
| `importMeta` ([提案](https://github.com/tc39/proposal-import-meta)) | `import.meta.url` |
| `bigInt` ([提案](https://github.com/tc39/proposal-bigint)) | `100n` |
| `optionalCatchBinding` ([提案](https://github.com/babel/proposals/issues/7)) | `try {throw 0;} catch{do();}` |
| `throwExpressions` ([提案](https://github.com/babel/proposals/issues/23)) | `() => throw new Error("")` |
| `pipelineOperator` ([提案](https://github.com/babel/proposals/issues/29)) | `a \|> b` |
| `nullishCoalescingOperator` ([提案](https://github.com/babel/proposals/issues/14)) | `a ?? b` |

### FAQ

#### Babylon 会支持插件系统吗？

以前的 issues：[babel/babel#1351](https://github.com/babel/babel/issues/1351)，[#500](https://github.com/babel/babylon/issues/500)。

我们目前不愿意承诺支持插件的 API 或者由此产生的生态系统(维护 Babel 的插件系统目前足够使用)。目前还不清楚如何使 API 更有效，并且会限制重构和优化代码库的能力。

我们目前对那些想要创建定制语法的用户建议是 fork Babylon 。

要使用自定义解析器，可以通过将其 npm 包名称添加到 `.babelrc`，或者如何使用 JavaScript 。

```json
{
  "parserOpts": {
    "parser": "custom-fork-of-babylon-on-npm-here"
  }
}
```
