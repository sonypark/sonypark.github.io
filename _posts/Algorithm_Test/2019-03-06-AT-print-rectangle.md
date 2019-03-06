---
layout: post
title: Lv1 - 직사각형 별찍
category: Algorithm Test

tags: [알고리즘, algorithm, python, 파이썬]
comments: true
---
> 출처: https://programmers.co.kr/learn/courses/30/lessons/12969

> 개인적으로 공부한 내용을 정리한 문서이므로 내용 상 오류가 있을 수 있습니다.

## 문제
이 문제에는 표준 입력으로 두 개의 정수 n과 m이 주어집니다.
별(*) 문자를 이용해 가로의 길이가 n, 세로의 길이가 m인 직사각형 형태를 출력해보세요.

#### 제한사항
- n과 m은 각각 1000 이하인 자연수입니다.

#### 입출력 예

##### 입력

```
5 3
```

##### 출력

```
*****
*****
*****
```

## 내 풀이
```python
a,b = map(int, input().strip().split(' '))
for _ in range(b):
    print(a*'*')
```

## 다른 사람 풀이
```python
a, b = map(int, input().strip().split(' '))
answer = ('*'*a +'\n')*b
print(answer)
```

## 배운점
- 입력값을 받아 처리할 때 input() 함수와 map() 함수를 이용한다.

