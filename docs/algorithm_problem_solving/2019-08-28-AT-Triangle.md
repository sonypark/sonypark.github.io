
2019년 8월 28일

# Codility  - Triangles (Sorting) {docsify-ignore-all}

> 출처: https://app.codility.com/programmers/lessons/6-sorting/triangle/

## 문제

An array A consisting of N integers is given. A triplet (P, Q, R) is triangular if 0 ≤ P < Q < R < N and:

- A[P] + A[Q] > A[R],
- A[Q] + A[R] > A[P],
- A[R] + A[P] > A[Q].

For example, consider array A such that:

      A[0] = 10    A[1] = 2    A[2] = 5
      A[3] = 1     A[4] = 8    A[5] = 20
Triplet (0, 2, 4) is triangular.

Write a function:

`def solution(A)`

that, given an array A consisting of N integers, returns 1 if there exists a triangular triplet for this array and returns 0 otherwise.

For example, given array A such that:

    A[0] = 10    A[1] = 2    A[2] = 5
    A[3] = 1     A[4] = 8    A[5] = 20
the function should return 1, as explained above. Given array A such that:

    A[0] = 10    A[1] = 50    A[2] = 5
    A[3] = 1

the function should return 0.

Write an efficient algorithm for the following assumptions:

- N is an integer within the range [0..100,000];
- each element of array A is an integer within the range [−2,147,483,648..2,147,483,647].

## 접근 방법

- 삼각형 성립 조건

- 세 숫자의 크기가 a,b,c (a < b < c )라고 할 때, 아래 세 조건을 만족해야 한다.

     1. a + b > c
     2. b + c > a
     3. c + a > b

- 주어진 배열 A를 정렬하면 `A[i] < A[i+1] < A[i+2]` 가 성립한다.

- 따라서 삼각형 성립 조건 중 2,3번은 항상 만족하므로 1번 조건만 체크하면 된다.

- `A[i] +A[i+1] > A[i+2]` 인 경우가 있는지만 체크 하고 있으면 `1`을 리턴하고 없으면 `0`을 리턴한다.

## 내 풀이

```python
def Triangle(A):

    if len(A) <3: return 0

    A.sort()
    for i in range(0, len(A)-2):
        if A[i] +A[i+1] > A[i+2]:
            return 1
    else: return 0
```
