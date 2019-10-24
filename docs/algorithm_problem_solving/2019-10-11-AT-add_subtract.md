
2019년 10월 11일

# Codewars - Basic Math (Add or Subtract) {docsify-ignore-all}

> 출처: https://www.codewars.com/kata/basic-math-add-or-subtract/train/python

## 문제

In this kata, you will do addition and subtraction on a given string. The return value must be also a string.

Note: the input will not be empty.

### Example

```
"1plus2plus3plus4"  --> "10"
"1plus2plus3minus4" -->  "2"
```

## 접근 방법

- replace 와 split을 적절히 사용해서 풀 수 있다.
- 핵심은 `minus`를 `plus-` 로 바꾸는 것이다.

## 내 풀이

```python
def calculate(s):
    a = s.replace('minus', 'plus-').split('plus')
    answer = 0
    for i in a:
        answer += int(i)
    return str(answer)
```

## 다른 사람 풀이

```python
def calculate(s):
    return str(sum(int(n) for n in s.replace("minus", "plus-").split("plus")))
```

## 느낀점

- 난이도가 높지 않은 문제임에도 불구하고 푸는데 상당히 오래 걸린 문제였다.

-  `minus`를 `plus-` 로 바꾸고 `plus`로 split하는 걸 왜 생각 못 했을까..
