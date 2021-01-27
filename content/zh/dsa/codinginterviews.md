+++
title = "剑指 Offer"
date = "2021-01-27T00:20:30+00:00"
description = "Python 版"
tags = ["LeetCode刷题"]
keywords = ["leetcode","剑指offer","数据结构","python","数组","栈","队列","MatNoble"]
toc = false
mathjax = true
+++

## 目录

- [x] [03. 数组中重复的数字](./#03-数组中重复的数字)
- [x] [04. 二维数组中的查找](./#04-二维数组中的查找)
- [ ] [05. 替换空格]

## 03. 数组中重复的数字

### 题目描述

{{< notice note >}}
在一个长度为 n 的数组 nums 里的所有数字都在 0～n-1 的范围内。数组中某些数字是重复的，但不知道有几个数字重复了，也不知道每个数字重复了几次。请找出数组中任意一个重复的数字。

示例：  
输入：[2, 3, 1, 0, 2, 5, 3]  
输出：2 或 3 

来源：力扣（LeetCode）  
链接：https://leetcode-cn.com/problems/shu-zu-zhong-zhong-fu-de-shu-zi-lcof  
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
{{< /notice >}}

### 思路

1. 判断“环”出口：`nums[nums[i]] = nums[i]`
2. 归位 `swap(nums, i, nums[i])`  
`j = nums[i]` $\to$ `nums[j] = j`

### 代码

```python
class Solution:
    def findRepeatNumber(self, nums):
        # dict = set()
        # for num in nums:
        #     if num in dict: return num
        #     dict.add(num)
        # return -1
        def swap(nums, i, j):
            temp = nums[i]
            nums[i] = nums[j]
            nums[j] = temp
        n = len(nums)
        i = 0
        while i < n:
            if nums[i] == i:
                i += 1
                continue
            if nums[nums[i]] == nums[i]: return nums[i]
            swap(nums, i, nums[i])
        return -1

mat = Solution()
nums = [2, 3, 1, 0, 2, 5, 3]
mat.findRepeatNumber(nums)
```

### 复杂度
- 时间复杂度：$O(n)$, $n$ 为数组长度
- 空间复杂度：$O(1)$

## 04. 二维数组中的查找

### 题目描述

{{< notice note >}}
在一个 n * m 的二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个高效的函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

示例:  
现有矩阵 matrix 如下：
```
[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]
```
给定 target = 5，返回 true。  
给定 target = 20，返回 false。

来源：力扣（LeetCode）  
链接：https://leetcode-cn.com/problems/er-wei-shu-zu-zhong-de-cha-zhao-lcof  
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
{{< /notice >}}

### 思路

从左下角出发：
1. `if nums[i][j] == target: return True`
2. `if nums[i][j]  < target: j -= 1` 舍弃第 `j` 列，搜索区间向右移
3. `if nums[i][j]  > target: i += 1` 舍弃第 `i` 列，搜索区间向上移

### 代码

```python
class Solution:
    def findNumberIn2DArray(self, matrix, target):
        m = len(matrix)
        if m == 0: return False
        n = len(matrix[0])
        i, j = m-1, 0
        while i >= 0 and j < n:
            if matrix[i][j] < target:
                j += 1
            elif matrix[i][j] > target:
                i -= 1
            else:
                return True
        return False


mat = Solution()
matrix = [
    [1,   4,  7, 11, 15],
    [2,   5,  8, 12, 19],
    [3,   6,  9, 16, 22],
    [10, 13, 14, 17, 24],
    [18, 21, 23, 26, 30]
]
# matrix = []
target = 5
# target = 20
mat.findNumberIn2DArray(matrix, target)
```

### 复杂度
- 时间复杂度：$O(m+n)$
- 时间复杂度：$O(1)$