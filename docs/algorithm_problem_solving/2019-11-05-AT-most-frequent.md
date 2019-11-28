
2019년 11월 5일

# Udemy - Most Frequently Occuring Item (Array) {docsify-ignore-all}

> 출처: https://www.udemy.com/course/11-essential-coding-interview-questions/learn/quiz/377806#overview

## 문제

Find the most frequently occuring item in an array.

### Example

The most frequelty occuring item in `[1, 3, 1, 3, 2, 1]` is `1`

If you're given an empty array, you should return null (in Java) or None (in Python).

### 제한 사항

You can assume that there is always a single, unique value that appears most frequently unless the array is empty.  

For instance, you won't be given an array such as `[1, 1, 2, 2]`

## 접근 방법

- 딕셔너리에 배열의 item을 담는다.

- `key`는 `item`, `value`에는 `item`이 나온 횟수를 저장한다.

- `max_count` 변수를 이용해 가장 큰 `value`를 가진 `item`을 출력한다.

## 내 풀이

```python
def cmp(x):
    return x[1]

def most_frequent(given_list):
    if len(given_list) == 0: return None

    count = dict()

    max_item = None
    max_count = 0
    for number in given_list:
        if number not in count:
            count[number] = 1
        else:
            count[number] +=1

        if max_count < count[number]:
            max_count = count[number]
            max_item = number
    return max_item
```
