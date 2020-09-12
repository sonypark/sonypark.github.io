
2019년 11월 12일

# Udemy - Rotating 2D Array (2D Array) {docsify-ignore-all}

> 출처: https://www.udemy.com/course/11-essential-coding-interview-questions/learn/quiz/383880#overview

## 문제

A 2-dimensional array is an array of arrays.

Implement a function that takes a **square** 2D array (# columns = # rows) and rotates it by 90 degrees.

### Example 1

Given field:

```
[
 [1, 2, 3],
 [4, 5, 6],
 [7, 8, 9],
]
```

Resulting field:

```
[
 [7, 4, 2],
 [8, 5, 2],
 [9, 6, 3],
]
```

When you are done, try implementing this function so that you can solve this problem **in place**. Solving it means that your function won't create a new array to solve this problem.  Instead, modify the content of the given array with O(1) extra space.

## 접근 방법

- 주어진 배열을 그대로 copy 하여 새로운 배열을 만든다.

- 

## 내 풀이

```python
import copy

def rotate(given_array, n):
    rotated = copy.deepcopy(given_array)
    for i in range(n):
        for j in range(n):
            rotated[i][j] = given_array[n-j-1][i]

    return rotated
```
