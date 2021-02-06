---
title: "[알고리즘 프로그래머스] 문자열 다루기 기본 (LEVEL 1)"
tag:
- 알고리즘
- 프로그래머스 LEVEL1
categories:
- algorithm
---

# (문제) 문자열 다루기 기본
---

문자열 s의 길이가 4 혹은 6이고, 숫자로만 구성돼있는지 확인해주는 함수, solution을 완성하세요.

예를 들어 s가 a234이면 False를 리턴하고 1234라면 True를 리턴하면 됩니다.

> **입력설명**

s는 길이 1 이상, 길이 8 이하인 문자열입니다.

> **출력설명**

문자열 s의 길이가 4 혹은 6이고

숫자로만 구성돼있으면 함수가 True를 리턴하면 됩니다.

아니면 False를 리턴.

> **테스트케이스**
 

| 입력예제 | 출력예제 |
| -------- | -------- | 
| a234 | false | 
| 1234 | true | 
| 15975 | false | 
| af1923fa | false |

---
# 해결방법

우선 문자가 4글자 혹은 6글자 인지 판단을 한다.

그리고 그 문자가 4글자 혹은 6글자가 맞다면, ASCII 코드의 48 --> 숫자 0 ~ 58 --> 9 를 나타내므로 문자를 순회하여 한 글자가 해당 ASCII 코드 값 안에 포함이 되는지 비교하여 맞으면 계속 순회하고 아니면 False를 반환한다.

정상적으로 끝나면 True를 반환한다.

---
# 코드
```python
def solution(s):
    if len(s) == 4 or len(s) == 6:
        pass
    else:
        return False
    
    for i in s:
        if 48 <= ord(i) <= 58:
            pass
        else:
            return False
    else:
        return True
```
