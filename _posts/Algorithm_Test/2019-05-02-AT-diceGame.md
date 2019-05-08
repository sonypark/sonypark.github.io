---
layout: post
title: [백준 2476] 주사위 게임
category: Algorithm Test

tags: [알고리즘, algorithm, python, 파이썬]
comments: true
---

> 출처: https://www.acmicpc.net/problem/2476

> 개인적으로 공부한 내용을 정리한 문서이므로 내용 상 오류가 있을 수 있습니다.
> 잘못된 내용이 있을 경우 댓글로 남겨주시면 감사하겠습니다.

## 문제
1에서부터 6까지의 눈을 가진 3개의 주사위를 던져서 다음과 같은 규칙에 따라 상금을 받는 게임이 있다.

같은 눈이 3개가 나오면 10,000원+(같은 눈)*1,000원의 상금을 받게 된다. 
같은 눈이 2개만 나오는 경우에는 1,000원+(같은 눈)*100원의 상금을 받게 된다. 
모두 다른 눈이 나오는 경우에는 (그 중 가장 큰 눈)*100원의 상금을 받게 된다.  
예를 들어, 3개의 눈 3, 3, 6이 주어지면 상금은 1,000+3*100으로 계산되어 1,300원을 받게 된다. 또 3개의 눈이 2, 2, 2로 주어지면 10,000+2*1,000 으로 계산되어 12,000원을 받게 된다. 3개의 눈이 6, 2, 5로 주어지면 그 중 가장 큰 값이 6이므로 6*100으로 계산되어 600원을 상금으로 받게 된다.

N(2 ≤ N ≤ 1,000)명이 주사위 게임에 참여하였을 때, 가장 많은 상금을 받은 사람의 상금을 출력하는 프로그램을 작성하시오.

#### 입력
첫째 줄에는 참여하는 사람 수 N이 주어지고 그 다음 줄부터 N개의 줄에 사람들이 주사위를 던진 3개의 눈이 빈칸을 사이에 두고 각각 주어진다. 

#### 출력
첫째 줄에 가장 많은 상금을 받은 사람의 상금을 출력한다.

#### 예제 입력

```python
3
3 3 6
2 2 2
6 2 5
```

#### 예제 출력

```python
12000
```

## 내 풀이: collections 이용

```python
import sys
import collections

n = int(sys.stdin.readline())
answer = []
def counter(n):
    for i in range(n):
        ll = list(map(int, sys.stdin.readline().split()))

        count = collections.Counter(ll)
        mostCommonNum = count.most_common()
        lenOfNum = len(count)
        result = 0
        if lenOfNum == 1:
            result = 10000 + (1000*mostCommonNum[0][0])
        if lenOfNum == 2:
            result = 1000 + (100*mostCommonNum[0][0])
        if lenOfNum == 3:
            result = 100*(max(ll))
        answer.append(result)

counter(n)
print(max(answer))
```

## 다른 사람 풀이

```python
import sys
n = int(sys.stdin.readline())
value = []
for i in range(n):
    l = list(map(int, sys.stdin.readline().split()))
    l.sort()
    if( l[0] == l[2] ):
        value.append(10000 + l[0]*1000)
    elif( (l[0] == l[1])or(l[1] == l[2]) ):
        value.append(1000 + l[1]*100)
    else:
        value.append( 100 * l[2] )

print(max(value))
```


## 배운점
- collections.Counter.most_common()
- 가장 많이 나온 값의 key,value를 튜플 형태로 반환해준다.

```python
Counter('abracadabra').most_common(3)
=> [('a', 5), ('r', 2), ('b', 2)]
```
