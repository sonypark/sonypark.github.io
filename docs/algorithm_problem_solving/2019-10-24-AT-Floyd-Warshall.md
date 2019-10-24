
2019년 10월 25일

# 백준 11403 - 경로 찾기 (플로이드 와샬) {docsify-ignore-all}

> 출처: https://www.acmicpc.net/problem/11403

## 문제

가중치 없는 방향 그래프 G가 주어졌을 때, **모든 정점 (i, j)에 대해서, i에서 j로 가는 경로가 있는지 없는지 구하는 프로그램**을 작성하시오.

#### 입력

첫째 줄에 정점의 개수 N (1 ≤ N ≤ 100)이 주어진다. 둘째 줄부터 N개 줄에는 그래프의 인접 행렬이 주어진다. i번째 줄의 j번째 숫자가 1인 경우에는 i에서 j로 가는 간선이 존재한다는 뜻이고, 0인 경우는 없다는 뜻이다. i번째 줄의 i번째 숫자는 항상 0이다.

#### 출력

총 N개의 줄에 걸쳐서 문제의 정답을 인접행렬 형식으로 출력한다. 정점 i에서 j로 가는 경로가 있으면 i번째 줄의 j번째 숫자를 1로, 없으면 0으로 출력해야 한다.

#### 예제 입력1

```
3
0 1 0
0 0 1
1 0 0
```

#### 예제 출력1

```
1 1 1
1 1 1
1 1 1
```

#### 예제 입력2

```
7
0 0 0 1 0 0 0
0 0 0 0 0 0 1
0 0 0 0 0 0 0
0 0 0 0 1 1 0
1 0 0 0 0 0 0
0 0 0 0 0 0 1
0 0 1 0 0 0 0
```

#### 예제 출력2

```
1 0 1 1 1 1 1
0 0 1 0 0 0 1
0 0 0 0 0 0 0
1 0 1 1 1 1 1
1 0 1 1 1 1 1
0 0 1 0 0 0 1
0 0 1 0 0 0 0
```

## 접근 방법

- **모든 정점에 대한 경로를 구하는 알고리즘** 은 플로이드 와샬 알고리즘으로 풀 수 있다.

https://ko.wikipedia.org/wiki/%ED%94%8C%EB%A1%9C%EC%9D%B4%EB%93%9C-%EC%9B%8C%EC%85%9C_%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98

## 내 풀이

```python
import sys
from collections import deque

N = int(input())

graph = [list(map(int,sys.stdin.readline().split())) for i in range(N)]

#플로이드 워셜 알고리즘(Floyd Warshall Algorithm) 이용
for k in range(0, N) :
    for i in range(0, N) :
        for j in range(0, N):
            if graph[i][k] and graph[k][j] :
                graph[i][j] = 1

for g in graph:
    print(*g)
```

## 배운점

- 모든 정점에 대한 경로를 구하는 문제는 플로이드 와샬 알고리즘을 이용해 풀면 쉽게 풀 수 있다.
