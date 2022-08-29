# volta

node、npm、yarn的版本管理工具

- 打开开发人员模式：设置-更新和安全-开发者选项-开发人员模式
- 以管理员身份运行终端

# 安装node

- 不指定版本，默认安装最新版
- 只指定主版本号，默认安装主版本下的最新版
- 指定完整版本号

## node16

```sh
volta install node@16
```

- node版本：v12.22.12
- npm版本：6.14.16

## node12

```sh
volta install node@12
```

- node版本：v16.17.0
- npm版本：8.15.0



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



# 为项目单独指定node版本

npm init -y 创建package.json

然后

```sh
volta pin node@16.17.0
volta pin npm@8.15.0
```

volta会把node版本写进package.json

此时，在项目路径下查看node版本是v16.17.0，而在其他地方查看node版本是v12.22.12

