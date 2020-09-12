
2019년 11월 10일

# Udemy - Assign Numbers in Minesweeper (2D Array) {docsify-ignore-all}

> 출처: https://www.udemy.com/course/11-essential-coding-interview-questions/learn/quiz/379168#overview

## 문제

Implement a function that assigns correct numbers in a field of Minesweeper, which is represented as a 2 dimensional array.

### Example

- The size of the field is 3x4, and there are bombs at the positions [0, 0] (row index = 0, column index = 0) and [0, 1] (row index = 0, column index = 1).

- Then, the resulting field should be:

```
[
 [-1, -1, 1, 0],
 [2, 2, 1, 0],
 [0, 0, 0, 0]
]
```

Your function should return the resulting 2D array after taking the following three arguments:

1. **bombs** : A list of bomb locations.  Given as an array of arrays.  Example: [[0, 0], [0, 1]] ([row index = 0, column index = 0], [row index = 0, column index = 1].  Assume that there are no duplicates.

2. **num_rows** : The number of rows in the resulting field.

3. **num_columns** : : The number of columns in the resulting field.

In the resulting field:

- **-1** represents that there is a bomb in that location.
- **1, 2, 3... etc** represents that there are **1, 2, 3... etc** bombs in the surrounding cells (including diagonally adjacent cells).
- **0** represents that there are no bombs in the surrounding cells.

## 접근 방법

- 주어진 조건의 행(row)과 열(column)로 원소가 0인 이차원 배열을 만든다. 

- 폭탄의 위치를 `-1`로 표기한다.

- bfs를 이용하여 `대각선 포함 상하좌우`를 탐색하며 `-1`을 발견하면 `+1`을 해준다. 

## 내 풀이

```python
from collections import deque


def bfs(y, x, field, num_rows, num_cols):
    dx = [0, 1, 0, -1, -1, 1, -1, 1]
    dy = [1, 0, -1, 0, 1, 1, -1, -1]

    q = deque()
    q.append((y, x))

    while q:
        y, x = q.popleft()
        for i in range(8):
            ny = y + dy[i]
            nx = x + dx[i]

            if ny < 0 or nx < 0 or ny >= num_rows or nx >= num_cols: continue
            if field[y][x] == -1: continue

            if field[ny][nx] == -1:
                field[y][x] += 1
                q.append((ny, nx))
    return field


def mine_sweeper(bombs, num_rows, num_cols):
    field = [[0 for i in range(num_cols)] for j in range(num_rows)]

    for r, c in bombs:
        field[r][c] = -1

    for i in range(num_cols):
        for j in range(num_rows):
            field = bfs(j, i, field, num_rows, num_cols)

    return field
```
