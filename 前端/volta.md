# volta

node、npm、yarn的版本管理工具

- 打开开发人员模式：设置-更新和安全-开发者选项-开发人员模式
- 以管理员身份运行终端

# 安装node

语法

```sh
volta install node@version
```

version:

- 不指定版本，默认安装最新版 `volta install node`
- 只指定主版本号，默认安装主版本下的最新版 `volta install node@14`
- 指定完整版本号 `volta install node@16.17.0`



# 已安装的node版本

| node      | npm     |
| --------- | ------- |
| v18.15.0  | 9.5.0   |
| v16.17.0  | 8.15.0  |
| v12.22.12 | 6.14.16 |

# 命令

查看当前使用的版本

```sh
volta list
```

```
⚡️ Currently active tools:

    Node: v16.17.0 (default)
    Tool binaries available: NONE
```

查看所有版本

```sh
volta list all
```

```
⚡️ User toolchain:

    Node runtimes:
        v12.22.12
        v16.17.0
        v18.15.0 (default)

    Package managers:
        npm:
            v8.15.0
        Yarn:
            v1.22.19 (default)
```



# pin

使用pin命令为项目指定node和npm的版本，volta会把版本信息写进package.json

```sh
volta pin node@18.15.0
```

```sh
volta pin npm@9.5.0
```



package.json

```json
"volta": {
  "node": "18.15.0",
  "npm": "9.5.0"
}
```

此时，在项目路径下查看node版本是v18.15.0，而在其他地方查看node版本是v12.22.12

