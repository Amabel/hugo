---
author: "Weibin Luo"
title: "LeetCode 21. Merge Two Sorted Lists"
date: 2018-03-23T16:39:58+09:00
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

Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.
<!--more-->

Input: 1->2->4, 1->3->4
Output: 1->1->2->3->4->4

**[leetcode.com][question-link]**

---

# Solution

经典题，用两个指针遍历两个链表，每次移动小的那一个指针，并把小的那个元素添加到返回的链表里。

本题链表的数据结构已经给出，可以先`new`一个dummy节点，就不用单独判断第一个元素，最后返回`dummy.next`就可以了。

对于没有排序过的两个链表，可以考虑先排序之后再用这个算法合并。

---

# Complexity

* 时间复杂度：**O(m + n)**
* 空间复杂度：**O(m + n)**

---

# Code

[LeetCode 21. Merge Two Sorted Lists][solution]

{{< tabbed-codeblock "Merge Two Sorted Lists" >}}
<!-- tab java -->
class ListNode {
    int val;
    ListNode next;
    ListNode(int x) {
    	val = x;
    }
}

public class MergeTwoSortedLists {
    static ListNode mergeTwoLists2(ListNode l1, ListNode l2) {
        if (l1 == null) {
            return l2;
        }
        if (l2 == null) {
            return l1;
        }
        // dummy
        ListNode ret = new ListNode(0);
        ListNode currentNode = ret;

        // remaining elements
        while (l1 != null && l2 != null) {
            if (l1.val < l2.val) {
                currentNode.next = new ListNode(l1.val);
                l1 = l1.next;
            } else {
                currentNode.next = new ListNode(l2.val);
                l2 = l2.next;
            }
            currentNode = currentNode.next;
        }

        // l1 reaches the end
        while (l1 == null && l2 != null) {
            currentNode.next = new ListNode(l2.val);
            l2 = l2.next;
            currentNode = currentNode.next;
        }
        // l2 reaches the end
        while (l1 != null && l2 == null) {
            currentNode.next = new ListNode(l1.val);
            l1 = l1.next;
            currentNode = currentNode.next;
        }
        return ret.next;
        }
    }
}
<!-- endtab -->
{{< /tabbed-codeblock >}}

---

[question-link]:https://leetcode.com/problems/merge-two-sorted-lists/description/
[solution]:https://github.com/Amabel/leetcode/blob/master/021.%20Merge%20Two%20Sorted%20Lists/src/MergeTwoSortedLists.java
