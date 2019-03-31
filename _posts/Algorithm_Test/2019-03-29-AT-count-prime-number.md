---
layout: post
title: Lv2 - 소수 만들기
category: Algorithm Test

tags: [알고리즘, algorithm, python, 파이썬, 피보나치]
comments: true
---
> 출처: https://programmers.co.kr/learn/courses/30/lessons/12977

> 개인적으로 공부한 내용을 정리한 문서이므로 내용 상 오류가 있을 수 있습니다.


## 문제
주어진 숫자 중 3개의 수를 더했을 때 소수가 되는 경우의 개수를 구하려고 합니다. 숫자들이 들어있는 배열 nums가 매개변수로 주어질 때, nums에 있는 숫자들 중 서로 다른 3개를 골라 더했을 때 소수가 되는 경우의 개수를 return 하도록 solution 함수를 완성해주세요.

#### 제한사항
- nums에 들어있는 숫자의 개수는 3개 이상 50개 이하입니다.
- nums의 각 원소는 1 이상 1000 이하의 자연수이며, 중복된 숫자가 들어있지 않습니다.

#### 입출력 예

s | return
:---------:  | :-----------:
[1,2,3,4]	| 1
[1,2,7,6,4]	| 4


## 내 풀이
```python
import math
from itertools import combinations

# 소수 판별 함수
def isPrimeNum(n):

    if n == 2:
        return True

    if n % 2 == 0:
        return False

    sqrt_n = math.floor(math.sqrt(n)) + 1

    for j in range(3, sqrt_n, 2):
        if n % j == 0:
            return False

    return True


# 서로 다른 숫자 세 개의 합이 소수인 갯수를 구하는 함수
def countPrimeNumber(nums):
    sum_list = list(map(sum, combinations(nums, 3)))
    print(sum_list)

    answer = 0

    for n in sum_list:
        if isPrimeNum(n):
            answer += 1

    return answer
```

## 배운점
- 조합(combination)을 구하는 방법
- `itertools.combinations`
- Syntax : `itertools.combinations(iterable, r)`
- Return r length subsequences of elements from the input iterable.
- 원소의 갯수가 r인 조합을 리턴한다.

```python
combinations('ABCD', 2) --> AB AC AD BC BD CD
combinations(range(4), 3) --> 012 013 023 123
```

- cf. 순열을 구하는 구하는 방법 
- `itertools.permutation`
