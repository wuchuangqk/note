# 搭建项目环境

创建项目目录

```sh
npm init -y
```

修改`package.json`

```json
"version": "1.0.0",
"author": "qk",
"description": "原神客户端",
"main": "main.js",
"scripts": {
    "start": "electron ."
}
```

- `main`：改成`main.js`
- `author`和`description`字段必填
- `scripts`添加启动命令（`pnpm start`）

##  安装electron

```sh
pnpm add -D electron@latest
npm i -D electron@latest
```

## 打包

```sh
yarn add --dev @electron-forge/cli
npx electron-forge import
yarn run make
```



An unhandled rejection has occurred inside Forge:
Error: Failed to locate module "debug" from "D:\Programming\WorkSpace\Front Project\yuanshendesktop\node_modules\electron-squirrel-startup"

        This normally means that either you have deleted this package already somehow (check your ignore settings if using electron-packager).  Or your module installation failed.

Electron Forge was terminated. Location:
{}
 ELIFECYCLE  Command failed with exit code 1.
