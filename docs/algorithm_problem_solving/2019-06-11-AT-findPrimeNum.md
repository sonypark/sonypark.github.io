2019년 6월 11일

# Lv2 - 소수 찾기 (sort) {docsify-ignore-all}

> 출처: https://programmers.co.kr/learn/courses/30/lessons/42839

## 문제

한자리 숫자가 적힌 종이 조각이 흩어져있습니다. 흩어진 종이 조각을 붙여 소수를 몇 개 만들 수 있는지 알아내려 합니다.

각 종이 조각에 적힌 숫자가 적힌 문자열 numbers가 주어졌을 때, 종이 조각으로 만들 수 있는 소수가 몇 개인지 return 하도록 solution 함수를 완성해주세요.

#### 제한 사항

- numbers는 길이 1 이상 7 이하인 문자열입니다.
- numbers는 0~9까지 숫자만으로 이루어져 있습니다.
- 013은 0, 1, 3 숫자가 적힌 종이 조각이 흩어져있다는 의미입니다

#### 입출력 예

numbers | return
----|----
"17" | 3
"011" | 2

## 접근 방법

1. 소수 판별 함수를 만든다.

2. for 문을 돌며 가능한 순열의 수를 구한다.

3. `set`을 이용해 중복된 수를 제거한다.

4. 소수 판별 함수를 이용해 소수를 카운트한다.

## 내 풀이

```python
import itertools

def primNumber(n):
    if n < 2: return False
    if n == 2: return True
    if n % 2 == 0: return False

    m = int(n**0.5)+1

    for i in range(3,m,2):
        if n % i == 0:
            return False
    return True

def findPrimeNum(numbers):
    count = 0
    a = set()
    for k in range(len(numbers)):
        n = list(itertools.permutations(numbers, k+1))

        for i in n:
            s = ''.join(i)
            a.add(int(s))

    for j in a:
        if primNumber(j):
            count += 1
    return count
```

## 다른 사람 풀이 : 에라토스테네스의 체

- 이중 포문 제거

- 소수 판별 함수가 더 간단하다.

```python
from itertools import permutations

def solution(numbers):
    answer = 0
    candidates, num_set = [], set()
    digits = [digit for digit in numbers]

    for i in range(1, len(numbers)+1):
        candidates += [*list(permutations(digits, i))]

    for candidate in candidates:
        num_set.add(int(''.join(map(str, candidate))))

    for num in num_set:
        if is_prime(num):
            answer += 1

    return answer

def is_prime(number):
    if number == 0 or number == 1:
        return False

    for i in range(2, number//2 + 1):
        if (number/i) == (number//i):
            return False

    return True
```

## 배운점

- 기존에 알던 것보다 더 간단한 소수 판별 함수를 알게 되었다.
