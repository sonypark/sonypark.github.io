---
layout: post
title: Lv2 - 피보나치 수
category: Algorithm Test

tags: [알고리즘, algorithm, python, 파이썬, 피보나치]
comments: true
---
> 출처: https://programmers.co.kr/learn/courses/30/lessons/12945

> 개인적으로 공부한 내용을 정리한 문서이므로 내용 상 오류가 있을 수 있습니다.

## 문제
피보나치 수는 F(0) = 0, F(1) = 1일 때, 1 이상의 n에 대하여 F(n) = F(n-1) + F(n-2) 가 적용되는 수 입니다.

예를들어

F(2) = F(0) + F(1) = 0 + 1 = 1
F(3) = F(1) + F(2) = 1 + 1 = 2
F(4) = F(2) + F(3) = 1 + 2 = 3
F(5) = F(3) + F(4) = 2 + 3 = 5
와 같이 이어집니다.

2 이상의 n이 입력되었을 때, n번째 피보나치 수를 1234567으로 나눈 나머지를 리턴하는 함수, solution을 완성해 주세요.


#### 제한사항
- * n은 1이상, 100000이하인 자연수입니다.


#### 입출력 예

n | return
:---------:  | :-----------:
3 | 2
5 | 5

## 내 풀이
```python
# 런타임 에러. 1000이상이면 recursion error가 발생한다. 문제는 10만까지 입력값으로 들어온다.
memo = {}
def fibo(n):
    memo[1] = 1
    memo[2] = 1
    if n not in memo:
        memo[n] = fibo(n-1) + fibo(n-2)
    return memo[n]

# botton_up 방식 (아래서부터 차례대로 계산)
def fibo2(n):
    a, b = 1, 0
    for i in range(n):
        a, b = b, a+b
    return b

def solution(n):
    return fibo2(n) % 1234567
```


## 배운점
- 피보나치 수를 구하는 알고리즘에 대해 좀 더 자세히 알게되었다.
- 피보나치 수에 대한 알고리즘은 크게 세 가지로 나뉜다.
- 이곳에 설명이 잘 되어있다. [출처](https://www.youtube.com/watch?v=vYquumk4nWw&list=PLBZBJbE_rGRU5PrgZ9NBHJwcaZsNpf8yD) 


## 느낀점
- 알고리즘을 공부하는 이유는 보다 효율적인 방식을 찾기 위함이다.
- 피보나치 수열은 재귀함수와 다이나믹 프로그래밍(DP)를 공부하기 좋은 예제이다.
