---
layout: post
title: 백준 1408 - 24
category: Algorithm Test

tags: [알고리즘, algorithm, python, 파이썬]
comments: true
---

> 출처: https://www.acmicpc.net/problem/1408

> 개인적으로 공부한 내용을 정리한 문서이므로 내용 상 오류가 있을 수 있습니다.
> 잘못된 내용이 있을 경우 댓글로 남겨주시면 감사하겠습니다.

## 문제
도현이는 선영이를 임무를 시작한지 정확하게 24시간이 되는 순간에 잡으려고 한다.

만약 지금 시간이 13:52:30이고, 임무를 시작한 시간이 14:00:00 이라면 도현이에게 남은시간은 00:07:30 이다.

모든 시간은 00:00:00 ~ 23:59:59로 표현할 수 있다. 입력과 출력에 주어지는 모든 시간은 XX:XX:XX 형태이며, 숫자가 2자리가 아닐 경우에는 0으로 채운다.

도현이가 임무를 시작한 시간과, 현재 시간이 주어졌을 때, 도현이에게 남은 시간을 구하는 프로그램을 작성하시오.


#### 입력
- 첫째 줄에는 현재 시간이, 둘째 줄에는 도현이가 임무를 시작한 시간이 주어진다. 임무를 시작한 시간과 현재 시간이 같은 경우는 주어지지 않는다.

#### 출력
- 첫째 줄에 도현이가 임무를 수행하는데 남은 시간을 문제에서 주어지는 시간의 형태 (XX:XX:XX)에 맞춰 출력한다.

#### 예제 입력

```python
13:52:30
14:00:00
```

#### 예제 출력

```python
00:07:30
```

## 내 풀이 : sort(key=cmp) 이용

```python
import sys

a,b,c = map(int, sys.stdin.readline().split(':'))
d,e,f = map(int, sys.stdin.readline().split(':'))

a = a * 60 * 60
b = b * 60
c = c

d = d * 60 * 60
e = e * 60
f = f

now = a+b+c
mission = d+e+f

# 만약 현재시간이 미션시간보다 크다면
# 미션시간에 +24시간을 해준다
if now > mission:
    mission += 24*60*60
s = mission - now

h = s // 3600
m = (s % 3600) // 60
sec = s % 60

print('{:0>2d}'.format(h) + ':' '{:0>2d}'.format(m) + ':' '{:0>2d}'.format(sec))
```

## 배운점

- Number formatting

<img width="763" alt="Screen Shot 2019-05-09 at 7 16 11 PM" src="https://user-images.githubusercontent.com/34808501/57446147-fef67d00-728e-11e9-9773-3e2f3bda54fd.png">

> 이미지 출처: https://mkaz.blog/code/python-string-format-cookbook/





