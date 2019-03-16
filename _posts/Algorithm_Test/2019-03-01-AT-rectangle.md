---
layout: post
title: Lv1 - 직사각형의 꼭지점 찾기
category: Algorithm Test

tags: [알고리즘, algorithm, python, 파이썬]
comments: true
---
> 출처: 코드스쿼드 마스터코스 온라인코딩 데모 테스트

## 문제
직사각형을 만드는 데 필요한 4개의 점 중 3개의 좌표가 주어질 때, 나머지 한 점의 좌표를 구하려고 합니다. 직사각형을 이루는 좌표를 담은 배열 v와 배열 v의 길이 v_len이 매개변수로 주어질 때, 직사각형을 만드는 데 필요한 나머지 한 점의 좌표를 return 하도록 solution 함수를 완성해주세요. 단, 직사각형의 각 변은 x축, y축에 평행하며, 반드시 직사각형을 만들 수 있는 경우만 입력으로 주어집니다.

#### 제한사항
- v는 세 점의 좌표가 들어있는 2차원 배열입니다.
- v의 각 원소는 점의 좌표를 나타내며, 좌표는 [x축 좌표, y축 좌표] 순으로 주어집니다.
- 좌표값은 1 이상 10억 이하의 자연수입니다.
- v_len은 항상 3입니다.
- 직사각형을 만드는 데 필요한 나머지 한 점의 좌표를 [x축 좌표, y축 좌표] 순으로 담아 return 해주세요.


#### 입출력 예

v | v_len | return
:--------: | :---------:  | :-----------:
[[1, 4], [3, 4], [3, 10]] | 3  | [1,10]
[[1, 1], [2, 2], [1, 2]] | 3   | [2,1]

## 내 풀이
```python
import collections

def fourth_point_of_rectangle(v):
    p4 = [] # 찾고자 하는 4번째 꼭지점 좌표

    x = []
    y = []

    for i in v:
        x.append(i[0])
        y.append(i[1])

    counter_x = collections.Counter(x)
    counter_y = collections.Counter(y)

    xx = [i for i in counter_x if counter_x[i] == 1]
    yy = [i for i in counter_y if counter_y[i] == 1]

    p4.extend(xx)
    p4.extend(yy)
    return p4
```

## 다른 사람 풀이
```python
def rectangle(v):
    p4 = []
    zip_v = zip(*v) # by using `*v` apply all tuples in `v` as separate arguments to the zip() function

    for i in zip_v:
        print(i)
        point = collections.Counter(i)
        print(point)
        p4.extend([i for i in point if point[i] == 1])

    return p4
```

## 배운점
#### append vs extend ([출처: stack overflow](https://stackoverflow.com/questions/252703/difference-between-append-vs-extend-list-methods-in-python))
- append: `객체를` 리스트 끝에 추가 (Appends object at the end)
- extend: 이터러블 `객체에 담긴 요소를` 리스트 끝에 추가 (Extends list by appending elements from the iterable)

```python
x = [1, 2, 3]
x.append([4, 5])

print (x)
=> [1, 2, 3, [4, 5]]
```

```python
x = [1, 2, 3]
x.extend([4, 5])

print (x)
=>[1, 2, 3, 4, 5]
```

#### zip()
- zip(): 같은 길이의 리스트를 같은 인덱스 요소끼리 잘라 튜플 형태로 반환
- `*`는 sequence/collection을 언팩(unpack) 하는 기능이 있다.
- v = [[1, 4], [3, 4], [3, 10]] 일 때 *v 하면 v = [1, 4] [3, 4] [3, 10]
- zip(*v) => (1, 3, 3), (4, 4, 10) 형태의 zip 객체 반환

