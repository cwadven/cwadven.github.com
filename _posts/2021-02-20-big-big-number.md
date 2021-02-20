---
title: "[알고리즘 프로그래머스] 큰 수 만들기 (LEVEL 2)"
tag:
- 알고리즘
- 프로그래머스 LEVEL2
categories:
- algorithm
---

# (문제) 큰 수 만들기 [탐욕법]
---

어떤 숫자에서 k개의 수를 제거했을 때 얻을 수 있는 가장 큰 숫자를 구하려 합니다.

예를 들어, 숫자 1924에서 수 두 개를 제거하면 [19, 12, 14, 92, 94, 24] 를 만들 수 있습니다.

이 중 가장 큰 숫자는 94 입니다.

문자열 형식으로 숫자 number와 제거할 수의 개수 k가 solution 함수의 매개변수로 주어집니다.

number에서 k 개의 수를 제거했을 때 만들 수 있는 수 중 가장 큰 숫자를 문자열 형태로 return 하도록 solution 함수를 완성하세요.

> **입력설명**

첫번째 입력으로는 문자열 숫자가 들어옵니다. 두번째 입력으로는 지울 개수가 들어 옵니다.

number는 1자리 이상, 1,000,000자리 이하인 숫자입니다.

k는 1 이상 number의 자릿수 미만인 자연수입니다.

> **출력설명**

number에서 k 개의 수를 제거했을 때 만들 수 있는 수 중 가장 큰 숫자를 문자열 형태로 return 하도록 solution 함수를 완성

> **테스트케이스**
 

| 입력예제 | 출력예제 |
| -------- | -------- | 
| "1924"	2	| "94" | 
| "1231234"	3 | "3234" | 
| "4177252841"	4	| "775841" |

---
# 해결방법

아래 링크를 통해 설명되어 있습니다.

[해결방법 참조 링크 : 가장 큰 수  (stack)](https://cwadven.github.io/algorithm/largest-num/)

---
# 코드
```python
from collections import deque

def solution(number, k):
    
    answer = []
    
    number = deque(number)
    
    answer.append(number.popleft())
    
    while number:
        current = number.popleft()
        while answer and answer[-1] < current and k > 0:
            k = k - 1
            answer.pop()
        answer.append(current)
    
    while k:
        k = k - 1
        answer.pop()
    
    return "".join(answer)
```
