
2019년 8월 16일

# Codility  - MaxProductOfThree (Sorting) {docsify-ignore-all}

> 출처: https://app.codility.com/programmers/lessons/6-sorting/max_product_of_three/

## 문제

A non-empty array A consisting of N integers is given. The product of triplet (P, Q, R) equates to A[P] * A[Q] * A[R] (0 ≤ P < Q < R < N).

For example, array A such that:

    A[0] = -3
    A[1] = 1
    A[2] = 2
    A[3] = -2
    A[4] = 5
    A[5] = 6

contains the following example triplets:

(0, 1, 2), product is −3 * 1 * 2 = −6
(1, 2, 4), product is 1 * 2 * 5 = 10
(2, 4, 5), product is 2 * 5 * 6 = 60

Your goal is to find the maximal product of any triplet.

Write a function:

`def solution(A):`

that, given a non-empty array A, returns the value of the maximal product of any triplet.

For example, given array A such that:

    A[0] = -3
    A[1] = 1
    A[2] = 2
    A[3] = -2
    A[4] = 5
    A[5] = 6

the function should return 60, as the product of triplet (2, 4, 5) is maximal.

Write an efficient algorithm for the following assumptions:

- N is an integer within the range [3..100,000];
- each element of array A is an integer within the range [−1,000..1,000].


## 내 풀이1 (시간 초과)

> 시간 복잡도 O(N^3)

- 정확도는 100%지만 시간복잡도가 높아 성능 검사를 통과하지 못 한다.

```python
from itertools import combinations
def maxProductOfThree(A):
    c = combinations(A,3)
    MAX_NUM = A[0]*A[1]*A[2]
    for x,y,z in c:
        m = x * y * z
        if m > MAX_NUM: MAX_NUM = m
    return MAX_NUM
```

## 접근 방법

- 배열을 오름차순 정렬한다.

- 이 경우 최댓값이 나올 수 있는 경우의 수는 아래 두 가지중 하나이다.

    1. 가장 큰 세 양수의 곱
    2. 가장 작은 음수 두 개의 곱과 가장 큰 양수의 곱

## 내 풀이2

```python
def maxProductOfThree(A):
    A.sort()
    return max(A[0]*A[1]*A[-1], A[-1]*A[-2]*A[-3])
```
