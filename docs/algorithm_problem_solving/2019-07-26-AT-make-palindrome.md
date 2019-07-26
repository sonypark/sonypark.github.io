2019년 7월 26일

# 백준 1213 - 팰린드롬 만들기 (브루트 포스) {docsify-ignore-all}

> 출처: https://www.acmicpc.net/problem/1213

## 문제

임한수와 임문빈은 서로 사랑하는 사이이다.

임한수는 세상에서 팰린드롬인 문자열을 너무 좋아하기 때문에, 둘의 백일을 기념해서 임문빈은 팰린드롬을 선물해주려고 한다.

임문빈은 임한수의 영어 이름으로 팰린드롬을 만들려고 하는데, 임한수의 영어 이름의 알파벳 순서를 적절히 바꿔서 팰린드롬을 만들려고 한다.

임문빈을 도와 임한수의 영어 이름을 팰린드롬으로 바꾸는 프로그램을 작성하시오.

#### 입력

첫째 줄에 임한수의 영어 이름이 있다. 알파벳 대문자로만 된 최대 50글자이다.

#### 출력

첫째 줄에 문제의 정답을 출력한다. 만약 불가능할 때는 "I'm Sorry Hansoo"를 출력한다. 정답이 여러 개일 경우에는 사전순으로 앞서는 것을 출력한다.

#### 예제 입력

```
AABB
```

#### 예제 출력

```
ABBA
```

### 접근 방법

팰린드롬 문자열을 만드는 경우는 다음 두 가지 이다.

1. **모든 알파벳**이 **짝수개**로만 이루어져있다.
2. 혹은 **홀수개인 알파벳**이 **하나** 있다.

## 내 풀이

```python
import sys
from collections import Counter

s = sys.stdin.readline().rstrip()
c = Counter(s)

if len(s) ==1:
    print(s)
    exit()

odd_count = 0
for j in c.values():
    if j % 2 == 1: odd_count += 1

if odd_count > 1:
    print("I'm Sorry Hansoo")

else:
    temp = []
    ll = []
    if odd_count == 0:
        for k in c.items():
            ll.append(k)
        count_alphabet = sorted(ll)
        for e in count_alphabet:
            temp.append(e[0] * (e[1] // 2))
            answer = ''.join(temp)
            answer += ''.join(reversed(answer))
        print(answer)

    else:
        for k in c.items():
            ll.append(k)
        count_alphabet = sorted(ll)
        for w in count_alphabet:
            if w[1] % 2 == 1:
                odd = w[0]
                odd_to_even = w[1]-1
                count_alphabet.remove(w)
        count_alphabet.append((odd,odd_to_even))
        count_alphabet.sort()

        for e in count_alphabet:
            temp.append(e[0] * (e[1] // 2))
            answer = ''.join(temp)
            rev_answer = ''.join(reversed(answer))
        s = answer + odd + rev_answer
        print(s)
```

## 다른 사람 풀이

```python
al = "ABCDEFGHIJKLMNOPQRSTUVWXYZ"
a = input()
l = [0] * 26 # 26개 알파벳(을 담을 배열
odd_flag = 0 # 홀수 갯수
odd_idx = 0 # 홀수 갯수인 알파벳 위치
s = ""

for x in a:
    l[al.index(x)] += 1 # 각 알파벳의 갯수 담는다.

for i in range(26):
    if l[i] % 2 == 1: # 해당 알파벳 갯수가 홀수라면
        odd_flag += 1 # 홀수 갯수 +1
        odd_idx = i # 홀수 갯수인 알파벳 위치 체크

if odd_flag > 1: # 홀수 갯수 알파펫이 2개 이상이면 펠린드롬이 될 수 없다.
    print("I'm Sorry Hansoo")
else:
    if odd_flag == 1:
        l[odd_idx] -= 1 # 해당 홀수 갯수 알파벳 갯수를 하나 뺀다.

    for i in range(26):
        s += (al[i] * (l[i] // 2)) # 남은 짝수 갯수의 알파벳의 절반만 알파벳 순으로 붙인다.

print(s, end = '') # 붙인 절반의 알파벳 출력

if odd_flag == 1: # 홀수 갯수 알파벳이 1개 있는 경우
    print(al[odd_idx], end ='') # 아까 뺀 홀수 알파벳을 한 개를 가운데에 붙인다.

print("".join(list(reversed(s)))) # 나머지 짝수 갯수의 알파벳을 역순으로 붙인다.
```

## 느낀점

- 이번 문제도 어려웠다..

- 다시 봐도 내 풀이는 지저분하다..^^

- 다른 사람 풀이에 주석을 달면서 팰린드롭 만드는 과정을 좀 더 잘 이해할 수 있었다.

