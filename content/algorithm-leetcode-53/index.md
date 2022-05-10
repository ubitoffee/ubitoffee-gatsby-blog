---
emoji: ⁉️
title: LeetCode 53. Maximum Subarray
date: '2022-05-10 21:42:00'
author: Ubi
tags: 알고리즘 LeetCode
categories: 알고리즘
---

Site : `LeetCode` [문제 바로가기](https://leetcode.com/problems/maximum-subarray/)  
Topic : `Array` `Divide and Conquer` `Dynamic Programming`
Difficulty : `Easy`  


전달받은 nums의 연결된 subarray 집합에서 가장 큰 합을 구하는 문제  

TODO - Divide and Conquer로 문제 풀어보기


## 풀이 - Dynamic Programming

배열을 순차적으로 돌면서 가장 큰 합이 나올 때 maxSum 변수에 기록한다.  

현재 합이 0보다 작아질 때 앞에 계산된 값들은 의미가 없어지니 0으로 초기화하여 다시 계산을 진행한다.  

```python
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        maxSum = float("-inf")
        curSum = 0
        
        for i in nums:
            curSum += i
            
            if curSum > maxSum:
                maxSum = curSum
            
            if curSum < 0:
                curSum = 0
            
        return maxSum
```
