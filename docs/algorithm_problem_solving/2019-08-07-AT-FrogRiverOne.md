2019년 8월 7일

# Codility  -  FrogRiverOne (Time Complexity) {docsify-ignore-all}

> 출처: https://app.codility.com/programmers/lessons/4-counting_elements/frog_river_one/

## 문제

A small frog wants to get to the other side of a river. The frog is initially located on one bank of the river (position 0) and wants to get to the opposite bank (position X+1). Leaves fall from a tree onto the surface of the river.

You are given an array A consisting of N integers representing the falling leaves. A[K] represents the position where one leaf falls at time K, measured in seconds.

The goal is to find the earliest time when the frog can jump to the other side of the river. The frog can cross only when leaves appear at every position across the river from 1 to X (that is, we want to find the earliest moment when all the positions from 1 to X are covered by leaves). You may assume that the speed of the current in the river is negligibly small, i.e. the leaves do not change their positions once they fall in the river.

For example, you are given integer X = 5 and array A such that:

```
  A[0] = 1
  A[1] = 3
  A[2] = 1
  A[3] = 4
  A[4] = 2
  A[5] = 3
  A[6] = 5
  A[7] = 4
```

In second 6, a leaf falls into position 5. This is the earliest time when leaves appear in every position across the river.

Write a function:

`def solution(X, A)`

that, given a non-empty array A consisting of N integers and integer X, returns the earliest time when the frog can jump to the other side of the river.

If the frog is never able to jump to the other side of the river, the function should return −1.

For example, given X = 5 and array A such that:

```
  A[0] = 1
  A[1] = 3
  A[2] = 1
  A[3] = 4
  A[4] = 2
  A[5] = 3
  A[6] = 5
  A[7] = 4
```

the function should return 6, as explained above.

Write an efficient algorithm for the following assumptions:

- N and X are integers within the range [1..100,000];
- each element of array A is an integer within the range [1..X].

## 접근 방법

- 목표 지점을 n이라 할 때, 목표 지점에 도달하기 위해서는 1부터 n 까지 연속된 수가 나와야한다.

- 연속된 수가 빠짐없이 나오는 가장 빠른 시점을 찾아야 한다.

1. 도달해야 할 목표 지점의 위치를 `uncovered_position`으로 놓는다.

2. `covered_time`이라는 배열을 만든다.
    - 이 배열의 **index**에는 covered 된 **위치**가 담기고, **value** 에는 해당 position이 covered 된 **시간**이 담긴다.

    - for 문을 돌며 배열 A에 주어진 위치(position)를 `covered_time` 배열에 담는다.
    
    - 값을 담을 때마다 `uncovered_position`의 값을 `-1` 해준다.
    
    - `uncovered_position`이 `0`이 되면 목표 지점까지 가는 경로가 모두 채워졌다는 뜻이므로, `uncovered_position`이 `0`이 되는 시점의 **시간(time)** 을 출력한다.

3. 위 과정을 모두 마치고도 `uncovered_position`이 `0`이 되지 않으면 목표 지점에 도달 할 수 없는 경우이므로 `-1`을 리턴한다.


## 내 풀이

- 테스트 케이스 몇 개를 계속 통과 못 해서 결국 아래 풀이를 보고 풀었다.

> https://codesays.com/2014/solution-to-frog-river-one-by-codility/

```python
def frogRiverOne(X,A):
    coverd_time = [-1]*(X+1)
    uncovered_position = X
    for i in range(len(A)):
        if coverd_time[A[i]] != -1: continue
        else:
            coverd_time[A[i]] = i
            uncovered_position -=1
            if uncovered_position ==0: return i
    return -1
```

