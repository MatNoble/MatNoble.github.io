+++
title = "滑动窗口"
date = "2021-03-01T00:19:30+00:00"
tags = ["双指针","编程刷题","滑动窗口"]
keywords = ["leetcode","数据结构","python","数组","栈","队列","MatNoble"]
toc = false
mathjax = true
+++

# 目录
- [每日一题](./#每日一题)
- [推荐](./#推荐题目)
  - [x] [239. 滑动窗口最大值](./#239-滑动窗口最大值)
  - [x] [3. 无重复字符的最长字串](./#3-无重复字符的最长字串)
  - [ ] [76. 最小覆盖字串](./#76-最小覆盖字串)
  - [ ] [438. 找到字符串中所有字母异位词](./#438-找到字符串中所有字母异位词)
  - [ ] [567. 字符串的排列](./#567-字符串的排列)

### 239. 滑动窗口最大值
https://leetcode-cn.com/problems/sliding-window-maximum/
#### 题目描述
{{< notice note >}}
给你一个整数数组 `nums`，有一个大小为 `k` 的滑动窗口从数组的最左侧移动到数组的最右侧。你只可以看到在滑动窗口内的 `k` 个数字。滑动窗口每次只向右移动一位。

返回滑动窗口中的最大值。

**示例：**  
输入：nums = [1,3,-1,-3,5,3,6,7], k = 3  
输出：[3,3,5,5,6,7]  
解释： 
```
  滑动窗口的位置                最大值
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7
```

**提示：**  
- 1 <= nums.length <= 105
- -104 <= nums[i] <= 104
- 1 <= k <= nums.length
{{< /notice >}}
#### 思路
- 借助**双端队列**。`popleft()` 时间复杂度为 $O(1)$
- **初始化窗口**: 将数组的前 `k` 个数依次加入到双端队列 `d` 中，每次加入前，判断队尾元素与 `num` 比较，保持队列 `d` 是..递减..的
- **滑动窗口**: 遍历 `nums[k:]`， 每次更新 `res`
  - 每次遍历需要判断队列最大值(即队首元素)是否窗口滑动时被“滑”出了，若**是**，则需要 `popleft()`
  - 之后，和初始化窗口中做的一样，保持队列是..递减..的

#### 代码
<details>
 <summary> Python </summary>

```python
class Solution:
    def maxSlidingWindow(self, nums: List[int], k: int) -> List[int]:
        # 双端队列
        d = collections.deque()
        # 初始化窗口
        for num in nums[:k]:
            while d and d[-1] < num: d.pop()
            d.append(num)
        res = [d[0]]
        # 滑动窗口
        for j in range(k, len(nums)):
            if nums[j-k] == d[0]: d.popleft()
            while d and d[-1] < nums[j]: d.pop()
            d.append(nums[j])
            res.append(d[0])
        return res
```
</details>

#### 复杂度
*n 为数组长度, k 为窗口大小*
- 时间复杂度：$O(n)$  
- 空间复杂度：$O(k)$  

### 3. 无重复字符的最长字串
https://leetcode-cn.com/problems/longest-substring-without-repeating-characters
#### 题目描述
{{< notice note >}}
给定一个字符串，请你找出其中不含有重复字符的 `最长子串` 的长度。

示例 1:  
输入: s = "abcabcbb"  
输出: 3  
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。

示例 2:  
输入: s = "bbbbb"  
输出: 1  
解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。

示例 3:  
输入: s = "pwwkew"  
输出: 3  
解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。  
**请注意** 你的答案必须是 `子串` 的长度，"pwke" 是一个子序列，不是子串。

示例 4:  
输入: s = ""  
输出: 0

提示：  
$0 <=$ `s.length` $<= 5 * 10^4$  
`s` 由英文字母、数字、符号和空格组成
{{< /notice >}}
#### 思路


#### 代码
<details>
 <summary> Python </summary>

```python
class Solution:
    def lengthOfLongestSubstring(self, s):
        res = left = right = 0
        hashMap = {}
        while right < len(s):
            if s[right] in hashMap:
                res = max(res, right-left)
                left = max(left, hashMap[s[right]])
            hashMap[s[right]] = right+1
            right += 1
        res = max(res, right-left)
        return res

s = "abcabcbb"
# s = "bbbbb"
# s = "pwwkew"
# s = ""
# s = " "
# s = "ab"
# s = "abba"

mat = Solution()
mat.lengthOfLongestSubstring(s)
```
</details>

#### 复杂度
- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$

### 76. 最小覆盖字串

### 438. 找到字符串中所有字母异位词

### 567. 字符串的排列


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

