2019년 5월 22일

# Lv2 - 가장 큰 수

> 출처: https://programmers.co.kr/learn/courses/30/lessons/42746

## 문제

0 또는 양의 정수가 주어졌을 때, 정수를 이어 붙여 만들 수 있는 가장 큰 수를 알아내 주세요.

예를 들어, 주어진 정수가 [6, 10, 2]라면 [6102, 6210, 1062, 1026, 2610, 2106]를 만들 수 있고, 이중 가장 큰 수는 6210입니다.

0 또는 양의 정수가 담긴 배열 numbers가 매개변수로 주어질 때, 순서를 재배치하여 만들 수 있는 가장 큰 수를 문자열로 바꾸어 return 하도록 solution 함수를 작성해주세요.

#### 제한사항

- 두 수는 1이상 1000000이하의 자연수입니다.

## 풀이 1 : 시간 초과

- 모든 순열 계산 : 시간 초과

```python
import itertools

def maxNum(numbers):
    numbers = list(map(str,numbers))
    p = list(itertools.permutations(numbers, len(numbers)))
    answer = []
    for i in p:
        e = ''.join(i)
        answer.append(e)
    answer.sort()
    return answer[-1]
```

## 풀이 2 : 성공

```python
import functools

def cmp(a,b):
    return int(a+b) - int(b+a)

def solution(numbers):
    numbers = list(map(str,numbers))
    tmp_arr = []

    for i in numbers:
        tmp_arr.append(i)
    tmp_arr.sort(key=functools.cmp_to_key(cmp), reverse=True)
    answer = ''.join(tmp_arr)

    if int(answer) == 0:
        return '0'
    return answer
```

## 배운점

- `sort` 함수의 `key` 옵션

> 출처: https://docs.python.org/3/howto/sorting.html

```python
def numeric_compare(x, y):
    return x - y
sorted([5, 2, 4, 1, 3], cmp=numeric_compare)

# [1, 2, 3, 4, 5]
```

```python
def reverse_numeric(x, y):
    return y - x
sorted([5, 2, 4, 1, 3], cmp=reverse_numeric)

# [5, 4, 3, 2, 1]
```

## 느낀점

- `sort` 함수의 `key` 옵션은 정말 강력하다.
- 이 문제는 개인적으로 풀기가 까다로웠는데 덕분에 `sort` 함수의 `key` 옵션에 대해 좀 더 잘 이해할 수 있었다.