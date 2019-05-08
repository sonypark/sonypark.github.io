---
layout: post
title: [백준 9506] 약수들의 합
category: Algorithm Test

tags: [알고리즘, algorithm, python, 파이썬]
comments: true
---

> 출처: https://www.acmicpc.net/problem/9506

> 개인적으로 공부한 내용을 정리한 문서이므로 내용 상 오류가 있을 수 있습니다.
> 잘못된 내용이 있을 경우 댓글로 남겨주시면 감사하겠습니다.

## 문제
어떤 숫자 n이 자신을 제외한 모든 약수들의 합과 같으면, 그 수를 완전수라고 한다. 

예를 들어 6은 6 = 1 + 2 + 3 으로 완전수이다.

n이 완전수인지 아닌지 판단해주는 프로그램을 작성하라.

#### 입력
- 입력은 테스트 케이스마다 한 줄 간격으로 n이 주어진다. (2 < n < 100, 000)

- 입력의 마지막엔 -1이 주어진다.

#### 출력
- 테스트케이스 마다 한줄에 하나씩 출력해야 한다.

- n이 완전수라면, n을 n이 아닌 약수들의 합으로 나타내어 출력한다(예제 출력 참고).

- 이때, 약수들은 오름차순으로 나열해야 한다.

- n이 완전수가 아니라면 n is NOT perfect. 를 출력한다.


#### 예제 입력

```python
6
12
28
-1
```

#### 예제 출력

```python
6 = 1 + 2 + 3
12 is NOT perfect.
28 = 1 + 2 + 4 + 7 + 14
```

## 내 풀이: template literal, string slice 이용

```python
import sys

def perfectNum(ll,s,n):
    if (s == n):
        answer = "%d = " % (s)
        ll.sort()
        for j in ll:
            answer += "%d + " % (j)
        print(answer[:-2])
    else:
        print("%d is NOT perfect." % (n))

while True:
    n = int(sys.stdin.readline())
    if n == -1:
        break

    ll = []
    # for i in range(1,round(n/2)+1): # n/2 가 아니라 n의 제곱근까지만 계산하는 게 더 빠르다.
    for i in range(1,int(n ** 0.5)+1):
        if(n % i ==0):
            a = n // i
            if(i == a):
                ll.append(i)
            elif (a not in ll) :
                ll.append(i)
                ll.append(a)
    ll.remove(n)
    s = sum(ll)
    perfectNum(ll,s,n)
```

## 다른 사람 풀이

- 내 풀이와 방식은 비슷하지만 더 깔끔하다.

```python
def get_measure(input_num):
    ret = []
    for i in range(1, int(input_num ** 0.5) + 1):
        if input_num % i == 0:
            ret.append(i)
            ret.append(input_num // i)
    ret.sort()
    ret.pop()
    return ret


def verify(input_num, measure_list):
    if sum(measure_list) == input_num:
        return True
    return False


n = int(input())
while n != -1:
    measureList = get_measure(n)
    if verify(n, measureList):
        print(str(n) + " = " + " + ".join(map(str, measureList)))
    else:
        print(str(n) + " is NOT perfect.")
    n = int(input())
```


## 배운점

- Python template literal
- 숫자는 `%d`, 문자는 `%s`

```python
x = ""%d is NOT perfect." % 10
firstName = "sony"
LastName = "park"
y = "My first name is %s and last name is %s." % (firstName, LastName)
```

- string slice
- 문자열의 마지막 값을 제외하고 리턴할 때

```python
st =  "123456789"
st = st[:-1]  # 12345678 
```

## 느낀점

- 그 동안 알고리즘 문제를 풀 때는 무작정 키보드에 손이 간 적이 대부분이었다.
- 이번에는 노트에 어떻게 풀지 설계를 한 뒤 풀었다.
- 이렇게 하니 훨씬 빨리 짤 수 있었고 중간에 오류가 나도 쉽게 해결 했다.
- 정답도 한 번에 맞추었다.
- 앞으로는 노트에 설계를 먼저 하는 습관을 들여야겠다.


