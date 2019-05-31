2019년 5월 31일

# Lv2 - 전화번호 목록 {docsify-ignore-all}

> 출처: https://programmers.co.kr/learn/courses/30/lessons/42577

## 문제

전화번호부에 적힌 전화번호 중, 한 번호가 다른 번호의 접두어인 경우가 있는지 확인하려 합니다.
전화번호가 다음과 같을 경우, 구조대 전화번호는 영석이의 전화번호의 접두사입니다.

구조대 : 119
박준영 : 97 674 223
지영석 : 11 9552 4421
전화번호부에 적힌 전화번호를 담은 배열 phone_book 이 solution 함수의 매개변수로 주어질 때, 어떤 번호가 다른 번호의 접두어인 경우가 있으면 false를 그렇지 않으면 true를 return 하도록 solution 함수를 작성해주세요.

#### 제한사항

- phone_book의 길이는 1 이상 1,000,000 이하입니다.
- 각 전화번호의 길이는 1 이상 20 이하입니다.


## 풀이

```python
def cmp(x):
    return len(x)

def phone_book_list(phone_book):
    phone_book.sort(key=cmp)
    for i in range(0,len(phone_book)-1):
        for j in range(i+1,len(phone_book)):
            if phone_book[j].startswith(phone_book[i]):
                return False
    return True
```

## 다른 사람 풀이
```python
def solution(phone_book):
    phone_book.sort()
    for a,b in zip(phone_book, phone_book[1:]):
        if b.startswith(a):
            return False
    return True
```

## 배운점

- 문자열 정렬하면 ASCII 코드 기준으로 정렬된다.
- 정렬한 뒤에는 0~9 순서로 정렬되기 때문에 이중 포문을 쓸 필요가 없다.

## 느낀점

- 정렬하고 이중포문을 써서 비효율적인 코드르 짰다.ㅠㅠ
- 그 동안 알고리즘을 풀 때 `zip()`을 한 번도 사용하지 않았다. 앞으로는 잘 활용해보자.
