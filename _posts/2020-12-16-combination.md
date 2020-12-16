---
title: "[알고리즘] 조합 구하기 (DFS)"
tag:
- dfs
- 깊이우선탐색
- 알고리즘
categories:
- algorithm
---

# 조합 구하기 (DFS)
---

1부터 N까지 번호가 적힌 구슬이 있습니다.

이 중 M개를 뽑는 방법의 수를 출력하는 프로그램을 작성하세요.


> **입력설명**

첫 번째 줄에 자연수 N(3<=N<=10)과 M(2<=M<=N) 이 주어집니다.

> **출력설명**

첫 번째 줄에 결과를 출력합니다.

맨 마지막 총 경우의 수를 출력합니다.

출력순서는 사전순으로 오름차순으로 출력합니다.

> **테스트케이스**
 

| 입력예제 | 출력예제 |
| -------- | -------- | 
| 4 2 | 1 2<br>1 3<br>1 4<br>2 3<br>2 4<br>3 4<br>6 | 
| 3 2 | 1 2<br>1 3<br>2 3<br>3 | 
| 5 3 | 1 2 3<br>1 2 4<br>1 2 5<br>1 3 4<br>1 3 5<br>1 4 5<br>2 3 4<br>2 3 5<br>2 4 5<br>3 4 5<br>10 | 

---
# 해결방법
1~n 까지의 부분집합을 구하여 append()한 리스트의 크기가 x의 깊이가 n+1까지 도착했을 경우 len이 m 인 것을 찾는다!

![]({{ 'assets/images/algorithm/combin/combin1.png' | relative_url }})<br>

[그림 그려주고 도와주신 사람 Github : Su100 프론트엔드](https://github.com/su100)

알려주셔서 감사합니다!! 😎👍👍

※ 팁 : 각 함수를 하나의 node로 봐야한다. 이전에는 1개라던지 2개라던지 헷갈렸는데, 각 함수는 다른 인스턴스 느낌이여서 각각 다른 node로 생각하는 것이 좋다! faet.Su100

---
# 코드
```python
def dfs(x):
    global count
    if x == n+1:
        if len(ch) == m:
            count = count + 1
            print(*ch)
        return
    else:
        ch.append(x)
        dfs(x+1)
        ch.pop()
        dfs(x+1)

n, m = map(int, input().split())

count = 0
ch = []
dfs(1)
print(count)
```
