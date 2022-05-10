---
emoji: ⁉️
title: LeetCode 66. Plus One
date: '2022-05-11 08:10:00'
author: Ubi
tags: 알고리즘 LeetCode
categories: 알고리즘
---

Site : `LeetCode` [문제 바로가기](https://leetcode.com/problems/plus-one/)  
Topic : `Array` `Math`  
Difficulty : `Easy`  


각 자릿수의 숫자로 이루어진 배열에 1을 더해 올바른 숫자를 리턴하는 문제이다.  
1의자리부터 순차적으로 돌면서 10이 될경우 포인터를 옮겨 가면서 1을 더해주는 방식으로 문제를 해결했다.  

풀고나서 list -> str -> int -> +1 -> list 로 하면 overflow가 날까봐 걱정했었는데 확인해보니 파이썬의 int는 `Arbitary precision`을 도입하여  
유동적인 메모리 사용으로 overflow가 일어나지 않는다고 한다.


## 풀이

```python
class Solution:
    def plusOne(self, digits: List[int]) -> List[int]:
        
        start = len(digits)
        
        while start != 0:
            digits[start - 1] += 1
            
            if digits[start - 1] != 10:
                return digits
            else:
                digits[start - 1] = 0
                start -= 1
                
        if digits[0] == 0:
            digits[0] = 0
            digits.insert(0, 1)
                
        return digits
```