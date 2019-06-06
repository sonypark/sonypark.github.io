2019년 5월 8일

# 소인수분해 {docsify-ignore-all}

> 개인적으로 공부한 과정을 정리해 놓은 글입니다. 내용 상 오류가 있을 수 있습니다. 잘못된 부분이 있을 경우 댓글에 남겨주시면 감사하겠습니다 :)
>
> 참고: https://www.acmicpc.net/problem/status/11653

## 정의
**합성수를 소수의 곱으로 나타내는 방법**을 말한다.

### 다양한 풀이법
___

## Method #1

```python
def decompose_fractions(n):
    for x in range(2, n + 1):
        count = 0    # 인수가 곱해진 횟수
        while n % x == 0:
            count += 1
            n /= x
        if count != 0:
            for i in range(count):
                print ("%d" % x)
```

## Method #2

```python
for i in range(2, int(n**0.5)+1):
    while n % i == 0:
        n = n // i
        print(i)
if n > 1:
    print(n)
```