2019년 8월 6일

# Codility  -  TapeEquilibrium (Time Complexity) {docsify-ignore-all}

> 출처: https://app.codility.com/programmers/lessons/3-time_complexity/tape_equilibrium/

## 문제

A non-empty array A consisting of N integers is given. Array A represents numbers on a tape.

Any integer P, such that 0 < P < N, splits this tape into two non-empty parts: A[0], A[1], ..., A[P − 1] and A[P], A[P + 1], ..., A[N − 1].

The difference between the two parts is the value of: |(A[0] + A[1] + ... + A[P − 1]) − (A[P] + A[P + 1] + ... + A[N − 1])|

In other words, it is the absolute difference between the sum of the first part and the sum of the second part.

For example, consider array A such that:

  A[0] = 3
  A[1] = 1
  A[2] = 2
  A[3] = 4
  A[4] = 3
We can split this tape in four places:

- P = 1, difference = |3 − 10| = 7 
- P = 2, difference = |4 − 9| = 5 
- P = 3, difference = |6 − 7| = 1 
- P = 4, difference = |10 − 3| = 7 

Write a function:

`def solution(A)`

that, given a non-empty array A of N integers, returns the minimal difference that can be achieved.

For example, given:

  A[0] = 3
  A[1] = 1
  A[2] = 2
  A[3] = 4
  A[4] = 3
the function should return 1, as explained above.

Write an efficient algorithm for the following assumptions:

- N is an integer within the range [2..100,000];
- each element of array A is an integer within the range [−1,000..1,000].


## 내 풀이1 (시간 초과)

- 시간 복잡도 `O(N^2)`
- **sum**은 `O(N)`의 시간복잡도를 갖는다.
- for 문 안에 **sum**이 있으니 시간 복잡도가 `O(N^2)` 이 되어 시간 초과가 난다.
- **list slicing**도 `O(K)`의 시간복잡도를 갖는다. (K는 slicing 하는 element의 인덱스)

```python
def tapeEquilibrium(A):
    m = 2000
    for i in range(len(A)-1):
        a = abs(sum(A[:i+1]) - sum(A[i+1:]))
        if (m >= a): m = a
    return m
```

## 내 풀이2

- for 문 안에서 **sum** 함수와 **list slicing**을 쓰지 않았다.
- for 문 안에서 모든 계산을 처리하므로 시간 복잡도는 `O(N)` 이다.

```python
def tapeEquilibrium(A):
    s = sum(A)
    m = 2000
    l_sum = 0
    for i in A[:-1]:
        l_sum += i
        a = abs((l_sum)*2 - s)
        if (m >= a): m = a
    return m
```

## 느낀점

- 문제 자체는 어렵지 않았는데, 시간 복잡도를 줄이는 과정에서 시간을 많이 썼다.

- 그 동안 파이썬 내장 함수인 `sum`과 내장 기능인 `list slicing`을 아무 생각 없이 쓰고 있었는데, 이 문제를 통해 해당 기능이 갖는 시간복잡도에 대해서 생각해보게 되었다.

