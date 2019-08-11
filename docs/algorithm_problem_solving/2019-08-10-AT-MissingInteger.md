2019년 8월 10일

# Codility  - MissingInteger  (Counting Elements) {docsify-ignore-all}

> 출처: https://app.codility.com/programmers/lessons/4-counting_elements/missing_integer/

## 문제

Write a function:

`def solution(A)`

that, given an array A of N integers, returns the smallest positive integer (greater than 0) that does not occur in A.

For example, given A = [1, 3, 6, 4, 1, 2], the function should return 5.

Given A = [1, 2, 3], the function should return 4.

Given A = [−1, −3], the function should return 1.

Write an efficient algorithm for the following assumptions:

- N is an integer within the range [1..100,000];
- each element of array A is an integer within the range [−1,000,000..1,000,000].

## 접근 방법

- **주어진 배열(A)** 에 들어있는 **원소의 개수**가 **n**이면 무조건 **1~n+1 범위** 안에서 **최소값**이 나온다. (비둘기집 원리)

- 주어진 배열의 길이(n)에서 하나를 더한 **n+1 길이**의 **boolean 배열(m)** 을 만든다.
    - 이 때, 각 요소는 `False`로 채운다.
    - **boolean 배열(m)** 의 길이를 n+1로 해주는 이유는 1~n까지 모두 연속된 숫자가 있을 경우에 n+1이 최솟값이 되기 때문이다.

- for문을 돌며 배열 A를 하나씩 탐색하면서 **1~n 범위**에 있는 숫자라면 **boolean 배열(m)** 의 해당 항목을 `True`로 표시한다. 범위 밖에 있는 숫자들은 최소값에 영향이 없으므로 무시한다.

- for 문을 돌며 **boolean 배열(m)** 을 하나씩 탐색하면서 `False`라고 표시된 값이 나오면 해당 항목을 리턴한다. -- 이게 최솟값이 된다.

## 내 풀이

```python
def missingInteger(A):
    n = len(A)
    m = [False]*(n+1)

    for i in range(n):
        if 1<=A[i]<=n:
            m[A[i]-1] = True
    for j in range(len(m)):
        if m[j] == False:
            return j+1
    return n+1
```

## 배운점

- 비둘기집의 원리에 대해 알게되었다.

## 느낀점

- 풀이 방식도 깔끔하고 재미있는 문제였다.
