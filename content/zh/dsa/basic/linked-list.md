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
  - [x] [61. 旋转链表](./#61-旋转链表)
  - [x] [24. 两两交换链表中的节点](./#24-两两交换链表中的节点)
  - [x] [109. 有序链表转换二叉搜索树](./#109-有序链表转换二叉搜索树)
- [x] [扩展](./#扩展)
  - [x] [21. 合并两个有序链表](./#21-合并两个有序链表)
  - [x] [83. 删除排序链表中的重复元素](./#83-删除排序链表中的重复元素)
  - [ ] [86. 分隔链表]()
  - [ ] [92. 反转链表 II]()
  - [ ] [138. 复制带随机指针的链表]()
  - [ ] [141. 环形链表]()
  - [ ] [142. 环形链表 II]()
  - [ ] [143. 重排链表]()
  - [ ] [148. 排序链表]()
  - [ ] [206. 反转链表]()
  - [ ] [234. 回文链表]()

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

### 24. 两两交换链表中的节点
https://leetcode-cn.com/problems/swap-nodes-in-pairs/
#### 题目描述
{{< notice note >}}
给定一个链表，两两交换其中相邻的节点，并返回交换后的链表。**你不能只是单纯的改变节点内部的值**，而是需要实际的进行节点交换。

示例：  
<img src="https://cdn.jsdelivr.net/gh/MatNoble/Images/20210208121842.png"/>
输入：head = [1,2,3,4]  
输出：[2,1,4,3]

示例 2：  
输入：head = []  
输出：[]

示例 3：  
输入：head = [1]  
输出：[1]

提示：  
- 链表中节点的数目在范围 [0, 100] 内
- 0 <= Node.val <= 100
{{< /notice >}}
#### 思路
当 `pre.next` 和 `pre.next.next` 非空时，交换之
<img src="https://cdn.jsdelivr.net/gh/MatNoble/Images/linked-list.png" width=500/>

#### 代码
<details>
 <summary> Python </summary>

```python
# Definition for singly-linked list.
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next
class Solution:
    def swapPairs(self, head: ListNode) -> ListNode:  
        if not (head and head.next): 
            return head
        res = ListNode()
        pre = res
        pre.next = head
        while pre.next and pre.next.next:
            former, latter = pre.next, pre.next.next
            pre.next, former.next = latter, latter.next
            latter.next = former
            pre = former
        return res.next
```
</details>

#### 复杂度
- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$

### 109. 有序链表转换二叉搜索树
https://leetcode-cn.com/problems/convert-sorted-list-to-binary-search-tree/
#### 题目描述
{{< notice note >}}
给定一个单链表，其中的元素按升序排序，将其转换为高度平衡的二叉搜索树。

本题中，一个高度平衡二叉树是指一个二叉树每个节点 的左右两个子树的高度差的绝对值不超过 1。

**示例:**  
给定的有序链表： [-10, -3, 0, 5, 9],  
一个可能的答案是：[0, -3, 9, -10, null, 5], 它可以表示下面这个高度平衡二叉搜索树：
```
      0
     / \
   -3   9
   /   /
 -10  5
``` 
{{< /notice >}}
#### 思路
链表顺序即为搜索二叉数中序遍历的输出。运用递归中序遍历构建搜索二叉数。

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
    def sortedListToBST(self, head: ListNode) -> TreeNode:
        if not head: return
        # 使用self声明全局变量h, 记住head的位置
        self.h = head
        # 获得链表的长度
        length = 0
        while head:
            length += 1
            head = head.next
        
        # 通过递归，根据中序遍历创建二叉树，左父右；
        # 递归传入当前区间开始、结束索引
        def buildBST(start, end):
            if start > end: return None
            mid = (start + end) // 2
            # 左区间递归创建左子树
            left = buildBST(start, mid - 1)
            # 创建父节点
            root = TreeNode(self.h.val)
            # 创建一个父节点便更新h的位置
            self.h = self.h.next
            # 连接左子树和父节点
            root.left = left
            # 右区间创建右子树
            root.right = buildBST(mid + 1, end)
            return root
        
        return buildBST(0, length - 1)
```
</details>

#### 复杂度
- 时间复杂度：$O(n)$
- 空间复杂度：$O(log N)$

## 扩展

### 21. 合并两个有序链表
https://leetcode-cn.com/problems/merge-two-sorted-lists/

#### 题目描述
{{< notice note >}}
将两个升序链表合并为一个新的 **升序** 链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。 

示例：
<img src="https://cdn.jsdelivr.net/gh/MatNoble/Images/20210208205015.png"/>
**输入**：l1 = [1,2,4], l2 = [1,3,4]  
**输出**：[1,1,2,3,4,4]

提示：  
- 两个链表的节点数目范围是 [0, 50]
- -100 <= Node.val <= 100
- l1 和 l2 均按 **非递减顺序** 排列
{{< /notice >}}
#### 思路
遍历即可
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
    def mergeTwoLists(self, l1: ListNode, l2: ListNode) -> ListNode:
        res = ListNode()
        cur = res
        while l1 and l2:
            if l1.val < l2.val:
                cur.next = l1
                l1 = l1.next
            else:
                cur.next = l2
                l2 = l2.next
            cur = cur.next
        cur.next = l1 if l1 else l2
        return res.next
```
</details>

#### 复杂度
$m, n$ 分别是 l1 和 l2 的长度
- 时间复杂度：$O(min(m,n))$
- 空间复杂度：$O(1)$

### 83. 删除排序链表中的重复元素
https://leetcode-cn.com/problems/remove-duplicates-from-sorted-list/
#### 题目描述
{{< notice note >}}
给定一个排序链表，删除所有重复的元素，使得每个元素只出现一次。

**示例 1:**  
**输入**: 1->1->2  
**输出**: 1->2

**示例 2:**  
**输入**: 1->1->2->3->3  
**输出**: 1->2->3
{{< /notice >}}
#### 思路
创建**哑节点** `pre` 跟在 `cur` 后面，遍历数组。并查询 `cur.val` 是否在创建的 `hashSet` 里
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
    def deleteDuplicates(self, head: ListNode) -> ListNode:
        hashSet = set()
        pre = ListNode()
        pre.next = head
        cur = head
        while cur:
            if cur.val in hashSet:
                pre.next = cur.next
            else:
                pre = cur
                hashSet.add(cur.val)
            cur = cur.next
        return head
```
</details>

#### 复杂度
- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$


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