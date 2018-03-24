---
author: "Weibin Luo"
title: "LeetCode 23. Merge k Sorted Lists"
date: 2018-03-23T22:34:48+09:00
draft: false
tags:
- leetcode
- algorithm
- sort
- linked list
categories:
- leetcode
keywords:
- leetcode
thumbnailImage: http://res.cloudinary.com/luoweibinb/image/upload/c_scale,w_150/v1521594161/hugo/leetcode/LeetCode_logo.png
thumbnailImagePosition:
---

Merge k sorted linked lists and return it as one sorted list. Analyze and describe its complexity.
<!--more-->

**[leetcode.com][question-link]**

相关问题：[Merge Two Sorted Lists](https://amabel.github.io/2018/03/leetcode-21.-merge-two-sorted-lists/)

---

# Solution

## 解法1 （优先级队列）

把所有元素放入小根堆，依次取出每个元素。要注意的是堆的大小只要设置为 list 的长度，每次取出一个元素之后再把那个元素之后的元素放进堆里就可以了。

---

# Complexity

* 时间复杂度：**O(nlogk)**
* 空间复杂度：**O(k)**

n 为`ListNode`的总个数，k 为`list`的长度 / 堆的大小。对于每个元素，调堆的时间为O(logk)。

---

# Code

[LeetCode 23. Merge k Sorted Lists][solution]

{{< tabbed-codeblock "Merge k Sorted Lists" >}}
<!-- tab java -->
class ListNode {
    int val;
    ListNode next;
    ListNode(int x) {
    	val = x;
    }
}

public class MergekSortedLists {
    static ListNode mergekSortedLists(ListNode[] lists) {
        if (lists == null || lists.length == 0) {
            return null;
        }
        // 小根堆
        PriorityQueue<ListNode> queue = new PriorityQueue<>(lists.length,(a,b)->a.val-b.val);
        // dummy节点
        ListNode dummy = new ListNode(0);
        ListNode currentNode = dummy;

        // 遍历数组把每个元素入队
        for (ListNode listNode : lists) {
            if (listNode != null) {
                queue.add(listNode);
            }
        }
        // 取出最小元素同时把该节点的后面元素入队
        while (!queue.isEmpty()) {
            currentNode.next = queue.poll();
            currentNode = currentNode.next;
            if (currentNode.next != null) {
                queue.add(currentNode.next);
            }
        }
        return dymmy.next;
    }
}
<!-- endtab -->
{{< /tabbed-codeblock >}}

---

[question-link]:https://leetcode.com/problems/merge-k-sorted-lists/description/
[solution]:https://github.com/Amabel/leetcode/blob/master/023.%20Merge%20k%20Sorted%20Lists/src/MergekSortedLists.java
