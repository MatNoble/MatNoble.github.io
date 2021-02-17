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
  - [x] [129. 求根到叶子节点数字之和](./#129-求根到叶子节点数字之和)
  - [x] [513. 找树左下角的值](./#513-找树左下角的值)
  - [x] [297. 二叉树的序列化与反序列化](./#297-二叉树的序列化与反序列化)
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


### 129. 求根到叶子节点数字之和
https://leetcode-cn.com/problems/sum-root-to-leaf-numbers/
#### 题目描述
{{< notice note >}}
给定一个二叉树，它的每个结点都存放一个 `0-9` 的数字，每条从根到叶子节点的路径都代表一个数字。

例如，从根到叶子节点路径 `1->2->3` 代表数字 `123`。

计算从根到叶子节点生成的所有数字之和。

**说明**: 叶子节点是指没有子节点的节点。

**示例 1:**  
输入: `[1,2,3]`
```
    1
   / \
  2   3
```
**输出:** `25`  
**解释:**  
从根到叶子节点路径 `1->2` 代表数字 `12`.  
从根到叶子节点路径 `1->3` 代表数字 `13`.  
因此，数字总和 = `12 + 13 = 25`.
{{< /notice >}}
#### 思路
- DFS 深度优先搜索
  - 递归
  - 遇到 **叶节点**，加入 `self.res`
  - 否则，进行数学进位运算
- BFS 深度优先搜索
  - 使用双端队列，`queue.popleft()` 时间复杂度是 $O(1)$
  - 遇到 **叶节点**，加入 `res`
  - 否则，进行数学进位运算
#### 代码
<details>
 <summary> Python DFS</summary>

```python
class Solution:
    def sumNumbers(self, root: TreeNode) -> int:
        ## DFS
        def dfs(root, sum_):
            if not (root.left or root.right):
                self.res += sum_
                return
            if root.left:
                dfs(root.left, sum_*10 + root.left.val)
            if root.right:
                dfs(root.right, sum_*10 + root.right.val)
        if not root: return 0
        self.res = 0
        dfs(root, root.val)
        return self.res
```
</details>

<details>
 <summary> Python BFS</summary>

```python
class Solution:
    def sumNumbers(self, root: TreeNode) -> int:
        ## BFS
        if not root: return 0
        res, queue = 0, collections.deque()
        queue.append((root, root.val))
        while queue:
            node, sum_ = queue.popleft()
            if not (node.left or node.right):
                res += sum_
            if node.left:
                queue.append((node.left, sum_*10 + node.left.val))
            if node.right:
                queue.append((node.right, sum_*10 + node.right.val))
        return res
```
</details>

#### 复杂度
- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$ # 最坏情况，二叉数退化为单链表

### 513. 找树左下角的值
https://leetcode-cn.com/problems/find-bottom-left-tree-value/
#### 题目描述
{{< notice note >}}
给定一个二叉树，在树的最后一行找到最左边的值。

**示例 1:**
```
输入:

    2
   / \
  1   3

输出:
1
```

**示例 2:**
```
输入:

        1
       / \
      2   3
     /   / \
    4   5   6
       /
      7

输出:
7
```
**注意:** 您可以假设树（即给定的根节点）不为 **NULL**。
{{< /notice >}}
#### 思路
- DFS 深度优先搜索
  - 借助递归
  - 初始化 `self.res = [root.val, 0]`
  - 到达 `叶子节点`：
    - 若 `self.res[1] < k`，更新 `self.res = [node.val, k]`
    - 否则，`return`
  - 否则，向左或向右递归
- BFS 0 广度优先搜索
  - 对 [剑指 Offer 32 - III. 从上到下打印二叉树 III](https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-iii-lcof/) 作小改动
- BFS 1 广度优先搜索
  - 借助双端队列
  - 每层 `由右向左` 遍历
  - 最后一个 `node` 即为所求

#### 代码
<details>
 <summary> Python DFS</summary>

```python
class Solution:
    def findBottomLeftValue(self, root: TreeNode) -> int:
        ## DFS
        def dfs(node, k):
            if not (node.left or node.right):
                if self.res[1] < k:
                    self.res = [node.val, k]
                return
            if node.left:  dfs(node.left, k+1)  # 向左递归
            if node.right: dfs(node.right, k+1) # 向右递归
        self.res = [root.val, 0]
        dfs(root, 0)
        return self.res[0]
```
</details>

<details>
 <summary> Python BFS 0</summary>

```python
class Solution:
    def findBottomLeftValue(self, root: TreeNode) -> int:
        ## BFS 0
        res, queue = [], collections.deque()
        queue.append((root, 0))
        while queue:
            node, k = queue.popleft()
            if k >= len(res): res.append([])
            res[k].append(node.val)
            if node.left:
                queue.append((node.left, k+1))
            if node.right:
                queue.append((node.right, k+1))
        return res[-1][0]
```
</details>

<details>
 <summary> Python BFS 1</summary>

```python
class Solution:
    def findBottomLeftValue(self, root: TreeNode) -> int:
        ## BFS 1
        queue = collections.deque()
        queue.append(root)
        while queue:
            node = queue.popleft()
            if node.right:
                queue.append(node.right)
            if node.left:
                queue.append(node.left)
        return node.val
```
</details>

#### 复杂度
- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$

### 297. 二叉树的序列化与反序列化
https://leetcode-cn.com/problems/serialize-and-deserialize-binary-tree
#### 题目描述
{{< notice note >}}
序列化是将一个数据结构或者对象转换为连续的比特位的操作，进而可以将转换后的数据存储在一个文件或者内存中，同时也可以通过网络传输到另一个计算机环境，采取相反方式重构得到原数据。

请设计一个算法来实现二叉树的序列化与反序列化。这里不限定你的序列 / 反序列化算法执行逻辑，你只需要保证一个二叉树可以被序列化为一个字符串并且将这个字符串反序列化为原始的树结构。

**示例 1：**
<img src="https://cdn.jsdelivr.net/gh/MatNoble/Images/20210217155428.png"/>
**输入**：`root = [1,2,3,null,null,4,5]`  
**输出**：`[1,2,3,null,null,4,5]`

**示例 2：**
**输入**：`root = []`  
**输出**：`[]`
{{< /notice >}}
#### 思路
将 `None` 补充为 `X`
- DFS
  - 序列化：处理根节点，将子树交给递归
  - 反序列化：构建二叉树
- BFS
  - 序列化：常规双端队列
  - **反序列化**：
    - `data`: 序列化节点列表（包含`X`）
    - `queue`: 层序存储非空节点
#### 代码
<details>
 <summary> Python DFS </summary>

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Codec:

    def serialize(self, root):
        """Encodes a tree to a single string.
        :type root: TreeNode
        :rtype: str
        """
        if not root: return 'X'
        return str(root.val) + ',' + self.serialize(root.left) + ',' + self.serialize(root.right)
        

    def deserialize(self, data):
        """Decodes your encoded data to tree.
        :type data: str
        :rtype: TreeNode
        """
        data = collections.deque(data.split(','))
        root = self.buildTree(data)
        return root

    
    def buildTree(self, data):
        val = data.popleft()
        if val == 'X': return None
        node = TreeNode(val)
        node.left  = self.buildTree(data)
        node.right = self.buildTree(data)
        return node
        

# Your Codec object will be instantiated and called as such:
# codec = Codec()
# codec.deserialize(codec.serialize(root))
```
</details>

<details>
 <summary> Python BFS </summary>

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Codec:

    def serialize(self, root):
        """Encodes a tree to a single string.
        :type root: TreeNode
        :rtype: str
        """
        if not root: return []
        res, queue = '', collections.deque()
        queue.append(root)
        while queue:
            node = queue.popleft()
            if not node:
                res += 'X,'
            else:
                res += str(node.val) + ','
                queue.append(node.left)
                queue.append(node.right)
        return res
        

    def deserialize(self, data):
        """Decodes your encoded data to tree.
        :type data: str
        :rtype: TreeNode
        """
        if not data: return None
        data = collections.deque(data.split(','))
        root = TreeNode(data.popleft())
        queue = collections.deque()
        queue.append(root)
        while queue:
            node = queue.popleft()
            if data:
                val = data.popleft()
                if val != 'X':
                    node.left = TreeNode(val)
                    queue.append(node.left)
            if data:
                val = data.popleft()
                if val != 'X':
                    node.right = TreeNode(val)
                    queue.append(node.right)
        return root
        

# Your Codec object will be instantiated and called as such:
# codec = Codec()
# codec.deserialize(codec.serialize(root))
```
</details>

#### 复杂度
- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$


## 扩展

### 剑指 offer

<img src="https://cdn.jsdelivr.net/gh/MatNoble/Images/20210217161519.png"/>

链接在这里 [🔗](https://leetcode-cn.com/problemset/lcof/?topicSlugs=tree)

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