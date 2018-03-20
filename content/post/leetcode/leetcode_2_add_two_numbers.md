---
title: "Leetcode 2. Add Two Numbers"
date: 2017-06-18T22:13:34+09:00
draft: false
tags: ["Leetcode", "Algorithm"]
categories: ["Leetcode"]
---

# Question

> You are given two **non-empty** linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.
>
> You may assume the two numbers do not contain any leading zero, except the number 0 itself.
>
> Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
>
> Output: 7 -> 0 -> 8

**view on [leetcode.com][question-link]**

--------------------

# Solution

如同在纸上进行加法运算（如图），只要把每一位相加，并且考虑进位的情况即可。

需要注意的是 `ListNode` 的开头表示的是**最低位**。

[![clue-ap1][clue-ap1]][clue-ap1]

在上图中首先使用 2 个指针来分别指向 2 个 `ListNode`，把每一位进行加法运算后，得到该位的值以及 `carry` 的值，并把指针指向下一位，直到下一位是 `null` 为止。

如下图，有几种特殊情况需要特别考虑：

1. 2 个 `ListNode` 的长度不同（在这种情况下某一个指针会先指向 `null`）
2. 某 1 个 `ListNode` 为 `null`，此时结果应为另一个 `ListNode`
3. 在最高位（链表的最末一位）运算后仍然有 `carry`

[![clue-ap2][clue-ap2]][clue-ap2]

# 复杂度

* 时间复杂度：O(n)
* 空间复杂度：O(n)

时间和空间复杂度都与两个 `ListNode` 中较长的那个的长度有关

# Java代码

[LeetCode 2. Add Two Numbers][solution]

``` java
public ListNode solution(ListNode l1, ListNode l2) {
    // result 作为 dummy 头节点，最终返回 result.next
    ListNode result = new ListNode(0);
    ListNode p = l1, q = l2;
    // 当前位的指针
    ListNode current = result;
    int carry = 0;

    while (null != p || null != q) {
        // 若指针为 null 则表示当前位为 0
        // 这是为了应对 2 个链表长度不同，某一个链表先结束的情况
        int x = (null != p) ? p.val : 0;
        int y = (null != q) ? q.val : 0;
        int sum = carry + x + y;
        carry = sum / 10;
        current.next = new ListNode(sum % 10);
        current = current.next;
        if (null != p) {
            p = p.next;
        }
        if (null != q) {
            q = q.next;
        }
    }
    // 别忘记处理最后的 carry
    if (carry > 0) {
        current.next = new ListNode(carry);
    }
    return result.next;
}

```

[question-link]:https://leetcode.com/problems/add-two-numbers/#/description
[clue-ap1]:http://res.cloudinary.com/luoweibinb/image/upload/v1521467842/hugo/leetcode/2-add-two-numbers.png
[clue-ap2]:https://res.cloudinary.com/luoweibinb/image/upload/v1521467145/hugo/leetcode/2-add-two-numbers-2.png
[solution]:https://github.com/Amabel/leetcode/blob/master/002.%20Add%20Two%20Numbers/src/solutions/AddTwoNumbers.java
