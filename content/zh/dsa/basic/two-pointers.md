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
  - [x] [26. 删除排序数组中的重复项](./#26-删除排序数组中的重复项)
  - [ ] []()

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

### 26. 删除排序数组中的重复项
https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array/
#### 题目描述
{{< notice note >}}
给定一个排序数组，你需要在**原地**删除重复出现的元素，使得每个元素只出现一次，返回移除后数组的新长度。

不要使用额外的数组空间，你必须在**原地**修改输入数组并在使用 O(1) 额外空间的条件下完成。

**示例 :**

给定 nums = [0,0,1,1,1,2,2,3,3,4],

函数应该返回新的长度 5, 并且原数组 nums 的前五个元素被修改为 0, 1, 2, 3, 4。

你不需要考虑数组中超出新长度后面的元素。
{{< /notice >}}
#### 思路
- 排序数组
- i 指针更新数组
- j 指针遍历数组

#### 代码
<details>
 <summary> Python </summary>

```python
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        i, j = 0, 0 # 双指针
        while j < len(nums):
            if i == 0 or nums[i-1] != nums[j]:
                nums[i] = nums[j]  # 记录相异
                i += 1
            j += 1
        return i
```
</details>

#### 复杂度
- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$


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