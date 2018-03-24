---
author: "Weibin Luo"
title: "LeetCode 3. Longest Substring without Repeating Characters"
date: 2017-06-12T18:32:57+09:00
draft: false
tags:
- leetcode
- algorithm
- substring
categories:
- leetcode
keywords:
- leetcode
thumbnailImage: http://res.cloudinary.com/luoweibinb/image/upload/c_scale,w_150/v1521594161/hugo/leetcode/LeetCode_logo.png
thumbnailImagePosition: left
---

Given a string, find the **length** of the **longest substring** without repeating characters.
<!--more-->

**Example:**

Given `"abcabcbb"`, the answer is `"abc"`, which the length is 3.

Given `"bbbbb"`, the answer is `"b"`, which the length is 1.

Given `"pwwkew"`, the answer is `"wke"`, which the length is 3. Note that the answer must be a **substring**, `"pwke"` is a _subsequence_ and not a substring.

**[leetcode.com][question-link]**

--------------------

# Solution

## 解法 1

最直接的解法，列出所有的子字符串 _(substring)_ 并判断其中是否有重复的字符，如果没有重复的字符则记录它的长度，最后输出最大值。

### Complexity

* 时间复杂度：**O(n<sup>3</sup>)**

* 空间复杂度：**O(min(n, m))**

列出所有的子字符串需要的时间为 O(n<sup>2</sup>)， 判断每个子字符串中是否有重复的字符需要的时间为 O(n)，因此总体时间复杂度为 O(n<sup>3</sup>)。

判断是否有重复的字符时，需要 O(k) 的空间来存放子字符串。此处 k 为 `Set` 的大小，取决于字符串的大小 n 或是所有字符 _(the size of the charset / alphabet)_ 的总数 m。（相当于常数复杂度）

### Code

{{< tabbed-codeblock "Longest Substring without Repeating Characters" >}}
<!-- tab java -->
public class LongestSubstingWithoutRepeatingCharacters {
    static int lengthOfLongestSubstring(String s) {
        int n = s.length();
        int ans = 0;
        // 列出所有的子字符串并判断其中是否有重复的字符
        for (int i = 0; i < n; i++)
            for (int j = i + 1; j <= n; j++)
                // 若该子字符串中没有重复的字符，则记录长度并更新长度的最大值
                if (allUnique(s, i, j)) ans = Math.max(ans, j - i);
        return ans;
    }
    // 用于判断字符串中是否有重复的字符
    static boolean allUnique(String s, int start, int end) {
        Set<Character> set = new HashSet<>();
        for (int i = start; i < end; i++) {
            Character ch = s.charAt(i);
            if (set.contains(ch)) return false;
            set.add(ch);
        }
        return true;
    }
}
<!-- endtab -->
{{< /tabbed-codeblock >}}

---

## 解法 2

（用 2 个指针，最多遍历两次字符串）

用 2 个指针 `i` 和 `j`，首先把它们都指向字符串的首位，向右移动指针 `j` 直到 `j` 指向的字符与 `i` 指向的字符相同，此时 `i` 到 `j - 1` 之间的字符串就是一个不含有重复字符的子字符串，记录它的长度并且更新最大长度，最后把 `i` 向右移动 1 作为新的起点。

### Complexity

* 时间复杂度：**O(n)**

* 空间复杂度：**O(1)**

用长度为 256 的数组来存放字符出现的情况，因此空间复杂度与字符串的长度无关，为常量 O(1)。

### Code

{{< tabbed-codeblock "Longest Substring without Repeating Characters" >}}
<!-- tab java -->
public class LongestSubstingWithoutRepeatingCharacters {
    static int lengthOfLongestSubstring_2(String s) {
        if (s == null) {
            throw new IllegalArgumentException("string is null!");
        }

        boolean[] exist = new boolean[256];
        int i= 0;
        int maxLen = 0;

        for (int j=0; j<s.length(); j++) {
            if (exist[s.charAt(j)]) {
                exist[s.charAt(j)] = false;
                // 将 i 加 1，开始统计新的子字符串
                i ++;
            }
            exist[s.charAt(j)] = true;
            maxLen = Math.max(j -i + 1, maxLen);
        }
        return maxLen;
    }
}
<!-- endtab -->
{{< /tabbed-codeblock >}}

---

[question-link]:https://leetcode.com/problems/longest-substring-without-repeating-characters/#/description
[test-cases]:https://github.com/Amabel/leetcode/blob/master/003.%20Longest%20Substring%20Without%20Repeating%20Characters/src/test/TestLongestSubstingWithoutRepeatingCharacters.java
[solution]:https://github.com/Amabel/leetcode/blob/master/003.%20Longest%20Substring%20Without%20Repeating%20Characters/src/solutions/LongestSubstingWithoutRepeatingCharacters.java
