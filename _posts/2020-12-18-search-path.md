---
title: "[알고리즘] 경로 탐색(그래프 DFS)"
---

# (문제) 경로 탐색(그래프 DFS)
---

방향그래프가 주어지면 1번 정점에서 N번 정점으로 가는 모든 경로의 가지 수를 출력하는 프로그램을 작성하세요.

아래 그래프에서 1번 정점에서 5번 정점으로 가는 가지 수는

![]({{ 'assets/images/algorithm/search_path/search_path1.PNG' | relative_url }})

총 6 가지 입니다.

> **입력설명**

첫째 줄에는 정점의 수 N(2<=N<=20)와 간선의 수 M가 주어진다.

그 다음부터 M줄에 걸쳐 연결정보가 주어진다.


> **출력설명**

총 가지수를 출력한다.

> **테스트케이스**
 

| 입력예제 | 출력예제 |
| -------- | -------- | 
| 5 9<br>1 2<br>1 3<br>1 4<br>2 1<br>2 3<br>2 5<br>3 4<br>4 2<br>4 5  | 6 | 
| 7 8<br>1 2<br>2 3<br>3 4<br>4 5<br>5 6<br>6 7<br>2 4<br>3 5 | 3 | 
| 10 17<br>1 2<br>3 4<br>2 5<br>2 3<br>5 6<br>6 7<br>3 7<br>1 7<br>1 8<br>1 9<br>1 10<br>7 3<br>2 8<br>2 9<br>9 10<br>1 3<br>3 2 | 5 | 

---
# 해결방법
방향 그래프의 상호 관계를 2차원 리스트를 생성하여 각 인덱스 위치에 연결 되어 있으면 1로 아니면 0으로 초기화 한다.

맨 처음에 시작할 Node의 값을 dfs()를 돌기 전에 path라는 리스트에 Node의 수를 넣는다

> [dfs 하는 경우 생각해야 하는 것들]

~~~
1번) 가지치기 (직접 그리기)

2번) 그린 가지치기를 이용하여 "반복문" 생각

3번) 반복문 안에서 필요한 것만 가져오기 위한 "조건문" 생각

4번) dfs(v) v가 무엇이 들어갈지 가지치기를 통해서 Node에 적은 숫자를 생각

5번) 출력의 끝을 어디에 정할지 생각

6번) 출력에 끝에 무엇을 할 것인지를 생각
~~~

1. Node 가지치기를 위해 5가닥으로 갈래를 뻗는다. <br>(가지치기 for문)

2. 반복문 i를 이용해서 1~5까지 돈다. <br>(가지치기 for문)

3. 한번 방문한 노드는 다시 방문하지 못하도록 조건을 건다. <br>(if not i in path 조건문)

4. 만약 해당  dfs(i)를 호출한다. <br>(dfs(파라미터) 파라미터에 들어갈 것을 생각한다, Node의 가지치기 하면서 쓴 것을 하면 된다.)

5. 만약 dfs(v) 매개변수가 n과 같아질 경우 count를 1 더한다. 그리고 끝마친다.
## 동작 시각화

![]({{ 'assets/images/algorithm/search_path/search_path2.PNG' | relative_url }})

---
# 코드
```python
def dfs(v):
    # 종착 지점일 경우
    global count
    if v == n:
        count = count + 1
        print(path)
    else:
        # 1 : 가지치기 반복문, 2 : 조건걸기, 3 : dfs() 같에 들어갈 것 정하기
        # 가지를 뻗는다
        # 1번 부터 시작을 할 것이기 때문에 1번부터 n+1까지
        # 예) 1~n 가지
        for i in range(1, n+1):
            # i는 방문하려고 하는 노드 번호
            # 현재 노드에서 i 번째 노드로 갈 수 있냐?
            # 그리고 방문을 안 했는가
            if matrixs[v][i] == 1 and not i in path:
                # i로 방문하여 방문 했다 체크
                path.append(i)
                dfs(i)
                
                # dfs 하고 다시 뒤로 back 하는 지점
                path.pop()

n, m = map(int, input().split())

# n + 1을 하는 이유는 자체적으로 인덱스를 먼저 하기 위해서
matrixs = [[0] * (n+1) for _ in range(n+1)]
ch = [0] * (n+1)

for _ in range(m):
    start, end = map(int, input().split())
    matrixs[start][end] = 1

count = 0

# 1을 알기 위해서 처음부터 1번 노드 방문 했다
path = [1]
dfs(1)

print(count)
```
