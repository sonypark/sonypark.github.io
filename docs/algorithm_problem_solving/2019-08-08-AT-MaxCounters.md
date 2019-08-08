2019년 8월 8일

# Codility  - MaxCounters  (Counting Elements) {docsify-ignore-all}

> 출처: https://app.codility.com/programmers/lessons/4-counting_elements/max_counters/

## 문제

You are given N counters, initially set to 0, and you have two possible operations on them:

- increase(X) − counter X is increased by 1,
- max counter − all counters are set to the maximum value of any counter.

A non-empty array A of M integers is given. This array represents consecutive operations:

- if A[K] = X, such that 1 ≤ X ≤ N, then operation K is increase(X),
- if A[K] = N + 1 then operation K is max counter.

For example, given integer N = 5 and array A such that:

    A[0] = 3
    A[1] = 4
    A[2] = 4
    A[3] = 6
    A[4] = 1
    A[5] = 4
    A[6] = 4

the values of the counters after each consecutive operation will be:

    (0, 0, 1, 0, 0)
    (0, 0, 1, 1, 0)
    (0, 0, 1, 2, 0)
    (2, 2, 2, 2, 2)
    (3, 2, 2, 2, 2)
    (3, 2, 2, 3, 2)
    (3, 2, 2, 4, 2)

The goal is to calculate the value of every counter after all operations.

Write a function:

`def solution(N, A)`

that, given an integer N and a non-empty array A consisting of M integers, returns a sequence of integers representing the values of the counters.

Result array should be returned as an array of integers.

For example, given:

    A[0] = 3
    A[1] = 4
    A[2] = 4
    A[3] = 6
    A[4] = 1
    A[5] = 4
    A[6] = 4

the function should return [3, 2, 2, 4, 2], as explained above.

Write an efficient algorithm for the following assumptions:

- N and M are integers within the range [1..100,000];
- each element of array A is an integer within the range [1..N + 1].

## 접근 방법

- **마지막으로 업데이트 된 값**과 **현재 최대값**을 변수에 저장한다.

## 내 풀이1 (시간 초과)

> 시간 복잡도 O(N*M)

- for 문 안에서 `max` 함수를 쓰고 배열을 새로 만들어주는 과정에서 시간 복잡도가 `O(N*M)`이 되어버렸다.

```python
def maxCounters(N,A):
    answer = [0]*N

    for i in A:
        if i == N+1:
            m = max(answer)
            answer = [m] * N
        else:
            answer[i-1] +=1
    return answer
```

## 내 풀이2

- `last_update` 와 `max_value` 변수를 선언해줌으로써 시간 복잡도를 O(N)으로 줄였다.

    - for 문 안에서 최대값을 계산하고 배열을 새로 만들어주는 과정을 제거

```python
def maxCounters(N, A):
    answer = [0] * N
    last_update = 0
    max_value = 0

    for i in A:
        if i == N + 1:
            last_update = max_value
        else:
            if answer[i-1] < last_update:
                answer[i-1] = last_update

            answer[i-1] += 1

            if answer[i-1] > max_value:
                max_value = answer[i-1]

    for j in range(len(answer)):
        if answer[j] < last_update:
            answer[j] = last_update
    return answer
```

## 느낀점

- 시간 복잡도를 줄이는 과정이 어려우면서도 재미있다.
