---
title: 两数相加-LeetCode
top: false
cover: false
categories: LeetCode
tags:
  - 链表
  - 数学
keywords: 两数相加
abbrlink: b2bb6df8
date: 2020-10-20 15:16:10
---

    来源：力扣（LeetCode）
    链接：https://leetcode-cn.com/problems/add-two-numbers/

## 题目
给出两个 非空 的链表用来表示两个非负的整数。其中，它们各自的位数是按照 逆序 的方式存储的，并且它们的每个节点只能存储 一位 数字。

如果，我们将这两个数相加起来，则会返回一个新的链表来表示它们的和。

您可以假设除了数字 0 之外，这两个数都不会以 0 开头。


## 示例
输入：(2 -> 4 -> 3) + (5 -> 6 -> 4)
输出：7 -> 0 -> 8
原因：342 + 465 = 807

## 解题
```java
public class ListNode {
    int val;
    ListNode next;

    ListNode(int x) {
        val = x;
    }
}
```
### 两次遍历
```java
/**
 * 两次遍历
 * 第一次遍历：两个链表对应每个节点分别取和，若含有空节点则空节点取0，产生一个新链表。
 * 第二次遍历：对取完和的新链表遍历，判断当前的val是否大于等于10，大于或等于则其自身-10其next加1，若next为空则新建0节点。
 */
public class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode rs = new ListNode(l1.val + l2.val);

        l1 = l1.next;
        l2 = l2.next;
        ListNode temp = rs;
        while (l1 != null || l2 != null) {
            int a = 0;
            int b = 0;
            if (l1 != null) {
                a = l1.val;
            }
            if (l2 != null) {
                b = l2.val;
            }

            int t = a + b;
            temp.next = new ListNode(t);
            temp = temp.next;
            if (l1 != null) {
                l1 = l1.next;
            }
            if (l2 != null) {
                l2 = l2.next;
            }
        }

        temp = rs;
        while (temp != null) {
            if (temp.val >= 10) {
                temp.val = temp.val - 10;
                if (temp.next == null) {
                    temp.next = new ListNode(0);
                }
                temp.next.val = temp.next.val + 1;
            }
            temp = temp.next;
        }

        return rs;
    }
}
```
