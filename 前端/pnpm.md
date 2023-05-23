# pnpm是什么

`Performant npm `，即高性能的npm

和npm相比

- 速度快
- 依赖不会每创建一个项目就下载一次（节省空间）



# 官网

[Fast, disk space efficient package manager | pnpm](https://pnpm.io/zh/)

# 安装

```shell
npm install -g pnpm
```

查看版本

```shell
pnpm -v
# 8.3.1
```

# 常用命令

命令 | 作用 | 对比npm
--- | --- | ---
pnpm i | 安装所有依赖 | npm i
pnpm add <pkg> | 安装指定依赖 | npm i <pkg>
pnpm add <pkg> -D | 安装到开发依赖 | npm i <pkg> -D 
pnpm <cmd> | 执行脚本 | npm run <cmd>

# monorepo

多模块(包)管理

```sh
mkdir project-name
```

## 初始化仓库

```sh
pnpm init
```

添加`pnpm-workspace.yaml`

每一行是一个`模块`，`/**`表示packages子级下的目录也是模块

```yaml
packages:
    - 'packages/**'
    - 'examples'
```

- packages：模块目录
- examples：用来调式预览的项目

添加`packages`和`examples`目录

```
project-name
	|--	packages
	|--	examples
```

## 创建模块

```sh
cd packages
mkdir lan-ui
```

初始化环境

```sh
pnpm init
```

编辑packages.json，在"main": "index.js"下添加下列字段

```sh
"module":"es/index.js",
"files": ["es"],
"typings": "es/index.d.ts",
```

- module：es模块的入口（main是cmd模块的入口）
- files：指定哪些目录会发布到npm上
- typings：类型声明文件入口（也可以用types字段）

安装开发依赖

```sh
cd packages/lan-ui
pnpm add vue vite sass typescript @vitejs/plugin-vue vite-plugin-dts -D -w
```

- pnpm add：安装依赖（可以同时安装多个）
- -D：作为开发依赖（安装到devDependencies）
- -w：安装到顶层包，所有模块都可以共享

现在的目录结构

```
project-name
	|--	packages
		|-- lan-ui
		|-- package.json
	|--	examples
	|-- node_modules
	|-- package.json
	|-- pnpm-lock.yaml
	|-- pnpm-workspace.yaml
```

虽然`pnpm add`是在lan-ui目录下执行的，但因为添加了`-w`参数，依赖包被安装到了`project-name`最顶层下，这样一来，packages下的所有模块和examples都可以共享到这些依赖，不用重复安装。

