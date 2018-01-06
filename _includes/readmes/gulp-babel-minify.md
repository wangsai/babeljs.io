# gulp-babel-minify

## 安装

```sh
npm install gulp-babel-minify --save-dev
```

## 使用

```js
const gulp = require("gulp");
const minify = require("gulp-babel-minify");

gulp.task("minify", () =>
  gulp.src("./build/app.js")
    .pipe(minify({
      mangle: {
        keepClassName: true
      }
    }))
    .pipe(gulp.dest("./dist"));
);
```

## API

```js
gulpBabelMinify(minifyOptions, overrides);
```

### minify 选项

这些都是传递给 minify preset 的。请参阅 https://github.com/babel/minify/tree/master/packages/babel-preset-minify#options. 默认值为 `{}`

### 重写

默认为: `{}`

+ `babel`: 使用自定义的 `babel-core`
+ `minifyPreset`: 使用自定义的 `babel-preset-minify`
