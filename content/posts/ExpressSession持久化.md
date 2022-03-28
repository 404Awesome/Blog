---
title: ExpressSession数据持久化
toc: true
date: 2022-03-15 21:19:22
tags: ['Express','Session','MongoDB']
---

# 	准备

>  确保本地已开启 MongoDB 服务



# 安装模块

> 需安装以下模块

```sh
npm i connect-mongo -S
npm i express-session -S
```



# 使用案例

```js
let session = require("express-session")
let MongoStore = require("connect-mongo")

module.exports = (app) => {
   app.use(session({
      secret: "NaNaNa",
      resave: false,
      cookie: { maxAge: 8000 },
      saveUninitialized: true,
      store: MongoStore.create({
         mongoUrl: "mongodb://localhost:27017/session"
      })
   }))
}
```

# 注意

> app 为 express 的实例
>
> Cookie.maxAge 需要大于 6000
