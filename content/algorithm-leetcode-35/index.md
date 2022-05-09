---
emoji: ⁉️
title: LeetCode 35. Search Insert Position
date: '2022-05-09 14:30:00'
author: Ubi
tags: 알고리즘 LeetCode
categories: 알고리즘
---

Site : `LeetCode` [문제 바로가기](https://leetcode.com/problems/search-insert-position/)  
Topic : `Array` `Binary Search`  
Difficulty : `Easy`  


시간복잡도 `O(log n)`로 `target`을 어느 인덱스에 추가해야 하는 지를 찾는 문제. 

Binary Search 구현을 다시한번 복습하는 계기가 되었다.


## 풀이

```python
class Solution:
    def searchInsert(self, nums: List[int], target: int) -> int:
        low = 0
        mid = 0
        high = len(nums) - 1
        
        while low <= high:
            mid = low + (high - low) // 2
            
            if nums[mid] < target:
               low = mid + 1
            elif nums[mid] > target:
                high = mid - 1
            else:
                return mid
            
        if nums[mid] < target:
            return mid + 1
        else:
            return mid
```
