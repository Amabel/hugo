---
author: "Weibin Luo"
title: "Java: Scanner 的用法"
date: 2018-03-30T23:10:20+09:00
draft: false
tags:
- java
- inputs
- java library
categories:
- java
- lib
keywords:
- java
- scanner
thumbnailImage:
thumbnailImagePosition: bottom
---

Java 从 1.5 开始添加了 Scanner 类。Scanner 类用于从控制台读取输入，在做 OJ 的题时掌握 Scanner 的用法很重要。
<!--more-->

# 基本用法

首先引入包

```
import java.util.Scanner;
```

new 出实例，指定从标准输入获取数据

```
Scanner sc = new Scanner(System.in);
```

常用的方法：

```
sc.nextInt() // 读取下一个整数（返回 int）
sc.nextLine() // 读取下一行的内容（返回 String）
sc.next() // 读取下一个有效的 token （读取到空格为止，返回字符串）
sc.hasNext() // 检查是否存在下一个有效 token
// ...
```

在上面的方法中传入正则表达式`Pattern`可以直接按正则表达式进行匹配。

---

# 是否关闭 System.in ?

resource 使用完毕后应当随手关闭，否则会占用资源。但是此处若使用`sc.close()`会导致将`System.in`一起关闭。因此使用`System.in`的时候可以考虑不关闭资源，此时应在变量前加上注释来抑制编译器的警告：
```
@SuppressWarnings("resource")
Scanner sc = new Scanner(System.in);
```

如果想在关闭 `Scanner`的同时不想关闭 `System.in`，可以使用 Apache 的 [CloseShieldInputStream](http://commons.apache.org/proper/commons-io/apidocs/org/apache/commons/io/input/CloseShieldInputStream.html)

---

# The try-with-resources Statement

java 1.7 开始提供 try-with-resources Statement。格式如下：
```
try (Scanner sc = new Scanner(System.in)) {
    // 代码
}
```
上面代码可以保证在`try`执行完毕后会关闭其中的所有资源，等价于：
```
try (Scanner sc = new Scanner(System.in)) {
    // 代码
} finally {
    sc.close();
}
```
参考：[The try-with-resources Statement](https://docs.oracle.com/javase/tutorial/essential/exceptions/tryResourceClose.html#suppressed-exceptions)
