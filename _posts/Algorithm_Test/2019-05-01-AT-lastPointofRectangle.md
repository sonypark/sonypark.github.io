---
layout: post
title: [백준 3009] 직사각형 네 번 째 점
category: Algorithm Test

tags: [알고리즘, algorithm, python, 파이썬]
comments: true
---

> 출처: https://www.acmicpc.net/problem/3009

> 개인적으로 공부한 내용을 정리한 문서이므로 내용 상 오류가 있을 수 있습니다.
> 잘못된 내용이 있을 경우 댓글로 남겨주시면 감사하겠습니다.

## 문제
세 점이 주어졌을 때, 축에 평행한 직사각형을 만들기 위해서 필요한 네 번째 점을 찾는 프로그램을 작성하시오.

#### 입력
세 점의 좌표가 한 줄에 하나씩 주어진다. 좌표는 1보다 크거나 같고, 1000보다 작거나 같은 정수이다.

#### 출력
직사각형의 네 번째 점의 좌표를 출력한다.

#### 예제 입력

```python
30 20
10 10
10 20
```

#### 예제 출력

```python
30 10
```

## 내 풀이1: collections 이용

```python
import sys
import collections

x = []
y = []
for _ in range(3):
    a,b = map(int, sys.stdin.readline().split())
    x.append(a)
    y.append(b)

counter_x = collections.Counter(x)
counter_y = collections.Counter(y)
xx = [i for i in counter_x if counter_x[i] == 1]
yy = [i for i in counter_y if counter_y[i] == 1]
print(xx[0], yy[0])
```

## 내 풀이2: collections, zip 이용
```python
z = []
p = []
for _ in range(3):
    t = tuple(map(int, sys.stdin.readline().split()))
    z.append(t)

zz = list(zip(*z))
for i in zz:
    point = collections.Counter(i)
    p.extend([i for i in point if point[i] ==1])

print(*p)
```


## 다른 사람 풀이1

```python
x = []
y = []
for _ in range(3):
    x1, y1 = map(int, sys.stdin.readline().split())

    if x1 not in x:
        x.append(x1)
    else:
        x.remove(x1)

    if y1 not in y:
        y.append(y1)
    else:
        y.remove(y1)
print(x[0], y[0])
```

## 다른 사람 풀이2

```python
x = []
y = []
p = []
for _ in range(3):
    x1, y1 = map(int, sys.stdin.readline().split())
    x.append(x1)
    y.append(y1)
    x.sort()
    y.sort()

if x[0] == x[1]:
  p.append(x[2])
else:
  p.append(x[0])

if y[0] == y[1]:
  p.append(y[2])
else:
  p.append(y[0])

print(*p)
```

## 배운점
- 배열에서 `not in` 을 이용한 풀이


## 느낀점
- 배열에서 `not in` 을 잘 사용하자

- 간단하게 풀 수 있는 문제를 복잡하게 풀었다.
    - 굳이 collections를 쓰지 않아도 됐다.

- 다른 사람의 풀이를 보면서 많이 배운다.


