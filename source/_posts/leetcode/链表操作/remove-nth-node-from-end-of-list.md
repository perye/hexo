---
title: 删除链表的倒数第N个节点-LeetCode
top: false
cover: false
categories: LeetCode
tags:
  - 链表
  - 双指针
keywords: 删除链表的倒数第N个节点
abbrlink: 691a407d
date: 2020-10-20 15:22:36
---

```text
来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/remove-nth-node-from-end-of-list/
```

## 题目
给定一个链表，删除链表的倒数第 n 个节点，并且返回链表的头结点。

## 示例
给定一个链表: 1->2->3->4->5, 和 n = 2.

当删除了倒数第二个节点后，链表变为 1->2->3->5.

## 说明
给定的 n 保证是有效的。

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

### 双指针
```java
public class Solution {

    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode first = dummy;
        ListNode second = dummy;

        for (int i = 1; i <= n + 1; i++) {
            first = first.next;
        }

        while (first != null) {
            first = first.next;
            second = second.next;
        }
        second.next = second.next.next;
        return dummy.next;
    }
}
```