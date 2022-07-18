# .js.map文件

.map是source map文件的扩展命

source map文件是js文件压缩后，文件的变量名替换对应、变量所在位置等元信息数据文件，一般这种文件和min.js主文件放在同一个目录下。 比如压缩后原变量是map，压缩后通过变量替换规则可能会被替换成a，这时source map文件会记录下这个mapping的信息，这样的好处就是说，在调试的时候，如果有一些JS报错，那么浏览器会通过解析这个map文件来重新merge压缩后的js,使开发者可以用未压缩前的代码来调试，这样会给我们带来很大的方便！

# cjs esm iife

- CJS

  CommonJS，只能在 NodeJS 上运行，使用 `require("module")` 读取并加载模块。

  缺点：不支持浏览器，执行后才能拿到依赖信息，由于用户可以动态 require（例如 [react 根据开发和生产环境导出不同代码](https://link.zhihu.com/?target=https%3A//cdn.jsdelivr.net/npm/react%4017.0.1/index.js) 的写法），无法做到提前分析依赖以及 [Tree-Shaking](https://link.zhihu.com/?target=https%3A//rollupjs.org/guide/zh/%23tree-shaking) 。

- IIFE
  [Immediately Invoked Function Expression](https://link.zhihu.com/?target=https%3A//developer.mozilla.org/en-US/docs/Glossary/IIFE)，只是一种写法，可以隐藏一些局部变量，前端人要是不懂这个可能学的是假前端。可以用来代替 UMD 作为纯粹给前端使用的写法。

- ESM
  ECMAScript Module，现在使用的模块方案，使用 `import` `export` 来管理依赖。由于它们只能写在所有表达式外面，所以打包器可以轻易做到分析依赖以及 Tree-Shaking。当然他也支持动态加载（`import()`）。
