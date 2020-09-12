
2019년 11월 11일

# Udemy - Find Where to Expand in Minesweeper (2D Array) {docsify-ignore-all}

> 출처: https://www.udemy.com/course/11-essential-coding-interview-questions/learn/quiz/383880#overview

## 문제

Implement a function that turns revealed cells into -2 given a location the user wants to click.

For simplicity, only reveal cells that have 0 in them.  If the user clicks on any other type of cell (for example, -1 / bomb or 1, 2, or 3), just ignore the click and return the original field.  If a user clicks 0, reveal all other 0's that are connected to it.

### Example 1

Given field:

```
[
 [0, 0, 0, 0, 0],
 [0, 1, 1, 1, 0],
 [0, 1, -1, 1, 0]
]
```

Click location: **(2, 2: row index = 2, column index = 2)**

Resulting field:

```
[
 [0, 0, 0, 0, 0],
 [0, 1, 1, 1, 0],
 [0, 1, -1, 1, 0]
] (same as the given field)
```

### Example 2

Given field:

```
[
 [-1, 1, 0, 0],
 [1, 1, 0, 0],
 [0, 0, 1, 1],
 [0, 0, 1, -1]
]
```

Click location: **(1, 3: row index = 1, column index = 3)**

Resulting field:

```
[
 [-1, 1, -2, -2],
 [1, 1, -2, -2],
 [-2, -2, 1, 1],
 [-2, -2, 1, -1]
]
```

Your function should take:

### 제한 사항

- field: The given field as a 2D array
- num_rows / numRows: The number of rows in the given field
- num_cols / numCols: The number of columns in the given field
- given_i / givenI: The row index of the cell the user wants to click
- given_j / givenJ: The column index of the cell the user wants to click

## 접근 방법

- 클릭한 곳이 `1` 또는 `-1`인 경우 field를 그대로 리턴한다.

- 클릭한 곳이 `0`인 경우
    - bfs를 이용하여 `대각선 포함 상하좌우`를 탐색하며 `0`을 발견하면 `-2`로 바꿔준다.

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
            if field[y][x] == 1: continue

            if field[ny][nx] == 0:
                field[ny][nx] = -2
                q.append((ny, nx))
    return field


def click(field, num_rows, num_cols, given_i, given_j):
    if field[given_i][given_j] == 0:
        for i in range(num_cols):
            for j in range(num_rows):
                field = bfs(j, i, field, num_rows, num_cols)

    return field
```
