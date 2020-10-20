---
title: 字符串中的第一个唯一字符-LeetCode
top: false
cover: false
categories: LeetCode
tags:
  - 哈希表
  - 字符串
keywords: 字符串中的第一个唯一字符
abbrlink: 750521b8
date: 2020-10-20 12:37:41
---

    来源：力扣（LeetCode）
    链接：https://leetcode-cn.com/problems/first-unique-character-in-a-string/

## 题目
给定一个字符串，找到它的第一个不重复的字符，并返回它的索引。如果不存在，则返回 -1。

## 示例
s = "leetcode"
返回 0

s = "loveleetcode"
返回 2

提示：你可以假定该字符串只包含小写字母。

## 解题

### 线性时间复杂度解法
```java
class Solution {
    public int firstUniqChar(String s) {
        HashMap<Character, Integer> count = new HashMap<>();
        int n = s.length();
        for (int i = 0; i < n; i++) {
            char c = s.charAt(i);
            count.put(c, count.getOrDefault(c, 0) + 1);
        }
        for (int i = 0; i < n; i++) {
            if (count.get(s.charAt(i)) == 1) {
                return i;
            }
        }
        return -1;
    }
}
```
算法的思路就是遍历一遍字符串，然后把字符串中每个字符出现的次数保存在一个散列表中。这个过程的时间复杂度为 O(N)，其中 N 为字符串的长度。

接下来需要再遍历一次字符串，这一次利用散列表来检查遍历的每个字符是不是唯一的。如果当前字符唯一，直接返回当前下标就可以了。第二次遍历的时间复杂度也是 O(N)。



