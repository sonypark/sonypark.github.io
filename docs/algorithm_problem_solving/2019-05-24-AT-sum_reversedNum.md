2019년 5월 24일

# 백준 1357 - 뒤집힌 덧셈 {docsify-ignore-all}

> 출처: https://www.acmicpc.net/problem/1357

## 문제

어떤 수 X가 주어졌을 때, X의 모든 자리수가 역순이 된 수를 얻을 수 있다. Rev(X)를 X의 모든 자리수를 역순으로 만드는 함수라고 하자. 예를 들어, X=123일 때, Rev(X) = 321이다. 그리고, X=100일 때, Rev(X) = 1이다.

두 양의 정수 X와 Y가 주어졌을 때, Rev(Rev(X) + Rev(Y))를 구하는 프로그램을 작성하시오

#### 입력

첫째 줄에 수 X와 Y가 주어진다. X와 Y는 1,000보다 작거나 같은 자연수이다.

#### 출력
각 테스트 케이스에 대해서, 대회에 참가하지 못하는 사람의 수를 출력한다.

#### 예제 입력

```python
123 100
```

#### 예제 출력

```python
233
```

## 내 풀이 : reversed(), join() 이용

```python
import sys
a,b = sys.stdin.readline().split()
ra = int(''.join(list(reversed(a))))
rb = int(''.join(list(reversed(b))))
print(int(''.join(list(reversed(str(ra+rb))))))
```

## 다른 사람 풀이 : slice notation 이용

```python
a,b=input().split()
print(int(str(int(a[::-1])+int(b[::-1]))[::-1]))
```

## 느낀점

- slice notation 을 잘 이용하자.
