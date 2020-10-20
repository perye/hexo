---
title: 整数反转-LeetCode
top: false
cover: false
categories: LeetCode
tags:
  - 数学
keywords: 整数反转
abbrlink: a19ce20c
date: 2020-10-20 11:47:41
---

    来源：力扣（LeetCode）
    链接：https://leetcode-cn.com/problems/reverse-integer/

## 题目
给出一个 32 位的有符号整数，你需要将这个整数中每位上的数字进行反转。

## 示例
示例 1:
输入: 123
输出: 321

示例 2:
输入: -123
输出: -321

示例 3:
输入: 120
输出: 21

注意:

假设我们的环境只能存储得下 32 位的有符号整数，则其数值范围为 [−2<sup>31</sup>,  2<sup>31</sup> − 1]。请根据这个假设，如果反转后整数溢出那么就返回 0。


## 解题

### 弹出和推入数字 & 溢出前进行检查
```java
class Solution {
    public int reverse(int x) {
        int rev = 0;
        while (x != 0) {
            int pop = x % 10;
            x /= 10;
            if (rev > Integer.MAX_VALUE/10 || (rev == Integer.MAX_VALUE / 10 && pop > Integer.MAX_VALUE % 10)) return 0;
            if (rev < Integer.MIN_VALUE/10 || (rev == Integer.MIN_VALUE / 10 && pop < Integer.MIN_VALUE % 10)) return 0;
            rev = rev * 10 + pop;
        }
        return rev;
    }
}
```
#### 思路
反转整数的方法可以与反转字符串进行类比。

我们想重复“弹出”x的最后一位数字，并将它“推入”到 rev的后面。最后,rev将与x相反。

要在没有辅助堆栈/数组的帮助下 “弹出” 和 “推入” 数字，我们可以使用数学方法。

```java
//pop operation:
pop = x % 10;
x /= 10;

//push operation:
temp = rev * 10 + pop;
rev = temp;
```
但是，这种方法很危险，因为当 `temp = rev*10+pop`时会导致溢出。
幸运的是，事先检查这个语句是否会导致溢出很容易。
为了便于解释，我们假设rev是正数。
1. 如果temp = rev*10+pop 导致溢出，那么一定有 rev>=INTMAX/10。 
2. 如果 rev>INTMAX/10,那么 temp = rev*10+pop 一定会溢出。
3. 如果 rev=INTMAX/10,那么只要 pop > Integer.MAX_VALUE % 10 时，temp = rev*10+pop 就会溢出。

当rev为负时可以应用类似的逻辑

#### 复杂度分析
     
时间复杂度：O(log(x))，x中大约有 log<sub>10</sub>(x)位数字。
空间复杂度：O(1)。
