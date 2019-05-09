---
layout: post
title: 소인수분해 
category: Algorithm Tip

tags: [알고리즘, algorithm, python, 파이썬]
comments: true
---

> 출처: https://www.acmicpc.net/problem/status/11653

## 정의
합성수를 소수의 곱으로 나타내는 방법을 말한다.

### 다양한 풀이법

## Method #1

```python
def getprime(n):
    for x in range(2, n + 1):
        count = 0    # 인수가 곱해진 횟수
        while n % x == 0:
            count += 1
            n /= x
        if count != 0:
            for i in range(count):
                print ("%d" % x)
# getprime(n)
```

## Method #2

```python
for i in range(2, int(n**0.5)+1):
    while n % i == 0:
        n = n // i
        print(i)
if n > 1:
    print(n)
```