2019년 6월 29일

# 백준 2667 - 단지내번호붙이기 (DFS/BFS) {docsify-ignore-all}

> 출처: https://www.acmicpc.net/problem/2667

## 문제

<그림 1>과 같이 정사각형 모양의 지도가 있다. 1은 집이 있는 곳을, 0은 집이 없는 곳을 나타낸다. 철수는 이 지도를 가지고 연결된 집들의 모임인 단지를 정의하고, 단지에 번호를 붙이려 한다. 여기서 연결되었다는 것은 어떤 집이 좌우, 혹은 아래위로 다른 집이 있는 경우를 말한다. 대각선상에 집이 있는 경우는 연결된 것이 아니다. <그림 2>는 <그림 1>을 단지별로 번호를 붙인 것이다. 지도를 입력하여 단지수를 출력하고, 각 단지에 속하는 집의 수를 오름차순으로 정렬하여 출력하는 프로그램을 작성하시오.

![](https://user-images.githubusercontent.com/34808501/60385129-dd608780-9ac0-11e9-8233-9cbe8b9237fb.png)

#### 입력

첫 번째 줄에는 지도의 크기 N(정사각형이므로 가로와 세로의 크기는 같으며 5≤N≤25)이 입력되고, 그 다음 N줄에는 각각 N개의 자료(0혹은 1)가 입력된다.

#### 출력

첫 번째 줄에는 총 단지수를 출력하시오. 그리고 각 단지내 집의 수를 오름차순으로 정렬하여 한 줄에 하나씩 출력하시오.

#### 예제 입력

```
7
0110100
0110101
1110101
0000111
0100000
0111110
0111000
```

#### 예제 출력

```
3
7
8
9
```

## 접근 방법

1. 지도에서 값이 `1`인 좌표만 탐색한다.

2. 탐색한 `1`은 `0`으로 바꾼다. -- **이게 핵심!**

3. `DFS/BFS` 탐색을 통해 인접한 `1`을 발견할 때마다 `count+1` 해준다.

4. 리턴한 `count` 값은 `apartment` 배열에 담는다.

5. 지도의 모든 좌표를 탐색할 때까지 위 과정을 반복한다.

- 배열 `apartment`의 길이가 `단지 수`가 된다.

- 배열 `apartment`에 담긴 `단지 내 집수`를 오름차순 정렬하여 출력한다.

## 내 풀이

```python
import sys
from collections import deque

n = int(sys.stdin.readline())
dy = [-1,0,1,0]
dx = [0,-1,0,1]

a = [list(map(int,sys.stdin.readline().rstrip())) for _ in range(n)]
apartment = []

def bfs(i,j):
    q = deque()
    q.append((i,j))
    count = 1

    while q:
        y, x = q.popleft()
        for i in range(4):
            ny = y + dy[i]
            nx = x + dx[i]
            if ny < 0 or nx < 0 or ny >= n or nx >= n: continue
            if a[ny][nx] == 1:
                a[ny][nx] = 0
                count +=1
                q.append((ny, nx))
    return count

for i in range(n):
    for j in range(n):
        if a[i][j] == 1:
            a[i][j] = 0
            apartment.append(bfs(i,j))

print(len(apartment))
apartment.sort()

for a in apartment:
    print(a)
```

## 느낀점

- DFS/BFS 문제는 여전히 어렵다.

- 탐색한 1을 0으로 바꾸는 부분은 다른 사람의 풀이를 보고 힌트를 얻었다.

