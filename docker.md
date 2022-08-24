# container和image

- image相当于类，container是类的实例，是运行时的实体。可被创建、启动、停止、删除、暂停等。
- image提供容器运行时所需的程序、库、资源、配置等文件外，还包含一些为运行时准备的一些配置参数（如匿名卷、环境变量、用户等）



列出所有正在运行的容器

```sh
docker container ls
```

```sh
CONTAINER ID   IMAGE                    COMMAND
9efbbff9a013   docker/getting-started   "/docker-entrypoint.…"
75c6271ace3d   node:16.16               "docker-entrypoint.s…"
```

- `CONTAINER ID`容器ID
- `IMAGE`容器所属镜像

强制退出

```sh
docker container kill [容器ID]
```

新建容器

```sh
docker container run
docker run -it --name node -p 8080:80 -v 本地目录:容器目录 node:16.16
docker run -d --name 容器名称 -p 本地端口:容器端口 -v 本地目录:容器目录 镜像:版本号
```

- -it 不会闪退
- -p 8080:80 本机端口`:`映射镜像端口
- --name 定义容器名称
- -v 目录路径必须是绝对路径，D:\Programming\WorkSpace\\`'`Front Project'\docker`'`:`/app
  - 在powershell里，如果文件夹名有各种，要用`''`包起来
- node:16.16 镜像

启动容器

```sh
docker container start [容器ID]
```

停止容器

```sh
docker container stop [容器ID]
```

进入容器

```sh
docker container exec -it [容器ID] /bin/bash
```



# Dockerfile

新建`Dockerfile`文件（无需后缀）

```sh
FROM node:16.16
COPY . /app
WORKDIR /app
CMD node index.js
```

## COPY

将源文件拷贝到构建的镜像中

```sh
# 将index.js文件拷贝到镜像的/app路径下
COPY index.js /app 
# . 代表所有文件
COPY . /app
# 可以有多个路径
COPY test.txt /doc
```

## WORKDIR

镜像构建时要去从哪个目录下开始（相当于`cd /app/main`）

```sh
# 构建时，会进入这个目录下
WORKDIR /app
```

## CMD

构建时执行的命令（在WORKDIR指定的目录下执行）

- `run` 是在 `docker build` 构建镜像时, 会执行的命令（**打包时执行**）
- `cmd` 是在 `docker run` 创建容器时, 会执行的命令（**创建容器时执行**）

## 构建镜像

```sh
$ docker image build -t koa-demo .
# 或者
$ docker image build -t koa-demo:0.0.1 .
```

- `-t`参数用来指定 image 文件的名字，后面还可以用冒号指定标签。如果不指定，默认的标签就是`latest`。
- `.`最后的那个点表示 Dockerfile 文件所在的路径，上例是当前路径，所以是一个点。

查看镜像

```sh
docker image ls
```

从镜像创建容器

```sh
docker container run koa-demo:0.0.1
```



## 创建镜像和挂载本地目录

```sh
docker run -it --name pnpm --net=host -v D:\Programming\WorkSpace\'Front Project'\docker:/app node:16.17.0
```
