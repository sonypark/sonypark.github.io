2019년 8월 11일

# Codility  - PassingCars  (Counting Elements) {docsify-ignore-all}

> 출처: https://app.codility.com/programmers/lessons/4-counting_elements/missing_integer/

## 문제

A non-empty array A consisting of N integers is given. The consecutive elements of array A represent consecutive cars on a road.

Array A contains only 0s and/or 1s:

- 0 represents a car traveling east,
- 1 represents a car traveling west.

The goal is to count passing cars. We say that a pair of cars (P, Q), where 0 ≤ P < Q < N, is passing when P is traveling to the east and Q is traveling to the west.

For example, consider array A such that:

    A[0] = 0
    A[1] = 1
    A[2] = 0
    A[3] = 1
    A[4] = 1

We have five pairs of passing cars: (0, 1), (0, 3), (0, 4), (2, 3), (2, 4).

Write a function:

`def solution(A)`

that, given a non-empty array A of N integers, returns the number of pairs of passing cars.

The function should return −1 if the number of pairs of passing cars exceeds 1,000,000,000.

For example, given:

    A[0] = 0
    A[1] = 1
    A[2] = 0
    A[3] = 1
    A[4] = 1

the function should return 5, as explained above.

Write an efficient algorithm for the following assumptions:

- N is an integer within the range [1..100,000];
- each element of array A is an integer that can have one of the following values: 0, 1.

## 접근 방법

- **pair가 될 수 있는 최대 갯수**는 배열 내 **1을 모두 합한 값**이다.

- 그렇다면 **1을 모두 합한 값(s)** 을 **기준**으로 for문을 돌면서
    - `1`을 만나면 `s-1`을 해주고
    - `0`을 만나면 `s`를 pair 갯수에 더해주면 된다.

## 내 풀이

```python
def passingCars(A):
    s = sum(A)
    pair = 0
    for i in range(len(A)):
        if A[i] ==1:
            s -=1
        if A[i] ==0:
           pair += s
        if pair > 1000000000: return -1
    return pair
```

## 느낀점

- for문 안에서 **sum** 함수, **list slicing** 을 쓰면 시간 복잡도가 `n^2`이 나오는 것을 인식하게 되었다.

- 예전에 비슷하게 시간복잡도를 해결했던 경험이 있어서 이번 문제는 쉽게 해결했다.

- 시간 복잡도를 줄이는 방법을 조금씩 배워가고 있다.
