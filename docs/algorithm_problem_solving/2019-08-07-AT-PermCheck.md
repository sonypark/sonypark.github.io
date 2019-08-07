2019년 8월 7일

# Codility  -  PermCheck (Time Complexity) {docsify-ignore-all}

> 출처: https://app.codility.com/programmers/lessons/4-counting_elements/perm_check/

## 문제

A non-empty array A consisting of N integers is given.

A permutation is a sequence containing each element from 1 to N once, and only once.

For example, array A such that:

    A[0] = 4
    A[1] = 1
    A[2] = 3
    A[3] = 2
is a permutation, but array A such that:

    A[0] = 4
    A[1] = 1
    A[2] = 3
is not a permutation, because value 2 is missing.

The goal is to check whether array A is a permutation.

Write a function:

def solution(A)

that, given an array A, returns 1 if array A is a permutation and 0 if it is not.

For example, given array A such that:

    A[0] = 4
    A[1] = 1
    A[2] = 3
    A[3] = 2
the function should return 1.

Given array A such that:

    A[0] = 4
    A[1] = 1
    A[2] = 3
the function should return 0.

Write an efficient algorithm for the following assumptions:

- N is an integer within the range [1..100,000];
- each element of array A is an integer within the range [1..1,000,000,000].

## 접근 방법

- 처음에는 예시 처럼 배열에 1부터 N까지 연속된 숫자가 담겨 있고 그 중 하나만 비어있는 배열을 생각하고 풀었는데 틀렸다.

- 틀린 후에 `[1,4,1]` 이런 식으로도 주어질 수 있다는 걸 알고 Counter 함수를 써서 중복된 숫자가 있는지 체크해주었다.


## 내 풀이

```python
from collections import Counter

def permCheck(A):
    n = len(A)
    ss = n*(n+1)/2
    s = sum(A)
    if ss == s:
        c = Counter(A).most_common()
        if c[0][1] >=2: return 0
        return 1
    else: return 0
```

## 느낀점

- 순열인지 아닌지 판별하는 문제에서 연속된 숫자의 합을 구하는 공식이 유용하다.
