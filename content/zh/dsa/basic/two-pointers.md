+++
title = "双指针"
date = "2021-02-25T00:19:30+00:00"
description = "91 天学算法"
tags = ["LeetCode题解","编程刷题","双指针"]
keywords = ["leetcode","数据结构","python","链表","数组","栈","队列","双指针","MatNoble"]
toc = false
mathjax = true
+++

# 目录
- [每日一题](./#每日一题)
  - [x] [876. 链表的中间结点](./#876-链表的中间结点)

## 每日一题
### 876. 链表的中间结点
https://leetcode-cn.com/problems/middle-of-the-linked-list/
#### 题目描述
{{< notice note >}}
给定一个头结点为 `head` 的非空单链表，返回链表的中间结点。

如果有两个中间结点，则返回第二个中间结点。

**示例 1：**  
**输入：** [1,2,3,4,5]  
**输出：** 此列表中的结点 3 (序列化形式：[3,4,5])
返回的结点值为 3 。
{{< /notice >}}
#### 思路
**快慢指针**
- 慢指针：每次走一步
- 快指针：每次走两步

#### 代码
<details>
 <summary> Python </summary>

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def middleNode(self, head: ListNode) -> ListNode:
        slow, fast = head, head
        while fast and fast.next:
            slow, fast = slow.next, fast.next.next
        return slow
```
</details>

#### 复杂度
- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$

<!--
#### 题目描述
{{< notice note >}}

{{< /notice >}}
#### 思路
#### 代码
<details>
 <summary> Python </summary>

```python

```
</details>

#### 复杂度
- 时间复杂度：
- 空间复杂度：
-->