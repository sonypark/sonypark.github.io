
2019년 10월 29일

# codewars - Is Divisible By 6 {docsify-ignore-all}

> 출처: https://www.codewars.com/kata/simple-fun-number-258-is-divisible-by-6/train/python

## 문제

A masked number is a string that consists of digits and one asterisk (*) that should be replaced by exactly one digit. Given a masked number s, find all the possible options to replace the asterisk with a digit to produce an integer divisible by 6.


[input] string s

A masked number.

1 ≤ inputString.length ≤ 10000.

[output] a string array

Sorted array of strings representing all non-negative integers that correspond to the given mask and are divisible by 6.

## Example

```
For s = "1*0", the output should be ["120", "150", "180"].

For s = "*1", the output should be [].

For s = "1234567890123456789012345678*0",

the output should be

[
"123456789012345678901234567800",
"123456789012345678901234567830",
"123456789012345678901234567860",
"123456789012345678901234567890"]```
As you can see, the masked number may be very large
```

## 접근 방법

- `*`에 들어갈 수 있는 숫자는 `0~9`이다.
- 따라서 `*`에 `0~9` 까지의 숫자를 넣으면서 6으로 나누어 떨어지는 수만 배열에 담아 출력하면 된다.

    
## 내 풀이

```python
def is_divisible_by_6(s):
    answer = []
    for i in range(0, 10):
        a = int(s.replace('*', str(i)))
        if a % 6 == 0:
            answer.append(str(a))
    return answer
```
