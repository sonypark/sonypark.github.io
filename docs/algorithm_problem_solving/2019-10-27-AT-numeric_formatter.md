
2019년 10월 27일

# codewars - Generic numeric template formatter {docsify-ignore-all}

> 출처: https://www.codewars.com/kata/generic-numeric-template-formatter/train/python

## 문제

Your goal is to create a function to format a number given a template; if the number is not present, use the digits 1234567890 to fill in the spaces.

A few rules:

the template might consist of other numbers, special characters or the like: you need to replace only alphabetical characters (both lower- and uppercase);
if the given or default string representing the number is shorter than the template, just repeat it to fill all the spaces.
A few examples:

```
numeric_formatter("xxx xxxxx xx","5465253289") == "546 52532 89"
numeric_formatter("xxx xxxxx xx") == "123 45678 90"
numeric_formatter("+555 aaaa bbbb", "18031978") == "+555 1803 1978"
numeric_formatter("+555 aaaa bbbb") == "+555 1234 5678"
numeric_formatter("xxxx yyyy zzzz") == "1234 5678 9012"
```

## 접근 방법

- template을 순회하면서 알파벳인 부분만 숫자로 대체한다.

- 숫자로 대체할 때 주어진 숫자 배열의 길이로 인덱스를 나눈 주기를 이용한다.

- 인덱스에는 template 중간에 공백이 포함되면 안되므로 새로 인덱스 변수를 만들어 계산한다. 

    
## 내 풀이

```python
def numeric_formatter(template, data='1234567890'):
    answer = ''
    idx = 0
    for i in range(len(template)):
        if template[i].isalpha():
            answer += data[idx % len(data)]
            idx +=1
        else:
            answer += template[i]
    return answer
```

## 다른 사람 풀이

> cycle 모듈 이용

```python
def numeric_formatter(template, data='1234567890'):
    data = cycle(data)
    answer = []
    for c in template:
        if c.isalpha():
            answer.append(next(data))
        else:
            answer.append(c)
    return ''.join(answer)
```

## 배운점

- `cycle` 모듈이라는건 처음 알았다. 문자열이나 리스트를 순회할 때 쓰기 좋을 것 같다.

## 느낀점

- 순환 주기 문제는 길이로 나눈 나머지를 이용하자.