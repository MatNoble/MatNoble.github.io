+++
title = "反转链表"
date = "2021-02-27T00:19:30+00:00"
description = "数据结构从 0 到 1"
tags = ["数据结构与算法","编程刷题","链表"]
keywords = ["leetcode","数据结构","反转链表","python","链表","数组","栈","队列","MatNoble"]
toc = true
mathjax = true
+++

## 206. 反转链表
https://leetcode-cn.com/problems/reverse-linked-list/
### 题目描述
{{< notice note >}}
反转一个单链表。

**示例:**  
**输入:** 1->2->3->4->5->NULL  
**输出:** 5->4->3->2->1->NULL

**进阶:**  
你可以迭代或递归地反转链表。你能否用两种方法解决这道题？
{{< /notice >}}
### 思路
### 代码
<details>
 <summary> Python </summary>

```python
class Solution:
    def reverseList(self, head: ListNode) -> ListNode:
        # 迭代
        pre, cur = None, head
        while cur:
            cur.next, pre, cur = pre, cur, cur.next
        return pre

        # # 递归
        # if not (head and head.next): return head
        # newHead = self.reverseList(head.next)
        # head.next.next = head
        # head.next = None
        # return newHead
```
</details>

### 复杂度
- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$(迭代)  $O(n)$(递归)

## 92. 反转链表 II
https://leetcode-cn.com/problems/reverse-linked-list-ii/
### 题目描述
{{< notice note >}}

{{< /notice >}}
### 思路
### 代码
<details>
 <summary> Python </summary>

```python

```
</details>

### 复杂度
- 时间复杂度：
- 空间复杂度：

## 25. K 个一组翻转链表
https://leetcode-cn.com/problems/reverse-nodes-in-k-group/
### 题目描述
{{< notice note >}}

{{< /notice >}}
### 思路
### 代码
<details>
 <summary> Python </summary>

```python

```
</details>

### 复杂度
- 时间复杂度：
- 空间复杂度：