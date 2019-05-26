2019년 5월 26일

# 백준 11170 - 0의 개수 {docsify-ignore-all}

> 출처: https://www.acmicpc.net/problem/11170

## 문제

N부터 M까지의 수들을 종이에 적었을 때 종이에 적힌 0들을 세는 프로그램을 작성하라.

예를 들어, N, M이 각각 0, 10일 때 0을 세면 0에 하나, 10에 하나가 있으므로 답은 2이다.

#### 입력

첫 번째 줄에 테스트 케이스의 수 T가 주어진다.

각 줄에는 N과 M이 주어진다.

- 1 ≤ T ≤ 20
- 0 ≤ N ≤ M ≤ 1,000,000

#### 출력

각각의 테스트 케이스마다 N부터 M까지의 0의 개수를 출력한다.

#### 예제 입력

```python
3
0 10
33 1005
1 4
```

#### 예제 출력

```python
2
199
0
```

## 내 풀이

> 시간: 4024 ms

```python
import sys
t = int(input())

for _ in range(t):
   a,b = map(int, sys.stdin.readline().split())
   zero_count = 0

   for i in range(a,b+1):
       zero_count += int(str(i).count('0'))
   print(zero_count)
```

## 다른 사람 풀이 : 주어진 범위만큼 미리 배열에 만들어 놓기

> 시간: 648 ms

```python
K=[str(i).count('0') for i in range(1000001)]
for _ in range(int(input())):
	N,M=map(int,input().split())
	print(sum(K[N:M+1]))
```

## 느낀점

- 이런 문제는 주어진 범위만큼 미리 계산해 배열에 넣어두면 좋다.
- 한 번 계산한 값을 가져다 쓰므로 속도가 훨씬 빠르다.
