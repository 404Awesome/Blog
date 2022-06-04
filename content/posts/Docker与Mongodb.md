---
title: "Docker与Mongodb"
toc: true
date: 2022-03-24T16:56:31+08:00
tags: ['Docker', 'Mongodb', 'Node']
---

# 手动方式

## 1. 准备

>  先使用 docker 命令拉取最新的 mongo 镜像
>
> docker pull mongo:latest

## 2. 启动容器

### 方式一

使用以下命令，在启动容器的时候，配置数据库管理员账户，开启用户验证

```bash
docker run --name db -d -p 27017:27017 -e MONGO_INITDB_ROOT_USERNAME=admin  -e MONGO_INITDB_ROOT_PASSWORD=123456 mongo
```

以上的用户名为 admin，密码为 123456，生产环境建议使用复杂的密码，

进入容器

```bash
docker exec -it db /bin/bash
```

操作数据库并验证

```bash
mongo -u admin -p 123456
use admin
db.auth('admin', '123456')
```

返回 1 代表成功, 使用 exit 命令，退出数据库操作



### 方式二

使用以下命令，需在启动后，手动进入容器，进行添加账户操作

```bash
docker run --name db -d -p 27017:27017 mongo --auth
```

进入容器并操作数据库

```bash
docker exec -it db mongo admin
```

添加账户

```
db.createUser({ user:'admin',pwd:'123456',roles:[ { role:'userAdminAnyDatabase', db: 'admin'},"readWriteAnyDatabase"]});
```

测试是否添加成功

```bash
db.auth('admin', '123456')
```

返回 1 代表成功, 使用 exit 命令，退出数据库操作

> 完成以上任意一种后，还需更改 mongod 的配置文件，使其他容器可以访问 mongo 数据库，使用如下命令安装 vim

```bash
apt-get update
apt-get install vim   [Y]确认	
```

使用如下命令修改 mongod 配置文件

```bash
vi etc/mongod.conf.orig
# 修改以下内容
net:
  port: 27017
  bindIp: 127.0.0.1  # 修改前
  bindIp: 0.0.0.0    # 修改后
```

保存并退出容器即可



## 3. 使用 Node 操作 Mongo

### 代码结构

<img src="/img/post/docker/docker与mongo_1.png">

> 监听 3000 端口，请求 api 为 /user，为了方便使用 Get 方式传递参数，将数据持久化到 mongo



<img src="/img/post/docker/docker与mongo_2.png">

> 使用 mongoose 操作 mongo
>
> mongoose.connect("mongodb://账户名:密码@容器名称/数据库?authSource=admin")



<img src="/img/post/docker/docker与mongo_3.png">

> 使用 Dockerfile 打包镜像，步骤如上图所示
>
> docker build -t api .
>
> npm start 命令  ==  nodemon ./src/app.js



### 启动容器

使用以下命令，启动容器并关联 mongo 数据库

```bash
docker run --name nodeapi -d -p 3000:3000 --link db api
```



### 测试功能

打开浏览器，在地址栏输入数据以便于查看效果

<img src="/img/post/docker/docker与mongo_4.png">



> 功能一切正常，通过 Node 容器访问到了 Mongo 数据库



# DockerCompose方式

>  docker-compose.yml 文件如下

<img src="/img/post/docker/docker与mongo_5.png">

> 通过 docker-compose up 命令可以快速启动服务



