---
author: "Weibin Luo"
title: "Java: 使用 Deque 模拟栈和队列"
date: 2018-04-01T11:40:32+09:00
draft: false
draft: false
tags:
- java
- data structure
- queue
- stack
- deque
- java library
categories:
- java
- lib
keywords:
- java
- data structure
- queue
- stack
thumbnailImage:
thumbnailImagePosition: bottom
---

在编程时很多时候需要用到栈和队列，自己编码实现比较麻烦。本文介绍如何用 JDK 自带的类来实现栈和队列。
<!--more-->

---

# 关于 Deque

JDK 中使用`Deque (Double ended queue)`接口来模拟栈和队列的相关操作。常用类如`LinkedList`, `ArrayDeque`都实现了`Deque`接口。

![Deque接口](http://res.cloudinary.com/luoweibinb/image/upload/bo_1px_solid_rgb:000/v1522550774/hugo/java/java-deque.png)

### Deque 的用法

引入包：
```
import java.util.Deque;
import java.util.LinkedList;
```

声明时要将`LinkedList`当作`Deque`：

```
Deque<Integer> stack = new LinkedList<>();
stack.addFirst(3); // push
stack.removeFirst; // pop
```

---

# Deque 接口的方法

`Deque`接口提供对集合中的首元素和末尾元素的相关操作。对于一种操作有相应的两种方法，这两种方法的效果基本相同，但是在操作失败时一个会抛出异常`(add / remove / get)`，另一个会返回false`(offer / poll / peek)`。

![Deque方法](http://res.cloudinary.com/luoweibinb/image/upload/v1522551121/hugo/java/deque-methods.png)

---

# Deque 模拟栈

`Deque`中与`Stack`对应的方法：

![Deque-Stack](http://res.cloudinary.com/luoweibinb/image/upload/v1522551613/hugo/java/deque-stack.png)

---

# Deque 模拟队列

`Deque`中与`Queue`对应的方法：

![Deque-Queue](http://res.cloudinary.com/luoweibinb/image/upload/v1522551615/hugo/java/deque-queue.png)

---

更多请戳：[JDK 1.8 官方文档](https://docs.oracle.com/javase/8/docs/api/java/util/Deque.html)
