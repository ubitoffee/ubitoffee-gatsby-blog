---
emoji: ⁉️
title: LeetCode 67. Add Binary
date: '2022-05-11 14:10:00'
author: Ubi
tags: 알고리즘 LeetCode
categories: 알고리즘
---

Site : `LeetCode` [문제 바로가기](https://leetcode.com/problems/add-binary/)  
Topic : `Math` `String` `Bit Manipulation`  
Difficulty : `Easy`  


진짜 이진법 처리방식을 구현하는 문제로 문자열로 a와 b를 합친 후 2,3 처럼 몫이 남아있을 경우 위의 자리로 값을 올려주는 부분을 실제로 구현했다.  
더 나은 방법들이 있을지 풀어보자  


## 풀이

```python
class Solution:
    def addBinary(self, a: str, b: str) -> str:
        added = list(str(int(a) + int(b)))
        
        for i in range(len(added) -1, -1, -1):
            e = added[i]
            if i != 0:
                if e == "2":
                    added[i] = "0"
                    added[i - 1] =  str(int(added[i - 1]) + 1)
                elif e == "3":
                    added[i] = "1"
                    added [i - 1] = str(int(added[i - 1]) + 1)
            else:
                if e == "2":
                    added[i] = "10"
                elif e == "3":
                    added[i] = "11"

        return "".join(added)
```
