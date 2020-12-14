---
title: "[알고리즘] 순열 구하기 (DFS)"
tag:
- dfs
- 깊이우선탐색
- 알고리즘
categories:
- algorithm
---

# (문제) 순열 구하기 (DFS)
---

1부터 N까지 번호가 적힌 구슬이 있습니다.

이 중 M개를 뽑아 일렬로 나열하는 방법을 모두 출력합니다.

> **입력설명**

첫 번째 줄에 자연수 N(3<=N<=10)과 M(2<=M<=N) 이 주어집니다.

> **출력설명**

첫 번째 줄에 결과를 출력합니다.

맨 마지막 총 경우의 수를 출력합니다.

출력순서는 사전순으로 오름차순으로 출력합니다.

> **테스트케이스**
 

| 입력예제 | 출력예제 |
| -------- | -------- | 
| 3 2 | 1 2<br>1 3<br>2 1<br>2 3<br>3 1<br>3 2<br>6 | 
| 5 3 | 1 2 3<br>1 2 4<br>1 2 5<br>1 3 2<br>1 3 4<br>1 3 5<br>...<br>5 4 1<br>5 4 2<br>5 4 3<br>60 | 

---
# 해결방법

**해결방법 참고**<br>
[dfs 중복 순열](https://cwadven.github.io/algorithm/numbers/ "dfs 중복 순열")

순열이기 때문에 새로운 ch 라는 리스트를 생성하여 들릴 때마다 append()를 하고 나올 때는 pop()를 통해서 만약 깊이<br>즉, x가 m 개수 만큼 들어올 경우 spread operator를 이용하여 리스트 안에 있느 값을 띄운다.

그리고 동일한 것은 없어야하므로 만약 i가 ch라는 리스트에 이미 들어가 있으면 append()하지 않는다.

---
# 코드
```python
def dfs(x):
    global count
    if x == m:
        count = count + 1
        print(*ch)
    else:
        for i in range(1, n+1):
            if not i in ch:
                ch.append(i)
                dfs(x+1)
                ch.pop()
            
n, m = map(int, input().split())

count = 0
ch = []
dfs(0)

print(count)
```
