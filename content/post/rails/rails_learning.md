---
author: "Weibin Luo"
title: "Rails 学习笔记"
date: 2018-04-13T15:15:59+09:00
draft: false
tags:
- rails
categories:
- rails
keywords:
thumbnailImage:
thumbnailImagePosition: bottom
---

总之先写下来，等之后再整理
<!--more-->

---

# 创建项目

指定在 app 文件夹下面创建项目

```
$ rails new app
```

在当前目录下创建项目

```
$ rails new ./
```

---

# 创建模型

创建`User`类并且在`User`下创建 3 个字段，并自动生成数据库迁移文件
```
$ rails g model User name:string age:integer email:string
```

若要创建外键，需要使用`references`类型
```
$ rails g model Article title:string content:string user:references
```
会自动在`Article`类下添加`belongs_to`语句，并在迁移文件中指定外键

**注意外键总是在含有`belongs_to`语句的表中**

为了表明`User`和`Article`的关系，需要手动在`User`中添加`has_many`语句

---

# 删除模型

每个`rails g`命令都有对应的`rails d`命令

删除`User`模型
```
$ rails d model User
```

---

# 数据库迁移

根据迁移文件自动会更新数据库（生成表等）
```
$ rails migrate
```

---

# 创建控制器

和创建模型类似

```
$ rails g controller Users
```
会自动生成`users_controller.rb`，注意使用复数形式，rails会自动在后面加上`_controller`

---

# 路由

一般使用`RESTful`架构

在`config/routes.rb`中添加`resources :users`
```
Rails.application.routes.draw do
  resources :users
end
```
确认路径
```
$ rails routes

    users GET    /users(.:format)               users#index
          POST   /users(.:format)               users#create
 new_user GET    /users/new(.:format)           users#new
edit_user GET    /users/:id/edit(.:format)      users#edit
     user GET    /users/:id(.:format)           users#show
          PATCH  /users/:id(.:format)           users#update
          PUT    /users/:id(.:format)           users#update
          DELETE /users/:id(.:format)           users#destroy
     root GET    /                              users#index
```
对服务器的请求会自动匹配路径并执行控制器中相应的方法

---

# 使用 curl 发送请求

## GET

```
$ curl -i http://localhost:3000/users/index.json
```
## POST

---

# 数据库种子文件

---

# API

## jbuilder

---

# 测试 Rsepc
