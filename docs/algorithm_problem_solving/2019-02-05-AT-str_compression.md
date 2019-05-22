2019년 2월 4일

# Lv1 - 문자열 압축

> 출처: [코딩인터뷰완전분석](http://www.kyobobook.co.kr/product/detailViewKor.laf?mallGb=KOR&ejkGb=KOR&barcode=9788966263080&orderClick=JAj)

## 문제
- 1.6 문자열 압축

- 반복되는 문자의 개수를 세는 방식의 기본적인 문자열 압축 메서드를 작성하라.

- Ex) aabcccccaaa => a2b1c5a3



#### 제한사항
- 단, '압축된' 문자열의 길이가 기존 문자열의 길이보다 길다면 기존 문자열을 반환해야 한다.
  문자열은 대소문자 알파벳(a~z)으로만 이루어져 있다.



## 풀이
```python
def strCompression(string):

    new_str = ""
    count = 1

    # 첫번째 문자 넣기
    new_str += string[0]

    for n in range(len(string)-1):  # 현재 문자와 다음 문자 비교
        if (string[n] == string[n+1]): # 같다
            count +=1 # 같은 문자 수(count)
        else: # 다르다
            if count > 1: # 이전에 같은 문자가 있었다면
                new_str += str(count) # 같은 문자 수(count) 넣기
            new_str += string[n+1] # 다음 문자 넣기
            count = 1 # count 초기화

    # 마지막 문자 수(count)
    if(count>1): # 같은 문자가 있다면
        new_str += str(count) # 같은 문자 수(count) 넣기

    return new_str

```

## 배운점
- 기존의 문자열만 가지고 수정하기보다 새로운 문자열(`new_str`)을 만들어서 하는 푸는 방법