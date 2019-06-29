2019년 6월 28일

# 백준 1697 - 숨바꼭질 (BFS) {docsify-ignore-all}

> 출처: https://www.acmicpc.net/problem/1697

## 문제

수빈이는 동생과 숨바꼭질을 하고 있다. 수빈이는 현재 점 N(0 ≤ N ≤ 100,000)에 있고, 동생은 점 K(0 ≤ K ≤ 100,000)에 있다. 수빈이는 걷거나 순간이동을 할 수 있다. 만약, 수빈이의 위치가 X일 때 걷는다면 1초 후에 X-1 또는 X+1로 이동하게 된다. 순간이동을 하는 경우에는 1초 후에 2*X의 위치로 이동하게 된다.

수빈이와 동생의 위치가 주어졌을 때, 수빈이가 동생을 찾을 수 있는 가장 빠른 시간이 몇 초 후인지 구하는 프로그램을 작성하시오.

#### 입력

첫 번째 줄에 수빈이가 있는 위치 N과 동생이 있는 위치 K가 주어진다. N과 K는 정수이다.

#### 출력

수빈이가 동생을 찾는 가장 빠른 시간을 출력한다.

#### 예제 입력

```
5 17
```

#### 예제 출력

```
4
```

## 접근 방법

- 술래의 좌표를 `x`로 놓고 시작한다.

- `x`는 1초마다 `(x-1), (x+2), (x*2)` 중 하나로 이동힌다.

- 이동 중에 범위(`0<=x<=100000`)를 벗어난 경우는 제외한다.

- 이동하면서 걸린 시간을 `dict`에 저장한다.

- `x`의 좌표가 `K` 의 위치와 같아지면 종료한다.

## 내 풀이

```python
import sys
from collections import deque

q = deque()
dist = dict()

N, K = map(int, sys.stdin.readline().split())

def bfs():
    q.append(N)
    dist[N] = 0

    while q:
        x = q.popleft()
        if x == K:
            return dist[x]
        for nx in (x-1), (x+1), (2*x):
            if nx < 0 or nx > 100000: continue
            if dist.get(nx) is None:
                dist[nx] = dist[x]+1
                q.append(nx)

print(bfs())
```

## 느낀점

- BFS 문제에 대해 아주 조금은 감이 잡히는 것 같다.

