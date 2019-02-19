---
layout: post
title: Lv1 - 두 정수 사이의 합
category: Algorithm Test

tags: [알고리즘, algorithm, python, 파이썬]
comments: true
---
> 출처: https://programmers.co.kr/learn/courses/30/lessons/12912

## 문제
두 정수 a, b가 주어졌을 때 a와 b 사이에 속한 모든 정수의 합을 리턴하는 함수, solution을 완성하세요. 
예를 들어 a = 3, b = 5인 경우, 3 + 4 + 5 = 12이므로 12를 리턴합니다.


#### 제한사항
- n은 길이 10,000이하인 자연수입니다.

#### 입출력 예
- a와 b가 같은 경우는 둘 중 아무 수나 리턴하세요.
- a와 b는 -10,000,000 이상 10,000,000 이하인 정수입니다.
- a와 b의 대소관계는 정해져있지 않습니다.


## 내 풀이
```python

def sum_numbers(a,b):
    x,y = min(a,b), max(a,b)

    if (x == y):
        return a

    return sum(range(x,y+1))
```

## 다른 사람의 풀이
```python
def adder(a,b):
    return sum(range(min(a, b), max(a, b) + 1))

```

## 배운점
- 불필요한 변수 제거
- 이 코드가 반드시 필요한지, 다른 것을 대체 될 수 있는지 생각하자


## 느낀점
- 반드시 필요한 코드만 남기자