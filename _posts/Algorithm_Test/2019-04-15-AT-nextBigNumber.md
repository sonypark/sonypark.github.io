---
layout: post
title: Lv2_다음 큰 숫자
category: Algorithm Test

tags: [알고리즘, algorithm, python, 파이썬, 이진수]
comments: true
---
> 출처: https://programmers.co.kr/learn/courses/30/lessons/12911

> 개인적으로 공부한 내용을 정리한 문서이므로 내용 상 오류가 있을 수 있습니다.
> 잘못된 내용이 있을 경우 댓글로 남겨주시면 감사하겠습니다.

## 문제
자연수 n이 주어졌을 때, n의 다음 큰 숫자는 다음과 같이 정의 합니다.

- 조건 1. n의 다음 큰 숫자는 n보다 큰 자연수 입니다.
- 조건 2. n의 다음 큰 숫자와 n은 2진수로 변환했을 때 1의 갯수가 같습니다.
- 조건 3. n의 다음 큰 숫자는 조건 1, 2를 만족하는 수 중 가장 작은 수 입니다.

예를 들어서 78(1001110)의 다음 큰 숫자는 83(1010011)입니다.

자연수 n이 매개변수로 주어질 때, n의 다음 큰 숫자를 return 하는 solution 함수를 완성해주세요.


#### 제한사항
- n은 1,000,000 이하의 자연수 입니다.


#### 입출력 예

n | result
:---------:  | :-----------:
78	| 83
15	| 23


## 내 풀이
```python
import collections

def solution(n):
    nn = n
    remainder = []
    while n != 0:
        remainder.append(n % 2)
        n = n // 2
    a = collections.Counter(remainder)

    for i in range(nn+1, nn*2):
        remainder_i = []
        ii = i
        while i != 0:
            remainder_i.append(i % 2)
            i = i // 2

        b = collections.Counter(remainder_i)
        if(a[1] == b[1]):
            return ii
```

## 다른 사람 풀이

```python
def nextBigNumber(n):
    c = bin(n).count('1')
    for m in range(n+1, n*2):
        if bin(m).count('1') == c:
            return m
```


## 배운점

- 10진수를 다른 진수로 변환하려면
- 10진수를 변환하고자 하는 진수로 몫이 0이 될때까지 계속해서 나누고
- 나머지를 역순으로 나열한 값이 변환한 값이 된다.

### 파이썬 진수 변환

```python
num = 12345

bin(num)  # 10진수 -> 2진수 변환 : 0b11000000111001

oct(num)  # 10진수 -> 8진수 변환 : 030071

hex(num)  # 10진수 -> 16진수 변환 : 0x3039

int(bin(num),2)   # 2진수 -> 10진수 변환 : 12345

int(hex(num),16)  # 16진수 -> 10진수 변환 : 12345
```