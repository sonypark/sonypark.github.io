
2019년 11월 3일

# 프로그래머스 - 기능개발 (Stack/Queue) {docsify-ignore-all}

> 출처: https://programmers.co.kr/learn/courses/30/lessons/42586

## 문제

프로그래머스 팀에서는 기능 개선 작업을 수행 중입니다. 각 기능은 진도가 100%일 때 서비스에 반영할 수 있습니다.

또, 각 기능의 개발속도는 모두 다르기 때문에 뒤에 있는 기능이 앞에 있는 기능보다 먼저 개발될 수 있고, 이때 뒤에 있는 기능은 앞에 있는 기능이 배포될 때 함께 배포됩니다.

먼저 배포되어야 하는 순서대로 작업의 진도가 적힌 정수 배열 progresses와 각 작업의 개발 속도가 적힌 정수 배열 speeds가 주어질 때 각 배포마다 몇 개의 기능이 배포되는지를 return 하도록 solution 함수를 완성하세요.

###  제한사항

- 작업의 개수(progresses, speeds배열의 길이)는 100개 이하입니다.
- 작업 진도는 100 미만의 자연수입니다.
- 작업 속도는 100 이하의 자연수입니다.
- 배포는 하루에 한 번만 할 수 있으며, 하루의 끝에 이루어진다고 가정합니다. 예를 들어 진도율이 95%인 작업의 개발 속도가 하루에 4%라면 배포는 2일 뒤에 이루어집니다.

## 입출력 예

| progresses | speeds   | return |
|------------|----------|--------|
| [93,30,55] | [1,30,5] | [2,1]  |


## 접근 방법

- prgress와 speed를 이용해 기능별 남은 작업 일수를 구해서 queue에 담는다.

- 작업 일수를 비교후 배포 일자를 구분한다.
    - 현재 기능의 작업 일수가 이전 기능의 작업 일수보다 적은 경우 이전 기능의 배포일자에 포함시킨다.
    - 현재 기능의 작업 일수가 이전 기능의 작업 일수보다 큰 경우 새로운 배포일자를 만든다.
    - 배포 일자가 나뉘는 기준은 'flag'를 넣어서 구분해준다.

문제 예시의 경우 다음과 같이 queue에 담긴다.

```
[7, 3, 'flag', 9, 'flag']
```

- queue에 담긴 요소를 'flag'를 기준으로 잘라서 각 요소의 갯수를 계산하면 된다.

## 내 풀이

```python
def solution(progresses, speeds):
    queue = []
    for i in range(len(progresses)):
        work_load = 100 - progresses[i]
        work_day = work_load // speeds[i]
        if work_load % speeds[i] != 0:
            work_day += 1
        queue.append(work_day)

    tmp = []
    tmp.append(queue[0])
    flag = queue[0]
    for j in range(1, len(queue)):
        if queue[j] > flag:
            tmp.append('flag')
            flag = queue[j]
            tmp.append(queue[j])
        else:
            tmp.append(queue[j])
    tmp.append('flag')

    count = 0
    answer = []
    for k in tmp:
        if k == 'flag':
            answer.append(count)
            count = 0
        else:
            count +=1
    return answer
```

## 다른 사람 풀이

- 현재 기능의 작업 일수가 이전 기능의 작업 일수보다 적은 경우

    - 현재 기능의 작업 일수를 이전 기능의 작업일수로 대체한다.
    - 배포 일자는 이전 기능에 맞춰야하기 때문이다.

- 위와 같이 하니 코드가 더 간결해졌다.
- 또한 math 모듈의 ceil 메서드를 이용하여 prgress와 speed를 이용해 기능별 남은 작업 일수를 계산하는 코드가 더 간단해졌다.

```python
from math import ceil

def solution(progresses, speeds):
    daysLeft = list(map(lambda x: (ceil((100 - progresses[x]) / speeds[x])), range(len(progresses))))
    count = 1
    retList = []

    for i in range(len(daysLeft))는
        try:
            if daysLeft[i] < daysLeft[i + 1]:
                retList.append(count)
                count = 1
            else:
                daysLeft[i + 1] = daysLeft[i]
                count += 1
        exept IndexError:
            retList.append(count)

    return retList
```

## 배운점

- index error의 경우 `exept IndexError`를 이용해 예외 처리할 수 있다.

