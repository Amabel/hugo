---
author: "Weibin Luo"
title: "Rails: jbuilder 的基础用法"
date: 2018-04-13T14:18:45+09:00
draft: false
tags:
- rails
- jbuilder
- json
categories:
- rails
- jbuilder
keywords:
- rails
- jbuilder
- json
thumbnailImage:
thumbnailImagePosition: bottom
---

在 Rails 中会需要将数据以 json 的格式返回给用户，本文介绍了使用 jbuilder 构建 json 的方法。
<!--more-->

---

# 不使用变量返回 json

## 直接构建 json

如下


```
json.text "my_text"

# output:
# {"text": "my_text"}
```

## set! 方法

使用`set`方法实现嵌套

```
json.set! :tweet1 do
  json.text2 "my_text2"
  # 等于 json.set! :text2 "my_text2"
end

json.set! :tweet3 do
  jaon.text4 "my_text4"
end

# output:
# {"tweet1": {"text2": "my_text2"}, "tweet3": {"text4": "my_text4"} }
```

对同一个`key`赋值两次时会合并

```
json.set! :tweet do
  json.text2 "my_text2"
  # 等于 json.set! :text2 "my_text2"
end

json.set! :tweet do
  jaon.text4 "my_text4"
end

# output:
# {"tweet": {"text2": "my_text2"}, {"text4": "my_text4"} }
```

---

# 使用变量返回 json （单个变量的情况）

## 直接构建 json

直接获取`tweet`中的`text`字段

```
json.text @tweet.text

# output:
# {"text": "my_text"}
```

返回多个值

```
json.text  @tweet.text
json.title @tweet.title

# output:
# {"text": "my_text", "title": "my_title"}
```

将多个结果合并到 1 个`key`中

```
json.tweet @tweet, :text, :title

# output:
# {"tweet": {"text": "my_text", "title": "my_title"}}
```

另一种写法

```
json.tweet do |tweet|
  tweet.title @tweet.title
  tweet.text  @tweet.text
end

# output:
# {"tweet": {"text": "my_text", "title": "my_title"}}
```

也可以省略 `|tweet|`
```
json.tweet do
  tweet.title @tweet.title
  tweet.text  @tweet.text
end

# output:
# {"tweet": {"text": "my_text", "title": "my_title"}}
```

## extract! 方法

指定变量中的字段并返回 json

```
json.extract! @tweet, :text, :title

# output:
# {"text": "my_text", "title": "my_title"}
```

将多个结果合并到 1 个`key`中
```
json.tweet do
  json.extract! @tweet, :text, :title
end

# output:
# {"tweet": {"text": "my_text", "title": "my_title"} }
```

## merge! 方法

在 json 中追加自定义的键值对

```
text_hash = { text: "my_text" }

json.tweet do
  json.title "my_title"
  json.merge! text_hash
end

# output:
# {"tweet": {"title": "my_title", "text": "my_text"} }
```

自动返回所有键值对

```
json.merge! @tweet.attributes

# output:
# {"id": 1, "text": "my_text", "title": "my_title", "user_id": 1}
```

将所有键值对合并后返回

```
json.tweet do
  json.merge! @tweet.attributes
end

# output:
# {"tweet": {"id": 1, "text": "my_text", "title": "my_title", "user_id": 1} }
```

---

# 变量为复数的时候

## array! 方法

直接返回所有变量的键值对

注意返回的是数组

```
json.array! @tweets, :title, :text

# output:
# [{"title": "my_title1", "text": "my_text1"}, {"title": "my_title2", "text": "my_text2"}]
```

或者这样写

```
json.array! @tweets do |tweet|
  json.title tweet.title
  json.text  tweet.text
end

# output:
# [{"title": "my_title1", "text": "my_text1"}, {"title": "my_title2", "text": "my_text2"}]
```

指定字段并返回数组

```
json.tweet do
  json.array! @tweets, :title, :text
end

# output:
# {"tweet": [{"title": "my_title1", "text": "my_text1" }, {"title": "my_title2",  "text": "my_text2"}] }

```

---

# 参考资料
[https://qiita.com/ryouzi/items/06cb0d4aa7b6527b3645](https://qiita.com/ryouzi/items/06cb0d4aa7b6527b3645)
