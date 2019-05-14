---
layout: post
title: Lv2 - 피보나치 수열 함수 구현(Dynamic programming)
category: Algorithm Tip

tags: [알고리즘, algorithm, python, 파이썬, 피보나치]
comments: true
---
> 출처: https://www.youtube.com/watch?v=vYquumk4nWw&list=PLBZBJbE_rGRU5PrgZ9NBHJwcaZsNpf8yD

> 개인적으로 공부한 내용을 정리한 문서이므로 내용 상 오류가 있을 수 있습니다.

# 피보나치 수열 알고리즘

## 1. Recursion

```python
# 재귀
# 시간복잡도 O(2**n)
def fibo_1(n):
    if n ==1 or n == 2:
        return 1
    else:
        return fibo_1(n-1) + fibo_1(n-2)
```

## Memorized solution 

```python
# memo[] 이용
# 시간복잡 O(2N+1) = O(N)
# But 위에서부터 거꾸로 올라가서 값을 찾기 때문에 bottom_up보다 시간이 오래걸림
# recursion error가 발생함. `maximum recursion depth exceeded in comparison`
def fibo_2(n, memo):
    if memo[n] is not None:
        return memo[n]
    if n == 1 or n == 2:
        return 1
    else:
        memo[n] = fibo_2(n-1, memo) + fibo_2(n-2, memo)
        return memo[n]

def fibo_memo(n):
    memo = [None] * (n + 1)
    return fibo_2(n, memo)
```


## Bottom-up approach

```python
# bottom_up
# 시간복잡도 O(N)
def fibo_3(n):
    if n == 1 or n == 2:
        return 1
    bottom_up = [None] * (n + 1)
    bottom_up[1] = 1
    bottom_up[2] = 1
    for i in range(3, n+1):
        bottom_up[i] = bottom_up[i-1] + bottom_up[i-2]
    return bottom_up[n]
```