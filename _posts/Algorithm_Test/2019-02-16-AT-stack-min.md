---
layout: post
title: 스택(Stack)에 최소값 반환 함수 만들기
category: Algorithm Test

tags: [알고리즘, algorithm, python, 파이썬]
comments: true
---
> 출처: [코딩인터뷰완전분석](http://www.kyobobook.co.kr/product/detailViewKor.laf?mallGb=KOR&ejkGb=KOR&barcode=9788966263080&orderClick=JAj)

## 문제
- 3.2 스택 Min
- 기본적인 push, pop 기능이 구현된 스택에서 최소값을 반환하는 min 함수를 추가하라. 
- 단 push, pop min 연산은 모두 O(1) 시간에 동작해야 한다.


## 풀이
```python
class Stack:
    def __init__(self):
        self.items = []
        self.pre_mins = [] # 이전의 최소값을 순서대로 모아두는 리스트
        self.min = None

    def push(self, item):
        self.items.append(item)
        self.pre_mins.append(self.min)
        if self.min is None or self.min > item:
            self.min = item

    def pop(self):
        self.items.pop()
        self.min = self.pre_mins.pop()

    def peek(self):
        return self.items[-1]

    def get_min(self):
        return self.min

if __name__ == '__main__':
   stack = Stack()
   stack.push(10)
   stack.push(6)
   stack.push(8)
   stack.push(4)
   stack.push(7)
   stack.push(3)
   print(stack.min)    #3
   stack.pop()
   print(stack.peek()) #7
   print(stack.min)    #4
   stack.pop()
   print(stack.peek()) #4
   stack.pop()
   print(stack.peek()) #8
   print(stack.min)    #6

```

## 배운점
- 시간복잡도 O(1)으로 구현하기 위해서 변수를 만들었다.
- 이전의 최소값을 리스트에 순서대로 모아두면 데이터를 추가 삭제할 때마다 최소값을 업데이트 할 수 있다.