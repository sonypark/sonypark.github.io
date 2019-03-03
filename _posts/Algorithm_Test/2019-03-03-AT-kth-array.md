---
layout: post
title: Lv1 - k번째
category: Algorithm Test

tags: [알고리즘, algorithm, python, 파이썬]
comments: true
---
> 출처: https://programmers.co.kr/learn/courses/30/lessons/42748

> 개인적으로 공부한 내용을 정리한 문서이므로 내용 상 오류가 있을 수 있습니다.

## 문제
배열 array의 i번째 숫자부터 j번째 숫자까지 자르고 정렬했을 때, k번째에 있는 수를 구하려 합니다.

예를 들어 array가 [1, 5, 2, 6, 3, 7, 4], i = 2, j = 5, k = 3이라면

1. array의 2번째부터 5번째까지 자르면 [5, 2, 6, 3]입니다.
2. 1에서 나온 배열을 정렬하면 [2, 3, 5, 6]입니다.
3. 2에서 나온 배열의 3번째 숫자는 5입니다.


배열 array, [i, j, k]를 원소로 가진 2차원 배열 commands가 매개변수로 주어질 때, commands의 모든 원소에 대해 앞서 설명한 연산을 적용했을 때 나온 결과를 배열에 담아 return 하도록 solution 함수를 작성해주세요.


#### 제한사항
- array의 길이는 1 이상 100 이하입니다.
- array의 각 원소는 1 이상 100 이하입니다.
- commands의 길이는 1 이상 50 이하입니다.
- commands의 각 원소는 길이가 3입니다.

#### 입출력 예

array | commands | return
:--------: | :---------:  | :-----------:
[1, 5, 2, 6, 3, 7, 4] | [[2, 5, 3], [4, 4, 1], [1, 7, 3]]  | [5, 6, 3]

## 내 풀이
```python
def Kth_array(array, commands):
    answer = []

    for i in commands:
        s = i[0]
        e = i[1]
        k = i[2]
        answer.append(sorted(array[s-1:e])[k-1])
    return answer
```

## 다른 사람 풀이
```python
def solution(array, commands):
    return list(map(lambda x:sorted(array[x[0]-1:x[1]])[x[2]-1], commands))
```

## 배운점
####  lambda 함수 ([출처: w3school.com](https://www.w3schools.com/python/python_lambda.asp)
- `lambda arguments : expression`
- 한 줄의 로직만 표현하고 사라지는 함수. - 메모리에 저장되지 않아 메모를 아낄 수 있다.
- 선언과 동시에 호출이 되기 때문에 간단한 로직을 구현할 때 편리하다.
- append: `객체를` 리스트 끝에 추가 (Appends object at the end)
```python
x = lambda a, b : a * b
print(x(5, 6))
=> 30
```

#### map 함수([출처: w3school.com](https://www.w3schools.com/python/ref_func_map.asp)
- `map(function, iterables)`
- 반복 가능한(iterable) 자료형의 각 요소를 함수에 넣어 실행한 결과를 반환한다.

```python
def myfunc(a, b):
return a + b

x = map(myfunc, ('apple', 'banana', 'cherry'), ('orange', 'lemon', 'pineapple'))
print (x)
=> <map object at 0x034244F0>

#convert the map into a list, for readability:
print (list(x))
=> ['appleorange', 'bananalemon', 'cherrypineapple']
```

