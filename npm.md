# package
一个包必须要有一个`package.json`描述文件
# package.json 字段
一个`package.json`必须要有`name`和`version`字段
- name：包名，必须小写，可以用`-`或`_`
- version：版本号`x.x.x`
示例
```json
{
  "name": "my-awesome-package",
  "version": "1.0.0"
}
```
其他可选字段
字段名 | 作用
-- | --
description | 包的描述，便于在npm上被别人搜索
author | 作者名，还可以按以下格式添加邮箱和网站 `姓名 <email@example.com> (http://example.com)`

# 初始化npm开发环境
```shell
npm init -y
```
执行完命令后，npm会自动在项目目录下创建`package.json`

# scope

# 版本
查看npm版本
```cmd
npm -v
```
升級npm到最新版本
```cmd
npm install npm@latest -g
```

# 发布
- 登录npm账号(关掉梯子)
```cmd
npm login
或
npm login --registry https://registry.npmjs.org
```
username: `mzx_qk`  
password: `passqk1050`  
- 发布
```cmd
npm publish --registry https://registry.npmjs.org
```