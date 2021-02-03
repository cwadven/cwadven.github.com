---
title: "[알고리즘 프로그래머스] 완주하지 못한 선수 (LEVEL 1:해시)"
tag:
- 알고리즘
- 프로그래머스 LEVEL1
categories:
- algorithm
---

# (문제) 완주하지 못한 선수 [해시]

---

수많은 마라톤 선수들이 마라톤에 참여하였습니다. 단 한 명의 선수를 제외하고는 모든 선수가 마라톤을 완주하였습니다.

마라톤에 참여한 선수들의 이름이 담긴 배열 participant와 완주한 선수들의 이름이 담긴 배열 completion이 주어질 때, 완주하지 못한 선수의 이름을 return 하도록 solution 함수를 작성해주세요.


> **입력설명**

입력의 첫번째는 participant로 참여한 선수들의 리스트, 두번째 입력은 완주한 사람들의 이름이 들어있는 리스트이다.

마라톤 경기에 참여한 선수의 수는 1명 이상 100,000명 이하입니다.

completion의 길이는 participant의 길이보다 1 작습니다.

참가자의 이름은 1개 이상 20개 이하의 알파벳 소문자로 이루어져 있습니다.

참가자 중에는 동명이인이 있을 수 있습니다.

> **출력설명**

완주하지 못한 선수의 이름을 출력하시오.


> **테스트케이스**


| 입력예제 | 출력예제 |
| -------- | -------- | 
| ["leo", "kiki", "eden"] ["eden", "kiki"] | "leo" | 
| ["marina", "josipa", "nikola", "vinko", "filipa"] ["josipa", "filipa", "marina", "nikola"] | "vinko" | 
| ["mislav", "stanko", "mislav", "ana"] ["stanko", "ana", "mislav"] | "mislav" | 
 
 예제 #1
leo는 참여자 명단에는 있지만, 완주자 명단에는 없기 때문에 완주하지 못했습니다.

예제 #2
vinko는 참여자 명단에는 있지만, 완주자 명단에는 없기 때문에 완주하지 못했습니다.

예제 #3
mislav는 참여자 명단에는 두 명이 있지만, 완주자 명단에는 한 명밖에 없기 때문에 한명은 완주하지 못했습니다.


---
# 해결방법

> **정식 루트**

해시 이용하여 문제를 해결하는 것이므로

하나의 해시 테이블(딕셔너리)을 생성하여 participant 값 들로 해시테이블의 key를 생성하여 value 값으로는 1개만 있으면 1로 초기화 여러개가 있으면 +1 로 증가를 시켜준다.

완료 후, completion의 값을 이용하여 해시테이블에 존재하는 compleition의 값을 가지는 key의 value를 -1 씩 한다.

만약 해시테이블에 key들의 value가 0일 경우는 완주를 한 선수고, 만약 value가 0보다 클 경우는 완주를 하지 못한 것이기 때문에 value가 0 보다 클 경우 출력을 한다.

> **모듈 루트**

```python
from collection import Couter 
```

Couter라는 클래스를 이용하여 리스에 존재하는 동일한 값을 가진 것을 key 와 value의 형태인 딕셔너리로 변환 시켜, key는 값 value는 동일한 것의 횟수의 정보가 들어간다.

Couter끼리 산술 연산이 가능하며 산술 연산을 하면 동일한 key 이름을 가지는 value의 값끼리 연산을 진행 한다.

---
# 코드
```python
from collections import Counter

def solution(participant, completion):
    a1 = participant
    a2 = completion

    a = Counter(a1)
    b = Counter(a2)
    
    c = a - b
    
    for x in a2:
        if a.get(x):
            a[x] = a[x] - 1

    for key, val in a.items():
        if val > 0:
            return(key)
```
