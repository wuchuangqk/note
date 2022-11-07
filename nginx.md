# location

语法

```powershell
location [ = | ~ | ~* | ^~ | @ ] path { 
	……
}
```

位置

```
server.location
```

例如，监听3721端口

```properties
server {
	listen 3721;
	location / {}
	location = 50x.html {}
}
```

http://localhost:3721 匹配 /

http://localhost:3721/50x.html 匹配 /50x.html

# root

指定根路径

```
server.location.root
```

例如指定root为html/dist/oa_platform

```
server {
	listen 3721;
	location /oa/ {
		root html/dist/oa_platform
	}
}
```


当匹配/oa/test.html时，相当于从html/dist/oa_platform目录下，找oa/test.html。root + path

| 访问地址                           | 映射地址                           |
| ---------------------------------- | ---------------------------------- |
| http://localhost:3721/oa/test.html | html/dist/oa_platform/oa/test.html |

# alias

为访问路径起别名

```
server.location.alias
```

```
server {
	listen 3721;
	location /oa/ {
		alias html/dist/oa_platform/project
	}
}
```
当匹配/oa/test.html时，从html/dist/oa_platform/project目录下，找test.html。alias replac
| 访问地址                           | 映射地址                        |
| ---------------------------------- | ------------------------------- |
| http://localhost:3721/oa/test.html | html/dist/oa_platform/project/test.html |


# proxy_pass



# try_files

```
location / {
  # html/index.html
  root   html;
  index  index.html index.htm;
  try_files $uri $uri/ /index.html;
}
```

try_files $uri $uri/ /index.html 配置解释：$uri是Nginx的变量，代表访问的路径，例如访问http://localhost:3721/login，$uri变量的值是login，try_files命令会依次从后面的参数中寻找，首先查找是否有login这个文件，如果有就返回这个文件。然后查找是否有/login/这个目录，如果有这个目录，则从这个目录下开始找index.html或index.htm，最后返回/index.html。

在vue单页面应用中，只有一个入口index.html，所以要把所有请求最后都重定向到index.html



