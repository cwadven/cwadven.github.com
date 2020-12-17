---
title: "[알고리즘] 수들의 조합 (DFS)"
tag:
- dfs
- 깊이우선탐색
- 알고리즘
categories:
- algorithm
---

# (문제) 수들의 조합 (DFS)
---

N개의 정수가 주어지면 그 숫자들 중 K개를 뽑는 조합의 합이 임의의 정수 M의 배수인 개수는 몇 개가 있는지 출력하는 프로그램을 작성하세요.

예를 들면 5개의 숫자 2 4 5 8 12가 주어지고, 3개를 뽑은 조합의 합이 6의 배수인 조합을 찾으면 4+8+12 2+4+12로 2가지가 있습니다.


> **입력설명**

첫줄에 정수의 개수 N(3<=N<=20)과 임의의 정수 K(2<=K<=N)가 주어지고, 두 번째 줄에는 N개의 정수가 주어진다.

세 번째 줄에 M이 주어집니다.

> **출력설명**

총 가지수를 출력합니다.

> **테스트케이스**
 

| 입력예제 | 출력예제 |
| -------- | -------- | 
| 5 3<br>2 4 5 8 12<br>6 | 2 | 
| 7 3<br>2 4 5 8 12 7 13<br>6 | 5 | 
| 10 3<br>2 4 5 8 12 7 13 3 6 16<br>3 | 42 | 
| 12 5<br>2 4 5 8 12 7 13 1 3 16 19 22<br>7 | 114 | 
| 15 5<br>21 56 29 2 4 5 8 12 7 13 1 3 16 19 22<br>11 | 271 | 
| 20 7<br>21 56 29 2 4 5 8 12 7 13 1 3 16 19 22 42 45 67 61 33<br>15 | 5177 | 

---
# 해결방법

[참고 해결 방법 알고리즘](https://cwadven.github.io/algorithm/combination/ "참고 알고리즘")

---
# 코드

코드의 방식이 2가지 방법이 있다.

**방법1 dfs 이용**

```python
def dfs(x):
    global count
    if x == n:
        if len(ch) == m and sum(ch) % b == 0:
            count = count + 1
            # print(*ch)
        return
    else:
        ch.append(a[x])
        dfs(x+1)
        ch.pop()
        dfs(x+1)

n, m = map(int, input().split())

a = list(map (int, input().split()))

b = int(input())

count = 0
ch = []
dfs(0)
print(count)
```

**방법2 import itertools 이용**

```python
import itertools as it
n, k=map(int, input().split())
a=list(map(int, input().split()))
m=int(input())
cnt=0
# 리스트에서 3개로 이루어진 조합을 가져온다
for x in it.combinations(a, k):
    if sum(x)%m==0:
        cnt+=1
print(cnt)
```
