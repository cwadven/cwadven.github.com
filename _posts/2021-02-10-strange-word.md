---
title: "[알고리즘 프로그래머스] 이상한 문자 만들기 (LEVEL 1)"
tag:
- 알고리즘
categories:
- algorithm
---

# (문제) 이상한 문자 만들기
---

문자열 s는 한 개 이상의 단어로 구성되어 있습니다.

각 단어는 하나 이상의 공백문자로 구분되어 있습니다.

각 단어의 짝수번째 알파벳은 대문자로, 홀수번째 알파벳은 소문자로 바꾼 문자열을 리턴하는 함수, solution을 완성하세요.

> **입력설명**

입력으로는 s 의 문자열이 들어옵니다.

문자열 전체의 짝/홀수 인덱스가 아니라, 단어(공백을 기준)별로 짝/홀수 인덱스를 판단해야합니다.

첫 번째 글자는 0번째 인덱스로 보아 짝수번째 알파벳으로 처리해야 합니다.

> **출력설명**

각 단어의 짝수번째 알파벳은 대문자로, 홀수번째 알파벳은 소문자로 바꾼 문자열을 리턴하는 함수, solution을 완성

> **테스트케이스**
 

| 입력예제 | 출력예제 |
| -------- | -------- | 
| "try hello world" | TrY HeLlO WoRlD | 

---
# 해결방법

문자열을 split(" ")로 분리하여 각 단어를 순회한다.

값을 순회할 때 인덱스와 같이 순회하여 인덱스의 짝/홀 수 기준으로 문자열을 키우거나 줄인다.

대/소 문자로 변경한 단어를 리스트에 삽입한 후, 모든 것을 마쳤으면 리스트를 " ".join하여 띄어쓰기 기준으로 문자열로 만든다.

---
# 코드
```python
s = "try hello world"

answer = []

for i in s.split(" "):
    word = ""
    for idx, val in enumerate(i):
        if idx % 2 == 0:
            word = word + val.upper()
        else:
            word = word + val.lower()
    answer.append(word)
    
print(" ".join(answer))
```
