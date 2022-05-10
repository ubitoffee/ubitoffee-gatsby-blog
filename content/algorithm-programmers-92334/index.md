---
emoji: ⁉️
title: Programmers 92334. 2022 KAKAO BLIND RECRUITMENT 신고 결과 받기
date: '2022-05-11 01:45:00'
author: Ubi
tags: 알고리즘 Programmers
categories: 알고리즘
---

Site : `Programmers` [문제 바로가기](https://programmers.co.kr/learn/courses/30/lessons/92334?language=python3)  
Topic : `Hash`  
Difficulty : `Easy`  


해시테이블로 신고자와 신고 당한사람을 분리하여 정지기준을 만족하는 지 체크하여 안내 메일 발송 횟수를 리턴하는 문제  


## 풀이

```python
def solution(id_list, report, k):
    answer = []
    
    report_result = {}
    reported_cnt = {}
    
    for entity in set(report):
        spt = entity.split(" ")
        
        reporting = spt[0]
        reported = spt[1]
        
        if reported not in reported_cnt:
            reported_cnt[reported] = 1
        else:
            reported_cnt[reported] += 1
            
        if reporting not in report_result:
            report_result[reporting] = {reported}
        else:
            report_result[reporting].add(reported)
            
        
    for user in id_list:
        cnt = 0
        if user in report_result:
            cnt = len(list(filter(lambda reported: reported_cnt[reported] >= k, report_result[user])))
        
        answer.append(cnt)        
        
    
    return answer
```



아래는 다른사람의 풀이 중 가장 깔끔했던 코드  

answer와 reports를 미리 모든 id를 통해 만든 후 `set`로 report를 돌려서 처리  

미리 answer와 reports의 빈공간의 dict와 list를 만드는데에 메모리를 활용하는데에 id_list가 커질 수 있는 단점이 있지만, 코드가 너무 깔끔..  

내 문제 풀이에서도 신고자와 신고 당한사람을 dict로 별도로 관리했으니 메모리 측면에서는 크게 좋은 것 같지는 않다..  



```python
def solution(id_list, report, k):
    answer = [0] * len(id_list)    
    reports = {x : 0 for x in id_list}

    for r in set(report):
        reports[r.split()[1]] += 1

    for r in set(report):
        if reports[r.split()[1]] >= k:
            answer[id_list.index(r.split()[0])] += 1

    return answer
```