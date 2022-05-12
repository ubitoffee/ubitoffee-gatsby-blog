---
emoji: ⁉️
title: LeetCode 70. Climbing Stairs (다시 풀 것..)
date: '2022-05-12 14:58:00'
author: Ubi
tags: 알고리즘 LeetCode
categories: 알고리즘
---

Site : `LeetCode` [문제 바로가기](https://leetcode.com/problems/climbing-stairs/)  
Topic : `Math` `Dynamic Programming` `Memoization`  
Difficulty : `Easy`  


아직 알고리즘 문제에 익숙해지지 않았는지

- 메모이제이션 과정을 거쳐야 한다는 점
- 메모이제이션할 때 배열이 필요 없이 한다는 점

을 전혀 인지 하지 못했다..  

풀고나니 피보나치인 점도 왜 알고리즘을 꾸준히 풀어야 하는지에 대해 다시 한번 깨닫게 되었다..  

```
p.s. 제약조건부터 45개 제한인거 보고도 알아 차릴수 있었을텐데..
```


## 풀이

```python
class Solution(object):
    def climbStairs(self, n):
        step = [0] * n
        
        for i in range(0, n):
            if i == 0:
                step[i] = 1
            elif i == 1:
                step[i] = 2
            else:
                step[i] = step[i - 2] + step[i - 1]
                
        return step[i]
```
