---
layout: post
title: 백준 2490 - 윷놀이
category: Algorithm Test

tags: [알고리즘, algorithm, python, 파이썬]
comments: true
---

> 출처: https://www.acmicpc.net/problem/2490

> 개인적으로 공부한 내용을 정리한 문서이므로 내용 상 오류가 있을 수 있습니다.
> 잘못된 내용이 있을 경우 댓글로 남겨주시면 감사하겠습니다.

## 문제
우리나라 고유의 윷놀이는 네 개의 윷짝을 던져서 배(0)와 등(1)이 나오는 숫자를 세어 도, 개, 걸, 윷, 모를 결정한다. 네 개 윷짝을 던져서 나온 각 윷짝의 배 혹은 등 정보가 주어질 때 도(배 한 개, 등 세 개), 개(배 두 개, 등 두 개), 걸(배 세 개, 등 한 개), 윷(배 네 개), 모(등 네 개) 중 어떤 것인지를 결정하는 프로그램을 작성하라.

#### 입력
첫째 줄부터 셋째 줄까지 각 줄에 각각 한 번 던진 윷짝들의 상태를 나타내는 네 개의 정수(0 또는 1)가  빈칸을 사이에 두고 주어진다.

#### 출력
첫째 줄부터 셋째 줄까지 한 줄에 하나씩 결과를  도는 A, 개는 B, 걸은 C, 윷은 D, 모는 E로 출력한다.

#### 예제 입력

```python
0 1 0 1
1 1 1 0
0 0 1 1
```

#### 예제 출력

```python
B
A
B
```

## 내 풀이 : sort(key=cmp) 이용

```python
import sys
for _ in range(3):
    m = sys.stdin.readline().split()
    count_zero = m.count('0')
    if count_zero == 1: print('A')
    if count_zero == 2: print('B')
    if count_zero == 3: print('C')
    if count_zero == 4: print('D')
    if count_zero == 0: print('E')
```

## 다른 사람 풀이
- 0,1의 합을 이용

```python
b = ['D', 'C', 'B', 'A', 'E']
for i in range(3):
    print(b[sum(list(map(int ,input().split())))])
```


## 배운점

- 도개걸윷모를 0,1로 표현했을 때 0,1의 합(sum)으로 나올 수 있는 경우의 수는 0,1,2,3,4,5 중 하나 이므로 배열의 인덱스를 이용해 풀 수 있다.

