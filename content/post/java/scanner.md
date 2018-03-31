---
author: "Weibin Luo"
title: "Java: Scanner 的用法"
date: 2018-03-30T23:10:20+09:00
draft: false
tags:
- java
- inputs
categories:
- java
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

在上面的方法中传入正则表达式`Pattern`可以直接按正则表达式进行匹配
