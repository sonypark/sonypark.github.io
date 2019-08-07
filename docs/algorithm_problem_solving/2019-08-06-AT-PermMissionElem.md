2019년 8월 6일

# Codility  -  PermMissionElem (Time Complexity) {docsify-ignore-all}

> 출처: https://app.codility.com/programmers/lessons/3-time_complexity/perm_missing_elem/

## 문제

An array A consisting of N different integers is given. The array contains integers in the range [1..(N + 1)], which means that exactly one element is missing.

Your goal is to find that missing element.

Write a function:

`def solution(A)`

that, given an array A, returns the value of the missing element.

For example, given array A such that:

  A[0] = 2
  A[1] = 3
  A[2] = 1
  A[3] = 5
the function should return 4, as it is the missing element.

Write an efficient algorithm for the following assumptions:

- N is an integer within the range [0..100,000];
- the elements of A are all distinct;
- each element of array A is an integer within the range [1..(N + 1)].

## 접근 방법

- 이 문제는 연속된 숫자의 합을 이용해서 푸는 문제였다.

- 1부터 n까지의 연속된 합을 구하는 공식을 알면 쉽게 풀 수 있다.

```
1+2+3+ . . . + N = N*(N+1) / 2
```

## 내 풀이

```python
def permMissingElem(A):
    n = len(A)
    s = (n+1)*(n+2) / 2
    return int(s - sum(A))
```
