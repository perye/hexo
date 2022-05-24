---
title: Z 字形变换-LeetCode
top: false
cover: false
categories: LeetCode
tags:
  - 字符串
keywords: Z 字形变换
abbrlink: 5f15c7f2
date: 2020-10-20 17:36:23
---

```text
来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/zigzag-conversion/
```

## 题目
将一个给定字符串根据给定的行数，以从上往下、从左到右进行 Z 字形排列。

比如输入字符串为 "LEETCODEISHIRING" 行数为 3 时，排列如下：

    L   C   I   R
    E T O E S I I G
    E   D   H   N
之后，你的输出需要从左往右逐行读取，产生出一个新的字符串，比如："LCIRETOESIIGEDHN"。


## 示例

示例 1:

输入: s = "LEETCODEISHIRING", numRows = 3
输出: "LCIRETOESIIGEDHN"
示例 2:

输入: s = "LEETCODEISHIRING", numRows = 4
输出: "LDREOEIIECIHNTSG"
解释:

    L     D     R
    E   O E   I I
    E C   I H   N
    T     S     G



## 解题

### boolean变量代替求余操作
```java
public class Solution {
    public String convert(String s, int numRows) {
        if (numRows == 1) {
            return s;
        }
        int len = s.length();
        int col = 0;
        int n = 0;
        List<StringBuffer> list = new ArrayList<>();
        for (int i = 0; i < numRows; i++) {
            StringBuffer temp = new StringBuffer();
            list.add(temp);
        }
        while (n < len) {
            int y = col % (numRows - 1);
            if (y == 0) {
                for (int i = 0; i < numRows && n < len; i++) {
                    list.get(i).append(s.charAt(n));
                    n++;
                }
            } else {
                list.get(numRows - 1 - y).append(s.charAt(n));
                n++;
            }
            col++;
        }
        String rs = "";
        for (int i = 0; i < list.size(); i++) {
            rs += list.get(i).toString();
        }
        return rs;
    }

    public static void main(String[] args) {
        System.out.println(new Solution().convert("LEETCODEISHIRING", 4));
    }
}
```
#### 复杂度分析
时间复杂度:O(n)
