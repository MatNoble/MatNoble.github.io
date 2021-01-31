+++
title = "数组，栈，队列"
date = "2021-01-27T00:19:30+00:00"
description = "91 天学算法"
tags = ["LeetCode题解","编程刷题"]
keywords = ["leetcode","数据结构","python","数组","栈","队列","MatNoble"]
toc = false
mathjax = true
+++

# 目录
- [每日一题](./#每日一提)
  - [x] [989. 数组形式的整数加法](.//#989-数组形式的整数加法)
- [数组扩展](./#数组扩展)
  - [x] [75. 颜色分类](./#75-颜色分类)
  - [ ] [28. 实现 strStr()]
  - [ ] [380. 常数时间插入、删除和获取随机元素]
  - [x] [66. 加一](./#66-加一)
  - [x] [821. 字符的最短距离](./#821-字符的最短距离)
- [栈扩展](./#栈扩展)
  - [ ] [946. 验证栈序列]
- [队列扩展](./#队列扩展)  
  - [ ] [155. 最小栈]

## 每日一题

### 989. 数组形式的整数加法
### 题目描述
{{< notice note >}}
对于非负整数 `X` 而言，`X` 的数组形式是每位数字按从左到右的顺序形成的数组。例如，如果 `X = 1231`，那么其数组形式为 `[1,2,3,1]`。

给定非负整数 `X` 的数组形式 `A`，返回整数 `X+K` 的数组形式。

示例 1：  
`输入：A = [1,2,0,0], K = 34`  
`输出：[1,2,3,4]`  
`解释：1200 + 34 = 1234`

示例 2：  
`输入：A = [2,7,4], K = 181`
`输出：[4,5,5]`  
`解释：274 + 181 = 455`

示例 3：
`输入：A = [2,1,5], K = 806`
`输出：[1,0,2,1]`
`解释：215 + 806 = 1021`

示例 4：  
`输入：A = [9,9,9,9,9,9,9,9,9,9], K = 1`  
`输出：[1,0,0,0,0,0,0,0,0,0,0]`  
`解释：9999999999 + 1 = 10000000000`
 

提示：

- `1 <= A.length <= 10000`
- `0 <= A[i] <= 9`
- `0 <= K <= 10000`
- `如果 A.length > 1，那么 A[0] != 0`


来源：力扣（LeetCode）  
链接：https://leetcode-cn.com/problems/add-to-array-form-of-integer  
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
{{< /notice >}}

### 思路

- 取个位数：`K % 10`
- 去掉个位数：`K \\ 10`
- 用 `count` 记录进位
- 考虑两种情形：
  - `len(A) >= len(K)`
  - `len(A) <  len(K)`

### 代码
```python
from typing import List
class Solution:
    def addToArrayForm(self, A: List[int], K: int) -> List[int]:
        i, n, count = -1, len(A), 0
        while -i < n+1 and (K or count):
            temp = A[i] + count + K % 10
            A[i], count = temp % 10, temp // 10
            K = K // 10
            i -= 1
        while K: # 若 K 长于 A
            temp = count + K % 10
            A.insert(0, temp % 10)
            count = temp // 10
            K = K // 10
        return A if count == 0 else [count]+A

mat = Solution()
A = [1,1]
K = 11
K = 9
# K = 99
mat.addToArrayForm(A, K)
```

### 复杂度
- 时间复杂度：$O(m)$, `m` 为 `K` 的位数
- 空间复杂度：$O(1)$

### 66. 加一

#### 题目描述
{{< notice note >}}
给定一个由整数组成的非空数组所表示的非负整数，在该数的基础上加一。  最高位数字存放在数组的首位， 数组中每个元素只存储单个数字。  你可以假设除了整数 0 之外，这个整数不会以零开头。

示例 1:  
输入: [1,2,3]  
输出: [1,2,4]  
解释: 输入数组表示数字 123。

示例 2:  
输入: [4,3,2,1]  
输出: [4,3,2,2]  
解释: 输入数组表示数字 4321。

来源：力扣（LeetCode）  
链接：https://leetcode-cn.com/problems/plus-one  
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
{{< /notice >}}

#### 思路  
在数组上做竖式加法，用 `carry` 来表示进位，反向遍历数组。  

遍历结束条件：
- 遍历中，遇到 `carry` 为 0 的时候，直接 `return digits`
- 遍历结束，此时 `carry` 必不为 0 (等于 1)，返回 `return [carry] + digits`

#### 代码
```python
from typing import List
class Solution:
    def plusOne(self, digits: List[int]) -> List[int]:
        carry = 1
        for i in range(len(digits) - 1, -1, -1):
            digits[i], carry = (carry + digits[i]) % 10, (carry + digits[i]) // 10
            if not carry: return digits
        return [carry] + digits

mat = Solution()
digits = [9, 9, 9]
# digits = [0]
# digits = [0, 0]
mat.plusOne(digits)
```

#### 复杂度
- 时间复杂度：$O(N)$, N 为数组长度。
- 空间复杂度：$O(1)$。

### 821. 字符的最短距离

#### 题目描述

{{< notice note >}}
给定一个字符串 S 和一个字符 C。返回一个代表字符串 S 中每个字符到字符串 S 中的字符 C 的最短距离的数组。

示例 1:  
输入: S = "loveleetcode", C = 'e'  
输出: [3, 2, 1, 0, 1, 0, 0, 1, 2, 2, 1, 0]

说明:  
字符串 S 的长度范围为 [1, 10000]。  
C 是一个单字符，且保证是字符串 S 里的字符。  
S 和 C 中的所有字母均为小写字母。

来源：力扣（LeetCode）  
链接：https://leetcode-cn.com/problems/shortest-distance-to-a-character  
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
{{< /notice >}}

#### 思路

两次遍历：
1. 左 $\to$ 右，创建 `res`  
`res[i]` 记录 `i` 处距离左侧最近的字符 `C` 的距离。若左侧没有 `C`，则记录为 `len(S)`。比如：
    - `S = "aabacbd", C = 'b'`
    - `res = [7, 7, 0, 1, 2, 0, 1]`
2. 右 $\to$ 左，更新 `res`  
`if res[i] > res[i+1]+1: res[i] = res[i+1] + 1`
    - `res = [7, 7, 0, 1, 2, 0, 1]`
    - `res = [2, 1, 0, 1, 1, 0, 1]`

#### 代码
```python
from typing import List
class Solution:
    def shortestToChar(self, S: str, C: str) -> List[int]:
        n = len(S)
        res = [n]*n
        # first loop
        i = 0
        while S[i] != C[0]: i += 1
        while i < n:
            res[i] = 0 if S[i] == C[0] else res[i-1]+1
            i += 1
        # second loop
        i -= 2
        while i > -1:
            if res[i+1]+1 < res[i]: res[i] = res[i+1]+1 
            i -= 1
        return res

mat = Solution()
S = "loveleetcode"
C = 'e'

S = "aaba"
C = "b"
mat.shortestToChar(S, C)
```

#### 复杂度
- 时间复杂度：$O(N)$, N 为 S 的长度
- 空间复杂度：$O(1)$ (暂时有些疑问)

<hr />

## 数组扩展

### 75. 颜色分类

#### 题目描述

{{< notice note >}}
给定一个包含红色、白色和蓝色，一共 n 个元素的数组，原地对它们进行排序，使得相同颜色的元素相邻，并按照红色、白色、蓝色顺序排列。

此题中，我们使用整数 0、1 和 2 分别表示红色、白色和蓝色。  
注意: 不能使用代码库中的排序函数来解决这道题。

示例:  
输入: [2,0,2,1,1,0]
输出: [0,0,1,1,2,2]

进阶：  
一个直观的解决方案是使用计数排序的两趟扫描算法。  
首先，迭代计算出0、1 和 2 元素的个数，然后按照0、1、2的排序，重写当前数组。你能想出一个仅使用常数空间的一趟扫描算法吗？

来源：力扣（LeetCode）  
链接：https://leetcode-cn.com/problems/sort-colors  
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
{{< /notice >}}

#### 思路

利用双指针 `zero` 和 `two`：
- `[0, zero]` 闭区间内存储 `0`
- `(zero，two]` 左开右闭是未处理部分
- `(two, -1]` 左开右闭内存储 `2`

具体地，初始化 `zero，two = -1, len(nums)-1`, 然后以 `i=0` 遍历数组:
```python
if nums[i] 等于 0：
    zero += 1
    交换 nums[i] 和 nums[zero] # zero 向前一步，并保证 nums[zero] = 0
    i += 1
elif nums[i] 等于 1：
    i += 1
elif nums[i] 等于 2:
    交换 nums[i] 和 nums[two] 
    two -= 1 # two 后退一步， i 不变                     
```
注意： 区间 `(zero, i)` 之间的都是 `1`

#### 代码
```python
from typing import List
class Solution:
    def sortColors(self, nums: List[int]) -> None:
        n = len(nums)
        if n == 1: return
        def swap(nums, i, j):
            nums[i], nums[j] = nums[j], nums[i]
        i, zero, two = 0, -1, n-1
        while i <= two:
            if nums[i] == 0:
                zero += 1
                swap(nums, i, zero)
                i += 1
            elif nums[i] == 1:
                i += 1
            else:
                swap(nums, i, two)
                two -= 1
mat = Solution()
nums = [2,0,2,1,1,2]
# nums = [2,0,1]
mat.sortColors(nums)
print(nums)
```

#### 复杂度
- 时间复杂度：$O(N)$, $N$ 为数组长度
- 空间复杂度：$O(1)$

<hr />

## 栈扩展

<hr />

## 队列扩展