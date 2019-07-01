2019년 7월 1일

# 백준 11724 - 연결 요소의 개수 (DFS/BFS) {docsify-ignore-all}

> 출처: https://www.acmicpc.net/problem/11724

## 문제

방향 없는 그래프가 주어졌을 때, 연결 요소 (Connected Component)의 개수를 구하는 프로그램을 작성하시오.

#### 입력

첫째 줄에 정점의 개수 N과 간선의 개수 M이 주어진다. (1 ≤ N ≤ 1,000, 0 ≤ M ≤ N×(N-1)/2) 둘째 줄부터 M개의 줄에 간선의 양 끝점 u와 v가 주어진다. (1 ≤ u, v ≤ N, u ≠ v) 같은 간선은 한 번만 주어진다.

#### 출력

첫째 줄에 연결 요소의 개수를 출력한다.

#### 예제 입력1

```
6 5
1 2
2 5
5 1
3 4
4 6
```

#### 예제 출력1

```
2
```

#### 예제 입력2

```
6 8
1 2
2 5
5 1
3 4
4 6
5 4
2 4
2 3
```

#### 예제 출력2

```
1
```


## 접근 방법

- 연결 요소란?

- 아래 그림과 같이 그래프 내 모든 노드쌍에 대해 경로가 존재하는 걸 말한다.

    - 특징

    1. 연결 요소에 속한 모든 노드를 연결하는 경로가 있어야 한다.

    2. 다른 연결 요소와 연결되는 경로가 있으면 안 된다.

![](https://user-images.githubusercontent.com/34808501/60411846-ab0e7180-9c09-11e9-8677-8ff62e08dbb0.png)


1. 주어진 조건에 주어진 정점(N)의 개수 만큼 그래프 배열(`a`)을 만든다.

2. 간선으로 이어진 정점을 각 정점 배열에 담는다.

3. 방문한 정점을 체크하기 위해 `visited` 배열을 만든다.

4. 방문하지 않은 정점에 한해 탐색을 시작한다.

5. 탐색을 시작할 때 마다 카운트를 해준다.

## 내 풀이

```python
import sys
from collections import deque

N, M = map(int, sys.stdin.readline().split())

a = [[] for _ in range(N+1)]

for i in range(M):
    v1,v2 = map(int, sys.stdin.readline().split())
    a[v1].append(v2)
    a[v2].append(v1)

visited = [False] * (N+1)


def bfs(v):
    q = deque()
    q.append(v)
    visited[v] = True
    visit_route = []
    while q:
        d = q.popleft()
        visit_route.append(d)

        for i in a[d]:
            if visited[i] is False:
                visited[i] = True
                q.append(i)
    return visit_route


CC = []
for v in range(1, N+1):
    if visited[v] is False:
        CC.append(bfs(v))
print(len(CC))
```
