---
title: "[알고리즘] 플로이드 워샬 알고리즘"
tag:
- floyd_warshall
- 플로이드 워샬
- 알고리즘
categories:
- algorithm
---

# (문제) 플로이드 워샬 알고리즘
---

N개의 도시가 주어지고, 각 도시들을 연결하는 도로와 해당 도로를 통행하는 비용이 주어질 때 모든 도시에서 모든 도시로 이동하는데 쓰이는 비용의 최소값을 구하는 프로그램을 작성하세요.

![]({{ 'assets/images/algorithm/floyd/floyd.PNG' | relative_url }})

> **입력설명**

첫 번째 줄에는 도시의 수N(N<=100)과 도로수 M(M<=200)가 주어지고, M줄에 걸쳐 도로정보와 비용(20 이하의 자연수)이 주어진다.

만약 1번 도시와 2번도시가 연결되고 그 비용이 13이면 “1 2 13”으로 주어진다. 


> **출력설명**

모든 도시에서 모든 도시로 이동하는데 드는 최소 비용을 아래와 같이 출력한다.

자기자신으로 가는 비용은 0입니다. i번 정점에서 j번 정점으로 갈 수 없을 때는 비용을 “M"으로 출력합니다.


> **테스트케이스**
 

| 입력예제 | 출력예제 |
| -------- | -------- | 
| 5 8<br>1 2 6<br>1 3 3<br>3 2 2<br>2 4 1<br>2 5 13<br>3 4 5<br>4 2 3<br>4 5 7 | 0 5 3 6 13<br>M 0 M 1 8<br>M 2 0 3 10<br>M 3 M 0 7<br>M M M M 0 | 
| 6 9<br>1 2 12<br>1 3 4<br>2 1 2<br>2 3 5<br>2 5 5<br>3 4 5<br>4 2 2<br>4 5 5<br>6 4 5 | 0 11 4 9 14 M<br>2 0 5 10 5 M<br>9 7 0 5 10 M<br>4 2 7 0 5 M<br>M M M M 0 M<br>9 7 12 5 10 0 | 
| 7 9<br>1 2 3<br>1 3 4<br>2 1 2<br>2 3 5<br>2 5 5<br>3 4 5<br>4 2 2<br>4 5 5<br>6 4 5 | 0 3 4 9 8 M M<br>2 0 5 10 5 M M<br>9 7 0 5 10 M M<br>4 2 7 0 5 M M<br>M M M M 0 M M<br>9 7 12 5 10 0 M<br>M M M M M M 0 |

---
# 해결방법

**[플로이드 워샬 알고리즘]**

그래프에서 모든 정점에서 모든 정점으로 가는 최단 거리를 알 수 있는 알고리즘<br>
(1번 정점에서 -> 2, 3, 4, 5 번 정점으로 가는 모든 최단 거리!)

1. 다이나믹 테이블은 시작노드에서 도착노드로 가므로 2차원 이어야 한다.<br>
(dt[i][y] -> i 노드에서 j 노드 까지 가는데 드는 최소 비용)
2. 냅색 알고리즘이랑 동일한 방식이다.
3. 초기화는 인접 행렬을 초기화 한다.
4. i 에서 j 로 가는데, 바로 i에서 j 까지 갈 수 있지만, 중간에 경유를 사용하여 갈 수도 있다.<br>
(예: i -> 1 -> j)<br>
(예: i -> 1 -> 2 -> j)<br>
(예: i -> 2 -> 1 -> j)
5. 처음에 경유를 해서 간다고 가정을 했을 때, 1번 노드만 경유를 해서 간다고 가정
6. 그래서 냅색이랑 비슷하다. i에서 j로 가는 기존 값과 i에서 k에서 j를 걸쳐서 가는 경우를 비교하여 작은 값을 이용한다.
(예: min(dt[i][j], dt[i][k]+dt[k][j]))
7. k를 전부 dt의 현재 직행을 하는 값들을 2차원 배열을 통해 돌아서 작은 값은 dt에 채우고 계속 반복한다. (k가 1일 경우, 2일 경우...)
8. 만약 k가 1일 경우를 2차원 배열을 통해 전부다 돌았으면 그 dt는 직행하는 방법과 1을 들리는 방법이랑 같이 있게 된다! 존재하는 값들은 최단의 방법의 값들이 저장되어있는 것이다.

이때 다음으로 k가 2를 돌 경우 기존에 바로 1로 경유하지 않고 있던 것이 2로 경유해서 가는 경우도 있지만 1 경유한 곳에서 2로 경유해서 가는 경우도 생길 것이다.<br>
i -> j<br>
i -> 1 -> j<br>
i -> 2 -> j<br>
i -> 1 -> 2 -> j<br>
이런 경우들이 dt에 적용된 최단 값이 있을 수 있다는 것이다

아래 예와 같이 가능한 이유는 i -> k -> j 의 모든 경우를 보기 때문에 2 -> 1 도 보고 1 -> 2 도 보는 것이다.<br>
(예: i -> 1 -> 2 -> j)<br>
(예: i -> 2 -> 1 -> j)<br>

그래서 모든 경우의 수를 반복하여 최단 거리를 찾는다!

**플로이드 와샬 알고리즘 중요 공식**

```python
# 플로이드 와샬 알고리즘
# 3 중 포문
# 중간에 각 들어갈 노드들
for k in range(1, n+1):
    for i in range(1, n+1):
        for j in range(1, n+1):
            dt[i][j] = min(dt[i][j], dt[i][k] + dt[k][j])
```


---
# 코드
```python
# n : 노드의 개수
# m : 연결되어 있는 것 끼리의 개수
n, m = map(int, input().split())

# 다이나믹 테이블 생성 (2차원 인접 행렬 생성)
# 5000 이 들어가는 이유는 최단 거리를 구해야하는 것이기 때문에
# 큰 값을 넣음
dt = [[5000]*(n+1) for _ in range(n+1)]

# 자기 자신에서 자기 자신으로 가는 경우는
# 0으로 초기화 하기
for i in range(1, n+1):
    dt[i][i] = 0

for i in range(m):
    # 노드 끼리의 연결 지점을 dt에 초기화
    # 한번에 직행하는 경우 초기화 (바로 시작 --> 종료 노드로 가는 경로)
    a, b, c = map(int, input().split())
    dt[a][b] = c

# 플로이드 와샬 알고리즘
# 3 중 포문
# 중간에 각 들어갈 노드들
for k in range(1, n+1):
    for i in range(1, n+1):
        for j in range(1, n+1):
            dt[i][j] = min(dt[i][j], dt[i][k] + dt[k][j])

for i in range(1, n+1):
    for j in range(1, n+1):
        if dt[i][j] == 5000:
            print('M', end=' ')
        else:
            print(dt[i][j], end=' ')
    print()
```