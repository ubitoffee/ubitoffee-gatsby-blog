---
emoji: ⁉️
title: LeetCode 27. Remove Element
date: '2022-05-08 21:00:00'
author: Ubi
tags: 알고리즘 LeetCode
categories: 알고리즘
---

Site : `LeetCode`
Topic : `Array`
Difficulty : `Easy`


전달받은 배열 nums 에서 val을 제외하고 sorting 시키는 문제


## 풀이

```python
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        nums.sort(key= lambda x : x == val)
        
        return len(list(filter(lambda x : x != val, nums)))
```