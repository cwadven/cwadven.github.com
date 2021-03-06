---
title: "[알고리즘] 네트워크 선 자르기(Top-Down)"
tag:
- dfs
- 깊이우선탐색
- 알고리즘
categories:
- algorithm
---

# (문제) 네트워크 선 자르기(Top-Down)
---

현수는 네트워크 선을 1m, 2m의 길이를 갖는 선으로 자르려고 합니다.

예를 들어 4m의 네트워크 선이 주어진다면

![]({{ 'assets/images/algorithm/network_line_b/network_line_b.PNG' | relative_url }})<br><br>

의 5가지 방법을 생각할 수 있습니다. (2)와 (3)과 (4)의 경우 왼쪽을 기준으로 자르는 위치가 다르면 다른 경우로 생각한다.

그렇다면 네트워크 선의 길이가 Nm라면 몇 가지의 자르는 방법을 생각할 수 있나요?

> **입력설명**

첫째 줄은 네트워크 선의 총 길이인 자연수 N(3≤N≤45)이 주어집니다.

> **출력설명**

첫 번째 줄에 부분증가수열의 최대 길이를 출력한다.

> **테스트케이스**
 

| 입력예제 | 출력예제 |
| -------- | -------- | 
| 9 | 55 | 
| 30 | 1346269 | 
| 33 | 5702887 | 
| 40 | 165580141 | 
| 45 | 1836311903 |

---
# 해결방법

우선 기준을 1cm 와 2cm 만 된다는 가정이기 때문에, 끝에 부분을 1cm 자른다는 가정을 통해 나머지가 몇센치 남았는지 확인한다. 그리고 끝에 부분을 2cm 자른다는 가정을 통해 나머지가 몇센치 남았는지 확인한다.

그러면 그 남은 센치미터에서 구해지는 경우의 수를 더한다!

점화식을 이용해서 만든다!

f(1) = 1<br>
f(2) = 2<br>
f(n) = f(n-1) + f(n-2)

1차원 배열을 하나 만들어서 f(n-1) + f(n-2)의 값을 n번째 배열안에 넣는다.

1차원 배열안에 L위치에 값이 있을 경우, 값을 이용하여 불러오고 아닐 경우는 값을 만들어서 이용한다.

![]({{ 'assets/images/algorithm/network_line_b/network_line_b1.PNG' | relative_url }})<br>
(오른쪽의 노드의 값은 이미 왼쪽을 진행하면서 구해졌기 때문에 1차원 배열 안에 있는 것을 이용한다)<br>

그래서 전에 만든 dfs(4) 및 dfs(5) 같은 것은 1차원 배열에 이미 들어있어서 계산은 한번만 하고 나머지는 1차원 배열에 있는 값을 이용하여 구한다.

---
# 코드
```python
def DFS(L):
    # 저장한 곳에 있으면 바로 가지 컷~!
    if dy[L] > 0:
        return dy[L]
    # 1 미터일 경우는 1 return / 2 미터일 경우는 2 return
    if L == 1 or L == 2:
        return L
    else:
        # 메모 시키기
        dy[L] = DFS(L-1) + DFS(L-2)
        return dy[L]

n = int(input())
# 기억하는 테이블
# 1번 부터 사용하기 위해서 + 1
# 메모이제이션
dy = [0] * (n+1)

print(DFS(n))
```
