2019년 7월 23일

# 백준 5052 - 전화번호 목록 (정렬) {docsify-ignore-all}

> 출처: https://www.acmicpc.net/problem/5052

## 문제

전화번호 목록이 주어진다. 이때, 이 목록이 일관성이 있는지 없는지를 구하는 프로그램을 작성하시오.

전화번호 목록이 일관성을 유지하려면, 한 번호가 다른 번호의 접두어인 경우가 없어야 한다.

예를 들어, 전화번호 목록이 아래와 같은 경우를 생각해보자

긴급전화: 911
상근: 97 625 999
선영: 91 12 54 26
이 경우에 선영이에게 전화를 걸 수 있는 방법이 없다. 전화기를 들고 선영이 번호의 처음 세 자리를 누르는 순간 바로 긴급전화가 걸리기 때문이다. 따라서, 이 목록은 일관성이 없는 목록이다. 

#### 입력

첫째 줄에 테스트 케이스의 개수 t가 주어진다. (1 ≤ t ≤ 50) 각 테스트 케이스의 첫째 줄에는 전화번호의 수 n이 주어진다. (1 ≤ n ≤ 10000) 다음 n개의 줄에는 목록에 포함되어 있는 전화번호가 하나씩 주어진다. 전화번호의 길이는 길어야 10자리이며, 목록에 있는 두 전화번호가 같은 경우는 없다.

#### 출력

각 테스트 케이스에 대해서, 일관성 있는 목록인 경우에는 YES, 아닌 경우에는 NO를 출력한다.

#### 예제 입력1

```
2
3
911
97625999
91125426
5
113
12340
123440
12345
98346
```

#### 예제 출력1

```
NO
YES
```

### 접근 방법

- 문자열로 정렬한 후 `startswith` 메서드로 비교한다.

## 내 풀이1 (시간 초과)

> 문자열로 정렬 했으므로 이중포문 할 필요가 없었다.

```python
import sys
t = int(input())

def valid_number(number):
    for i in range(len(number)):
        for j in range(i+1,len(number)):
            if number[j].startswith(number[i]):
                return 'NO'
    return 'YES'

for _ in range(t):
    n = int(input())
    a = []
    for _ in range(n):
        a.append(sys.stdin.readline().rstrip())
    a.sort()
    print(valid_number(a))
```

## 내 풀이2 (성공)

```python
import sys
t = int(input())

def valid_number(number):
    for i in range(1,len(number)):
        if number[i].startswith(number[i-1]):
                return 'NO'
    return 'YES'

for _ in range(t):
    n = int(input())
    a = []
    for _ in range(n):
        a.append(sys.stdin.readline().rstrip())
    a.sort()
    print(valid_number(a))
```

## 배운점

- 문자열로 정렬하면 접두어가 같은 문자는 서로 인접하여 정렬된다.

```python
a = ['134', '15', '12', '13', '1234']
```

- 위 문자열 정렬 하면 다음과 같다.

```python
>> ['12', '1234', '13', '134', '15']
```

- 따라서 이중 포문으로 모든 요소를 체크할 필요가 없다.

