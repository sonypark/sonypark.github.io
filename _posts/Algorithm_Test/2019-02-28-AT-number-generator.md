---
layout: post
title: Lv1 - x만큼 간격이 있는 n개의 숫자
category: Algorithm Test

tags: [알고리즘, algorithm, python, 파이썬]
comments: true
---
> 출처: https://programmers.co.kr/learn/courses/30/lessons/12954

## 문제
함수 solution은 정수 x와 자연수 n을 입력 받아, x부터 시작해 x씩 증가하는 숫자를 n개 지니는 리스트를 리턴해야 합니다.
다음 제한 조건을 보고, 조건을 만족하는 함수, solution을 완성해주세요.


#### 제한사항
- x는 -10000000 이상, 10000000 이하인 정수입니다.
- n은 1000 이하인 자연수입니다.

#### 입출력 예

x | n | return
--- |---  |----
2 | 5  | [2,4,6,8,10]
4 | 3   | [4,8,12]
-4 | 2   | [-4,-8]

## 내 풀이
```python
def number_generator(x,n):
    ll = []

    if x == 0:
        for i in range(n):
            ll.append(x)

    if x > 0:
        for i in range(x, x*n+1, x):
            ll.append(i)

    elif x < 0:
        for i in range(x, x*n-1, x):
            ll.append(i)

    return ll
```

## 다른 사람 풀이
```python
def number_generator(x, n):
    return [i * x + x for i in range(n)]
```
