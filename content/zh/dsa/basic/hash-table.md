+++
title = "哈希表"
date = "2021-02-18T00:19:30+00:00"
description = "91 天学算法"
tags = ["LeetCode题解","编程刷题","哈希表"]
keywords = ["leetcode","数据结构","python","链表","数组","栈","队列","MatNoble"]
toc = false
mathjax = true
+++

# 目录
- [每日一题](./#每日一题)
  - [x] [1. 两数之和](./#1-两数之和)
  - [x] [347. 前 K 个高频元素](./#347-前-k-个高频元素)

## 每日一题
### 1. 两数之和
https://leetcode-cn.com/problems/two-sum
#### 题目描述
{{< notice note >}}
给定一个整数数组 `nums` 和一个整数目标值 `target`，请你在该数组中找出 **和为目标值** 的那 **两个** 整数，并返回它们的数组下标。

你可以假设每种输入只会对应一个答案。但是，数组中同一个元素不能使用两遍。

你可以按任意顺序返回答案。

**示例:**  
**输入：** nums = [2,7,11,15], target = 9  
**输出：** [0,1]  
**解释：** 因为 nums[0] + nums[1] == 9 ，返回 [0, 1] 。
{{< /notice >}}
#### 思路
- 用 **字典(哈希表)** 存储每个数对应的索引及值. 哈希表实现快速查找 $O(1)$
- 当 `target - 当前数` 在 **字典(哈希表)** 中存在时，说明已存储的数和当前数相加可以得到目标值 `target`
- 返回对应的索引 `[hashmap[target - num], idx]`
#### 代码
<details>
 <summary> Python </summary>

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        hashMap={}
        for idx, num in enumerate(nums):
            if (target - num) in hashMap:
                return [hashMap.get(target - num), idx]
            hashMap[num] = idx
```
</details>

#### 复杂度
- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$

### 347. 前 K 个高频元素
https://leetcode-cn.com/problems/top-k-frequent-elements
#### 题目描述
{{< notice note >}}
给定一个非空的整数数组，返回其中出现频率前 **k** 高的元素。

**示例 1:**  
**输入:** nums = [1,1,1,2,2,3], k = 2  
**输出:** [1,2]

**示例 2:**  
**输入:** nums = [1], k = 1  
**输出:** [1]
 
- 你可以假设给定的 k 总是合理的，且 1 ≤ k ≤ 数组中不相同的元素的个数。
- 你的算法的时间复杂度**必须**优于 O(n log n) , n 是数组的大小。
- 题目数据保证答案唯一，换句话说，数组中前 k 个高频元素的集合是唯一的。
- 你可以按任意顺序返回答案。
{{< /notice >}}
#### 思路
#### 代码
<details>
 <summary> Python </summary>

```python
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        dict = collections.Counter(nums) # 计数
        return [v[0] for v in sorted(dict.items(), key=lambda x:x[1])][-k:] # 排序返回
```
</details>

#### 复杂度
- 时间复杂度：$O(NlogN)$
- 空间复杂度：$O(N)$
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