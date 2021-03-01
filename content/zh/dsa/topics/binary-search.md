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