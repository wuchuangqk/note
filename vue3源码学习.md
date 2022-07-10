克隆仓库

```shell
git clone git@github.com:vuejs/core.git
```

vue3的包管理器是`pnpm`

# pnpm

全局安装`pnpm`

```shell
npm i pnpm -g
```

安装依赖

```shell
pnpm i
```



# 启动项目

启动命令添加`--sourcemap`

```json
"dev": "node scripts/dev.js --sourcemap",
```

启动项目

```shell
pnpm run dev
```



# packages

与平台无关的包

- compiler-core
- runtime-core
- reactivity(响应式)

浏览器平台的包

- compiler-dom
- runtime-dom

# runtime-dom

在runtime-dom/src/index.ts下有一个重要的方法：`createApp`

createApp做了两件事：

- 调用baseCreateRenderer获得app
- 给app添加mount方法

createApp是一个工厂方法，创建出一个又一个的vue根组件实例，实例之间彼此隔离互不干扰。

根组件实例是应用程序的入口，是组件树最顶层的节点，一切方法都要从实例上调用。



## baseCreateRenderer

runtime-core/src/renderer.ts

## mount
