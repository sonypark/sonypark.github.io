2019년 6월 14일

# 백준 10989 - 수 정렬하기 3 (countingSort) {docsify-ignore-all}

> 출처: https://www.acmicpc.net/problem/10989

## 문제

N개의 수가 주어졌을 때, 이를 오름차순으로 정렬하는 프로그램을 작성하시오.

#### 입력

첫째 줄에 수의 개수 N(1 ≤ N ≤ 10,000,000)이 주어진다. 둘째 줄부터 N개의 줄에는 숫자가 주어진다. 이 수는 10,000보다 작거나 같은 자연수이다.

#### 출력

첫째 줄부터 N개의 줄에 오름차순으로 정렬한 결과를 한 줄에 하나씩 출력한다.

#### 예제 입력

```
10
5
2
3
1
4
2
3
5
1
7
```

#### 예제 출력

```
1
1
2
2
3
3
4
5
5
7
```

## 접근 방법

1. 단순 정렬로는 시간 초과가 난다.

2. counting sort를 이용해 정렬한다.

## 내 풀이 1 : 시간 초과

> 정렬을 두 번 하기 때문에 시간초과가 난다.

```python
import sys
n = int(sys.stdin.readline())

## 메모리 초과 (실패)
def sortNum(n):
    ll =[]
    for i in range(1, n+1):
        ll.append(int(sys.stdin.readline()))

    for j in sorted(ll):
        print(j)
sortNum(n)
```

## 내 풀이 2 : Counting Sort

> Memorization, 미리 주어진 수의 크기만큼 배열을 만들어 값을 저장한다.

```python
n = int(input())

def countingSort(n):
    count_list = [0] * (10001) # 주어지는 수의 크기 범위만큼 리스트 길이를 만든다.
    for _ in range(n):
        a = int(sys.stdin.readline())
        count_list[a] += 1

    for j in range(len(count_list)):
        if count_list[j] != 0:
            for _ in range(count_list[j]):
                print(j)

countingSort(n)
```

## 다른 사람 풀이 : Dictionary 이용

```python
n = int(input())

def sortNum_dic(n):
    dic = {}
    for _ in range(n):
        i = int(sys.stdin.readline())
        if i in dic:
            dic[i] = dic[i] + 1
        else:
            dic[i] = 1

    for j in sorted(dic.items()):
        for _ in range(j[1]):
            print(j[0])

sortNum_dic(n)
```

## 배운점

- `counting sort`를 처음 사용해봤다.

- `dictionary`를 이용한 `counting sort` 풀이
