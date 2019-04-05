---
layout: post
title: [백준] 설탕 배달
category: Algorithm Test

tags: [알고리즘, algorithm, python, 파이썬, 피보나치]
comments: true
---
> 출처: https://www.acmicpc.net/problem/2839

> 개인적으로 공부한 내용을 정리한 문서이므로 내용 상 오류가 있을 수 있습니다.


## 문제
상근이는 요즘 설탕공장에서 설탕을 배달하고 있다. 상근이는 지금 사탕가게에 설탕을 정확하게 N킬로그램을 배달해야 한다. 설탕공장에서 만드는 설탕은 봉지에 담겨져 있다. 봉지는 3킬로그램 봉지와 5킬로그램 봉지가 있다.

상근이는 귀찮기 때문에, 최대한 적은 봉지를 들고 가려고 한다. 예를 들어, 18킬로그램 설탕을 배달해야 할 때, 3킬로그램 봉지 6개를 가져가도 되지만, 5킬로그램 3개와 3킬로그램 1개를 배달하면, 더 적은 개수의 봉지를 배달할 수 있다.

상근이가 설탕을 정확하게 N킬로그램 배달해야 할 때, 봉지 몇 개를 가져가면 되는지 그 수를 구하는 프로그램을 작성하시오.


#### 입력
- 첫째 줄에 N이 주어진다. (3 ≤ N ≤ 5000)

#### 출력
- 상근이가 배달하는 봉지의 최소 개수를 출력한다. 만약, 정확하게 N킬로그램을 만들 수 없다면 -1을 출력한다.

#### 입출력 예

s | return
:---------:  | :-----------:
18	| 4
4	| -1
6	| 2
9	| 3
11	| 3

## 내 풀이

```angular2
sugar 가 5로 나누어 떨어지면
    - sugar 에서 5kg을 빼주고 pack_num 를 하나 추가한다.
그렇지 않으면
    - sugar 에서 3kg을 빼주고 pack_num 를 하나 추가한다.
이 과정을 sugar 가 0이 될 때 까지 반복한다
sugar 가 0 밑으로 떨어지면 -1을 출력한다.
```

```python
sugar = int(input())
pack_num = 0

while(sugar>0):
    if(sugar % 5 == 0):
        sugar -= 5
        pack_num += 1
    else:
        sugar -= 3
        pack_num += 1

    if(sugar < 0):
        print(-1)
        break

if(sugar ==0):
    print(pack_num)
```

## 느낀점
- 나머지를 기준으로 로직을 분류하는 것보다 나누어 떨어질 경우 바로 결과에 반영해 재귀적으로 푸는 게 훨씬 직관적이다. 

