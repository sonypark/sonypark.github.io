---
layout: post
title: [백준 10988] 펠린드롬(Palindrome) - 앞뒤가 똑같은 문자열
category: Algorithm Test

tags: [알고리즘, algorithm, python, 파이썬]
comments: true
---
> 출처: https://www.acmicpc.net/problem/10988

> 개인적으로 공부한 내용을 정리한 문서이므로 내용 상 오류가 있을 수 있습니다.
> 잘못된 내용이 있을 경우 댓글로 남겨주시면 감사하겠습니다.

## 문제
알파벳 소문자로만 이루어진 단어가 주어진다. 이때, 이 단어가 팰린드롬인지 아닌지 확인하는 프로그램을 작성하시오.

팰린드롬이란 앞으로 읽을 때와 거꾸로 읽을 때 똑같은 단어를 말한다. 

level, noon은 팰린드롬이고, baekjoon, online, judge는 팰린드롬이 아니다.

#### 입력
첫째 줄에 단어가 주어진다. 단어의 길이는 1보다 크거나 같고, 100보다 작거나 같으며, 알파벳 소문자로만 이루어져 있다.

#### 출력
첫째 줄에 팰린드롬이면 1, 아니면 0을 출력한다.

#### 예제 입력1

```python
level
```

#### 예제 출력1

```python
1
```

#### 예제 입력1

```python
baekjoon
```

#### 예제 출력1

```python
0
```


## 내 풀이: extra 문자열 이용

```python
import sys
s = sys.stdin.readline().rstrip()
tmp = ''
for i in s:
    tmp = i + tmp
if tmp == s:
    print(1)
else:
    print(0)
```

## 다른 사람 풀이 : list slice notation 문법을 이용한 역순 배열

```python
a=input()
b=a[::-1]
if a==b:
    print(1)
else :
    print(0)
```

## 배운점

- Palindrome 여러가지 풀이법
- list slice notation 문법을 이용한 역순 배열

```python
a[start:stop]  # items start through stop-1
a[start:]      # items start through the rest of the array
a[:stop]       # items from the beginning through stop-1
a[:]           # a copy of the whole array
```

```python
a[start:stop:step] # start through not past stop, by step
```

```python
a[-1]    # last item in the array
a[-2:]   # last two items in the array
a[:-2]   # everything except the last two items
```

```python
a[::-1]    # all items in the array, reversed
a[1::-1]   # the first two items, reversed
a[:-3:-1]  # the last two items, reversed
a[-3::-1]  # everything except the last two items, reversed
```

## 느낀점

- list slice notation 을 잘 활용하자. 매우 유용하다.


