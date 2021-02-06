+++
title = "链表"
date = "2021-02-06T00:19:30+00:00"
description = "91 天学算法"
tags = ["LeetCode题解","编程刷题"]
keywords = ["leetcode","数据结构","python","链表","数组","栈","队列","MatNoble"]
toc = false
mathjax = true
+++

# 目录
- [每日一题](./#每日一题)
  - [x] [61. 旋转链表](#61-旋转链表)

## 每日一题

### 61. 旋转链表
https://leetcode-cn.com/problems/rotate-list/
#### 题目描述
{{< notice note >}}
给定一个链表，旋转链表，将链表每个节点向右移动 `k` 个位置，其中 `k` 是非负数。

示例 1:  
输入: 1->2->3->4->5->NULL, k = 2  
输出: 4->5->1->2->3->NULL  
解释:  
向右旋转 1 步: 5->1->2->3->4->NULL  
向右旋转 2 步: 4->5->1->2->3->NULL

示例 2:  
输入: 0->1->2->NULL, k = 4  
输出: 2->0->1->NULL  
解释:  
向右旋转 1 步: 2->0->1->NULL  
向右旋转 2 步: 1->2->0->NULL  
向右旋转 3 步: 0->1->2->NULL  
向右旋转 4 步: 2->0->1->NULL
{{< /notice >}}
#### 思路
- 首先计算链表长度，然后令：`k = k % n`
- 然后利用 `快慢指针`，当快指针走 `k` 步后，慢指针开始走，当快指针指向链表尾时，停止

#### 代码
<details>
 <summary> Python </summary>

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def rotateRight(self, head: ListNode, k: int) -> ListNode:
        if not (head and head.next and k): return head
        cur, n = head, 0
        while cur:
            cur = cur.next
            n += 1
        k = k % n
        if k == 0: return head
        fast = slow = head
        for _ in range(k): fast = fast.next
        while fast.next:
            fast, slow = fast.next, slow.next
        newHead = slow.next
        slow.next = None
        fast.next = head
        return newHead
```
</details>

#### 复杂度
- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$