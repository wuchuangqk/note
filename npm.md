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



# 镜像

查看镜像

```sh
npm config get registry
```

淘宝镜像

```sh
npm config set registry http://registry.npm.taobao.org/
```

官网镜像

```sh
npm config set registry https://registry.npmjs.org/
```



# peerDependencies

peer：同等

例如elementui依赖vue，如果把vue写在dependencies，那么项目自身有一个vue依赖，elementui也有一个vue依赖，导致同一个包下载两次。

```html
my-project 
| - node_modules    
	| - vue    
		| - element-ui        
			| - node_modules            
				| - vue
```

Dependencies告诉npm，让项目来下载这个依赖，依赖包使用项目的依赖。



1. 主版本号(major)：当你做了不兼容的API修改
2. 次版本号(minor)：当你做了向下兼容的功能性新增
3. 修订号(patch)：当你做了向下兼容的问题修正

先行版本号是加到修订号的后面，作为版本号的延伸；当要发行大版本或核心功能时，但不能保证这个版本完全正常，就要先发一个先行版本。

先行版本号的格式是在修订版本号后面加上一个连接号（-），再加上一连串以点（.）分割的标识符，标识符可以由英文、数字和连接号（[0-9A-Za-z-]）组成。例如：

```text
1.0.0-alpha
1.0.0-alpha.1
1.0.0-0.3.7
```

常见的先行版本号有：

1. alpha：不稳定版本，一般而言，该版本的Bug较多，需要继续修改，是测试版本
2. beta：基本稳定，相对于Alpha版已经有了很大的进步，消除了严重错误
3. rc：和正式版基本相同，基本上不存在导致错误的Bug
4. release：最终版本



在package.json的一些依赖的版本号中，我们还会看到`^`、`~`或者`>=`这样的标识符，或者不带标识符的，这都代表什么意思呢？

1. 没有任何符号：完全百分百匹配，必须使用当前版本号
2. 对比符号类的：>(大于) >=(大于等于) <(小于) <=(小于等于)
3. 波浪符号`~`：固定主版本号和次版本号，修订号可以随意更改，例如`~2.0.0`，可以使用 2.0.0、2.0.2 、2.0.9 的版本。
4. 插入符号`^`：固定主版本号，次版本号和修订号可以随意更改，例如`^2.0.0`，可以使用 2.0.1、2.2.2 、2.9.9 的版本。
5. 任意版本*：对版本没有限制，一般不用
6. 或符号：||可以用来设置多个版本号限制规则，例如 >= 3.0.0 || <= 1.0.0