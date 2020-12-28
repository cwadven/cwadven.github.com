---
title: "[알고리즘] 동전 분배하기(DFS)"
tag:
- dfs
- 깊이우선탐색
- 알고리즘
categories:
- algorithm
---

# (문제) 동전 분배하기(DFS)
---

N개의 동전을 A, B, C 세명에게 나누어 주려고 합니다.

세 명에게 동전을 적절히 나누어 주어, 세 명이 받은 각각의 총액을 계산해, 총액이 가장 큰 사람과 가장 작은 사람의 차가 최소가 되도록 해보세요.

단 세 사람의 총액은 서로 달라야 합니다.


> **입력설명**

첫째 줄에는 동전의 개수 N(3<=N<=12)이 주어집니다.

그 다음 N줄에 걸쳐 각 동전의 금액이 주어집니다.

> **출력설명**

총액이 가장 큰 사람과 가장 작은 사람의 최소차를 출력하세요.

> **테스트케이스**
 

| 입력예제 | 출력예제 |
| -------- | -------- | 
| 7<br>8<br>9<br>11<br>12<br>23<br>15<br>17 | 5 | 
| 5<br>300<br>10<br>10<br>10<br>10 | 290 | 
| 7<br>1<br>2<br>3<br>4<br>5<br>6<br>7 | 3 | 
| 10<br>21<br>34<br>12<br>56<br>7<br>8<br>89<br>120<br>55<br>77<br> | 5 | 

---
# 해결방법

ABC라는 리스트를 생성하여 A, B, C 구간을 각각 인덱스 0, 1, 2 로 나눴다.

생각을 해보니 A에 우선 : 8 + 9 + 11 + 12 + 23 .... / B에 0 / C 에 0 순으로 해야한다는 것을 깨닳았다.

그러면 DFS(L)에 있는 L을 이용해서 ABC라는 리스트에 반복문 i를 통해 접근하고 L은 숫자들이 들어있는 nums 인덱스에 접근해서 하나씩 더하고 또는 더하지 않고를 반복하면 되겠다라는 생각에 완성을 해보니 되었다....

---
# 코드
```python
def DFS(L):
    global diff
    if L == n:
        if diff > max(ABC) - min(ABC):
            # ABC 전체가 달라야한다
            if len(set(ABC)) == 3:
                # print(ABC)
                diff = max(ABC) - min(ABC)
    else:
        for i in range(3):
            ABC[i] = ABC[i] + nums[L]
            DFS(L+1)
            ABC[i] = ABC[i] - nums[L]

n = int(input())

nums = [int(input()) for _ in range(n)]

ABC = [0] * 3

diff = 2174000000

DFS(0)

print(diff)
```
