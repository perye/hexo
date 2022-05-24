---
title: 最长公共前缀-LeetCode
top: false
cover: false
categories: LeetCode
tags:
  - 字符串
keywords: 最长公共前缀
abbrlink: c5b7784d
date: 2020-10-20 17:40:11
---

```text
来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/longest-common-prefix/
```

## 题目
编写一个函数来查找字符串数组中的最长公共前缀。

如果不存在公共前缀，返回空字符串 ""。

## 示例
示例 1:

输入: ["flower","flow","flight"]
输出: "fl"
示例 2:

输入: ["dog","racecar","car"]
输出: ""
解释: 输入不存在公共前缀。

## 说明
所有输入只包含小写字母 a-z 。

## 解题

### 水平扫描
```java
public String longestCommonPrefix(String[] strs) {
        if (strs.length == 0) {
            return "";
        }
        if (strs.length == 1) {
            return strs[0];
        }
        String pre = "";
        int i = 0;
        while (true) {
            if (strs[0].length() == i) {
                return pre;
            }
            char temp = strs[0].charAt(i);
            for (int k = 1; k < strs.length; k++) {
                if (strs[k].length() == i || temp != strs[k].charAt(i)) {
                    return pre;
                }
            }
            pre += temp;
            i++;
        }
}
```
#### 复杂度分析
时间复杂度:O(n)
