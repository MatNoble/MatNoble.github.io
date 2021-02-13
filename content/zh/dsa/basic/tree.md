+++
title = "树"
date = "2021-02-12T00:19:30+00:00"
description = "91 天学算法"
tags = ["LeetCode题解","编程刷题","树"]
keywords = ["leetcode","数据结构","python","链表","数组","栈","队列","MatNoble"]
toc = false
mathjax = true
+++

# 目录
- [每日一题](./#每日一题)
  - [x] [104. 二叉树的最大深度](./#104-二叉树的最大深度)
  - [x] [100. 相同的树](./#100-相同的树)
- [扩展](./#扩展)

## 每日一题

### 104. 二叉树的最大深度
https://leetcode-cn.com/problems/maximum-depth-of-binary-tree/
#### 题目描述
{{< notice note >}}
给定一个二叉树，找出其最大深度。

二叉树的深度为根节点到最远叶子节点的最长路径上的节点数。

说明: 叶子节点是指没有子节点的节点。

示例：
给定二叉树 `[3,9,20,null,null,15,7]`，
```
    3
   / \
  9  20
    /  \
   15   7
```
返回它的最大深度 3 。
{{< /notice >}}
#### 思路
简单递归，终止条件: 到达叶节点 `return 0`

#### 代码
<details>
 <summary> Python </summary>

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def maxDepth(self, root: TreeNode) -> int:
        if not root: return 0
        left = self.maxDepth(root.left)
        right = self.maxDepth(root.right)
        res = max(left, right) + 1
        return res
```
</details>

#### 复杂度
- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$

### 100. 相同的树
https://leetcode-cn.com/problems/same-tree/
#### 题目描述
{{< notice note >}}
给你两棵二叉树的根节点 p 和 q ，编写一个函数来检验这两棵树是否相同。

如果两个树在结构上相同，并且节点具有相同的值，则认为它们是相同的。

**示例 1：** 
<img src="https://cdn.jsdelivr.net/gh/MatNoble/Images/20210213165916.png"/>
**输入**: p = [1,2,3], q = [1,2,3]  
**输出** true

**示例 2：**
<img src="https://cdn.jsdelivr.net/gh/MatNoble/Images/20210213165948.png"/>
**输入**: p = [1,2], q = [1,null,2]  
**输出**: false
{{< /notice >}}

#### 思路
- 运用递归
- 关注根节点 `root`
- 然后向下递归 `left` 和 `right`

#### 代码
<details>
 <summary> Python </summary>

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isSameTree(self, p: TreeNode, q: TreeNode) -> bool:
        if not (p or q): 
            return True
        elif not (p and q): 
            return False
        if p.val != q.val:
            return False
        return self.isSameTree(p.left, q.left) and self.isSameTree(p.right, q.right)
```
</details>

#### 复杂度
- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$

## 扩展
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