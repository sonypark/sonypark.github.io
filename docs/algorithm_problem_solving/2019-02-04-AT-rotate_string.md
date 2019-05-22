2019년 2월 5일

# Lv1 - 문자열 회전

> 출처: [코딩인터뷰완전분석](http://www.kyobobook.co.kr/product/detailViewKor.laf?mallGb=KOR&ejkGb=KOR&barcode=9788966263080&orderClick=JAj)

## 문제
- 1.9 문자열 회전
- 한 단어가 다른 문자열에 포함되어 있는지 판별하는 `isSubstring` 이라는 매서드가 있다고 하자.
- s1과 s2의 두 문자열이 주어졌고, s2가 s1을 회전시킨 결과인지 판별하고자 한다.
- `Ex) waterbottle 은 erbottlewat 을 회전시켜 얻을 수 있는 문자열이다.`
- `isSubstring` 메서드를 한 번만 호출해서 판별할 수 잇는 코드를 작성하라.


## 풀이
```python
def isSubstring(s1: str, s2:str)->bool:

    # 문자열 길이가 다르면 False
    if(len(s1) != len(s2)):
        return False

    s1s1 = s1+s1

    if(s2 in s1s1):
        return True
    else:
        return False
```

## 배운점
- 1시간을 고민 끝에 해설을 보고 힌트를 얻었다. 
- 문자열 두 개를 연결하는 건 해설을 보지 않았으면 전혀 생각 못 했을 것 같다.


## 느낀점
- 최소 1시간은 고민하고 전혀 감이 안 잡힐 땐 해설을 보고 힌트를 얻자.