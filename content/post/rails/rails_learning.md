---
author: "Weibin Luo"
title: "Rails 5 学习笔记"
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

{{< alert info >}}
注意外键总是在含有`belongs_to`语句的表中
{{< /alert >}}

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
会自动生成`users_controller.rb`，注意使用复数形式，rails 会在后面加上`_controller`

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

```
$ curl -u "name=bob&email=bob@gmail.com" http://localhost:3000/users/
```

---

# 使用 Postman 发送请求

[Postman](https://www.getpostman.com/) 可用于向服务器发送多种请求

---

# 数据库种子文件

```
rails db:seed
```

---

# API

用 Rails 写 API 的时候需要用到的一些工具


## Jbuilder

[Jbuilder](https://github.com/rails/jbuilder#jbuilder) 用于生成返回的`JSON`文件

关于 Jbuilder 的介绍请戳[这里](https://amabel.github.io/2018/04/rails-jbuilder-%E7%9A%84%E5%9F%BA%E7%A1%80%E7%94%A8%E6%B3%95/)



---

# 测试 RSepc

RSpec 为常用的 Rails 测试框架

（未完工）详细介绍戳[这里](https://amabel.github.io/2018/04/rspec_basic/)

---

# 各种语言的官方文档

中文：[https://ruby-china.github.io/rails-guides/index.html](https://ruby-china.github.io/rails-guides/index.html)

英文：[http://guides.rubyonrails.org/index.html](http://guides.rubyonrails.org/index.html)

日文：[https://railsguides.jp/](https://railsguides.jp/)
