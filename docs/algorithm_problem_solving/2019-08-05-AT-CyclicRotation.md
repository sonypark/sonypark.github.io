2019년 8월 5일

# Codility  - CyclicRotation (Array) {docsify-ignore-all}

> 출처: https://app.codility.com/programmers/lessons/2-arrays/cyclic_rotation/

## 문제

An array A consisting of N integers is given. Rotation of the array means that each element is shifted right by one index, and the last element of the array is moved to the first place. For example, the rotation of array A = [3, 8, 9, 7, 6] is [6, 3, 8, 9, 7] (elements are shifted right by one index and 6 is moved to the first place).

The goal is to rotate array A K times; that is, each element of A will be shifted to the right K times.

Write a function:

`def solution(A,K)`

that, given an array A consisting of N integers and an integer K, returns the array A rotated K times.

For example, given

    A = [3, 8, 9, 7, 6]
    K = 3
the function should return [9, 7, 6, 3, 8]. Three rotations were made:

    [3, 8, 9, 7, 6] -> [6, 3, 8, 9, 7]
    [6, 3, 8, 9, 7] -> [7, 6, 3, 8, 9]
    [7, 6, 3, 8, 9] -> [9, 7, 6, 3, 8]
For another example, given

    A = [0, 0, 0]
    K = 1
the function should return [0, 0, 0]

Given

    A = [1, 2, 3, 4]
    K = 4
the function should return [1, 2, 3, 4]

Assume that:

- N and K are integers within the range [0..100];
- each element of array A is an integer within the range [−1,000..1,000].

In your solution, focus on correctness. The performance of your solution will not be the focus of the assessment.

### 접근 방법

- 입력받은 숫자만큼 무작정 이동하는 건 매우 비효율적이다.

- 배열의 길이는 정해져 있으므로 배열의 길이로 나누었을 때 나머지만큼만 이동하면 된다.

- 빈 배열이거나 이동하는 길이가 배열의 길이와 같은 경우에는 배열을 그대로 리턴한다.

## 내 풀이

```python
def CyclicRotation(A,K):
    length = len(A)
    answer = [0] * length
    if K == length or length ==0: return A
    d = K % length
    for i in range(length):
        answer[(i+d) % length] = A[i]
    return answer
```
