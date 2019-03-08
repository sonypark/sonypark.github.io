---
layout: post
title: Lv1 - 직사각형 별찍
category: Algorithm Test

tags: [알고리즘, algorithm, python, 파이썬]
comments: true
---
> 출처: https://programmers.co.kr/learn/courses/30/lessons/12934

> 개인적으로 공부한 내용을 정리한 문서이므로 내용 상 오류가 있을 수 있습니다.

## 문제
임의의 정수 n에 대해, n이 어떤 정수 x의 제곱인지 아닌지 판단하려 합니다.
n이 정수 x의 제곱이라면 x+1의 제곱을 리턴하고, n이 정수 x의 제곱이 아니라면 -1을 리턴하는 함수를 완성하세요.


#### 제한사항
- n은 1이상, 50000000000000 이하인 정수입니다.


#### 입출력 예

n | return
:---------:  | :-----------:
121 | 144
3 | -1

## 내 풀이
```python
import math

def next_sqrt(n):
    if math.sqrt(n).is_integer():
        return int((math.sqrt(n)+1))**2
    else:
        return -1
```

## 다른 사람 풀이
```python
def next_sqrt(n):
    sqrt = n ** (1/2)

    if sqrt % 1 == 0:
        return (sqrt + 1) ** 2
    return -1
```

## 배운점
- `math.sqrt().is_integer()`
- math 모듈의 sqrt()를 이용해 제곱근을 구할 수 있다.
- math 모듈의 is_integer() 함수를 통해 정수인지 아닌지 판별할 수 있다.