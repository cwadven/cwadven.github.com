---
title: "[알고리즘] 격자판 최대합"
tag:
- 알고리즘
categories:
- algorithm
---

# (문제) 격자판 최대합
---

5 * 5 격자판에 아래롸 같이 숫자가 적혀있습니다. 

![]({{ 'assets/images/algorithm/grid_max_sum/grid_max_sum1.PNG' | relative_url }})<br><br>

N * N의 격자판이 주어지면 각 행의 합, 각 열의 합, 두 대각선의 합 중 가 장 큰 합을 출력합니다.



> **입력설명**

첫 줄에 자연수 N이 주어진다.(1<=N<=50)

두 번째 줄부터 N줄에 걸쳐 각 줄에 N개의 자연수가 주어진다.

각 자연수는 100을 넘지 않는다. 

> **출력설명**

최대합을 출력합니다.


> **테스트케이스**
 

| 입력예제 | 출력예제 |
| -------- | -------- | 
| 5<br>10 13 10 12 15<br>12 39 30 23 11<br>11 25 50 53 15<br>19 27 29 37 27<br>19 13 30 13 19 | 155 | 
| 10<br>75 79 6 72 40 72 28 43 64 19 <br>97 71 12 48 64 95 64 40 38 24 <br>52 17 58 64 13 37 38 5 30 36 <br>43 30 15 8 13 21 81 29 79 33 <br>20 4 31 24 93 60 61 19 9 88 <br>12 33 30 4 38 62 98 34 65 33 <br>37 26 6 60 82 57 49 85 66 67 <br>93 4 29 67 65 96 5 27 39 87 <br>16 52 8 7 56 19 8 53 52 93 <br>87 55 58 84 61 92 3 74 66 34  | 614 | 

---
# 해결방법

반복문을 돌려서 `가로`, `세로`, `대각선` 들의 합을 구한다.

---
# 코드
```python
n = int(input())

arr = [list(map(int, input().split())) for _ in range(n)]

_max = -2147000000
_sum = 0

for i in range(n):
    # 가로 먼저
    for j in range(n):
        _sum = _sum + arr[i][j]
    # print(_sum)
    
    if _max < _sum:
        _max = _sum
    
    _sum = 0

    # 세로
    for j in range(n):
        _sum = _sum + arr[j][i]

    if _max < _sum:
        _max = _sum
    
    _sum = 0

# 왼쪽 위에서 오른쪽 아래 대각선
for i in range(n):
    _sum = _sum + arr[i][i]

    if _max < _sum:
        _max = _sum
    
_sum = 0

# 오른쪽 위에서 왼쪽 아래 대각선
for i in range(n):
    _sum = _sum + arr[(n-1)-i][(n-1)-i]

    if _max < _sum:
        _max = _sum
    
print(_max)
```
