+++
title = "二分法"
date = "2021-03-01T00:20:30+00:00"
tags = ["双指针","编程刷题","二分法"]
keywords = ["leetcode","数据结构","python","数组","binary-search","二分法","MatNoble"]
toc = false
mathjax = true
+++

# 目录
- [每日一题](./#每日一题)
  - [x] [69. x 的平方根](./#69-x-的平方根)
- [推荐](./#推荐题目)
  - [x] [33. 搜索旋转排序数组](./#33-搜索旋转排序数组)
  - [x] [81. 搜索旋转排序数组 II](./#81-搜索旋转排序数组-ii)
### 69. x 的平方根
https://leetcode-cn.com/problems/sqrtx/
#### 题目描述
{{< notice note >}}
实现 `int sqrt(int x)` 函数。

计算并返回 `x` 的平方根，其中 `x` 是非负整数。

由于返回类型是整数，结果只保留整数的部分，小数部分将被舍去。

**示例 1:**  
**输入:** 4  
**输出:** 2

**示例 2:**  
**输入:** 8  
**输出:** 2  
**说明:** 8 的平方根是 2.82842..., 由于返回类型是整数，小数部分将被舍去。
{{< /notice >}}
#### 思路
- 解 $\sqrt{n} \leq \frac{n}{2}$:
  - $n = 0$, `return 0`
  - $1 \leq n \leq 3$, `return 1`
  - $n \geq 4$, 满足 $\sqrt{n} \leq \frac{n}{2}$
- 在 $\left[1, n//2\right]$ 内二分
- 利于..除法..判断: `mid > x/mid`, 避免溢出
#### 代码
<details>
 <summary> Python </summary>

```python
class Solution:
    def mySqrt(self, x: int) -> int:
        if x == 0: return 0
        i, j = 1, x // 2
        while i < j:
            mid = i + (j-i+1) // 2
            if mid > x/mid:
                j = mid - 1
            else: 
                i = mid
        return i
```
</details>

#### 复杂度
- 时间复杂度：$O(logX)$
- 空间复杂度：$O(1)$

### 33. 搜索旋转排序数组
https://leetcode-cn.com/problems/search-in-rotated-sorted-array/
#### 题目描述
{{< notice note >}}
整数数组 `nums` 按升序排列，数组中的值 **互不相同** 。

在传递给函数之前，`nums` 在预先未知的某个下标 `k（0 <= k < nums.length）`上进行了 **旋转**，使数组变为 `[nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]]`（下标 **从 0 开始** 计数）。例如， $[0,1,2,4,5,6,7]$ 在下标 $3$ 处经旋转后可能变为 $[4,5,6,7,0,1,2]$

给你 **旋转后** 的数组 `nums` 和一个整数 `target` ，如果 `nums` 中存在这个目标值 `target`，则返回它的索引，否则返回 $-1$

**示例 1：**  
**输入：** $nums = [4,5,6,7,0,1,2], \ target = 0$  
**输出：** $4$

**示例 2：**  
**输入：** $nums = [4,5,6,7,0,1,2], \ target = 3$  
**输出：** $-1$

**示例 3：**  
**输入：** $nums = [1],\ target = 0$  
**输出：** $-1$

**提示：**
- $1 \leq nums.length \leq 5000$
- $-10^4 \leq nums[i] \leq 10^4$
- `nums` 中的每个值都 **独一无二**
- `nums` 肯定会在某个点上旋转
- $-10^4 \leq target \leq 10^4$
{{< /notice >}}
#### 思路
- 二分法，**每次必须缩小区间，不能去掉可能解**
- `nums[left] <= nums[mid]` $\Longrightarrow$ 左侧为有序序列
<img src="https://cdn.jsdelivr.net/gh/MatNoble/Images/20210301201056.png"/>
- `nums[left] > nums[mid]` $\Longrightarrow$ 右侧为有序序列
<img src="https://cdn.jsdelivr.net/gh/MatNoble/Images/20210301201339.png"/>

#### 代码
<details>
 <summary> Python </summary>

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        left, right = 0, len(nums)-1
        while left <= right:
            mid = left + (right-left)//2
            if nums[mid] == target: return mid
            if nums[left] <= nums[mid]: # 左侧为有序序列
                if nums[left] <= target < nums[mid]:
                    right = mid-1
                else:
                    left  = mid+1
            else:                       # 右侧为有序序列
                if nums[mid] < target <= nums[right]:
                    left  = mid+1
                else:
                    right = mid-1
        return -1
```
</details>

#### 复杂度
- 时间复杂度：$O(logN)$
- 空间复杂度：$O(1)$


### 81. 搜索旋转排序数组 II
https://leetcode-cn.com/problems/search-in-rotated-sorted-array-ii/
#### 题目描述
{{< notice note >}}
假设按照升序排序的数组在预先未知的某个点上进行了旋转。

( 例如，数组 $[0,0,1,2,2,5,6]$ 可能变为 $[2,5,6,0,0,1,2]$ )。

编写一个函数来判断给定的目标值是否存在于数组中。若存在返回 `true`，否则返回 `false`。

**示例 1:**  
**输入:** nums = [2,5,6,0,0,1,2], target = 0  
**输出:** `true`

**示例 2:**  
**输入:** nums = [2,5,6,0,0,1,2], target = 3  
**输出:** `false`
{{< /notice >}}
#### 思路
- 相对于 [33. 搜索旋转排序数组](./#33-搜索旋转排序数组)，本题中**元素可能重复**  
```python
while left < mid and nums[left] == nums[mid]: # 消除重复元素
    left += 1 
```

#### 代码
<details>
 <summary> Python </summary>

```python
class Solution:
    def search(self, nums: List[int], target: int) -> bool:
        left, right = 0, len(nums)-1
        while left <= right:
            mid = left + (right-left)//2
            if nums[mid] == target: return True
            while left < mid and nums[left] == nums[mid]: 
                left += 1 # 消除重复元素
            if nums[left] <= nums[mid]:  # 左侧为有序序列
                if nums[left] <= target < nums[mid]:
                    right = mid-1
                else:
                    left = mid+1
            else:                        # 右侧为有序序列
                if nums[mid] < target <= nums[right]:
                    left = mid+1
                else:
                    right = mid-1
        return False
```
</details>

#### 复杂度
- 时间复杂度：$O(logN)$
- 空间复杂度：$O(1)$

<!-- 模板
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