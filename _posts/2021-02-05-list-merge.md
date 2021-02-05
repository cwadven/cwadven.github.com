---
title: "[알고리즘] 두 리스트 합치기"
tag:
- 알고리즘
categories:
- algorithm
---

# (문제) 두 리스트 합치기
---

오름차순으로 정렬이 된 두 리스트가 주어지면 두 리스트를 오름차순으로 합쳐 출력하는 프로그램을 작성하세요.

> **입력설명**

첫 번째 줄에 첫 번째 리스트의 크기 N(1<=N<=100)이 주어집니다.

두 번째 줄에 N개의 리스트 원소가 오름차순으로 주어집니다.

세 번째 줄에 두 번째 리스트의 크기 M(1<=M<=100)이 주어집니다.

네 번째 줄에 M개의 리스트 원소가 오름차순으로 주어집니다.

각 리스트의 원소는 int형 변수의 크기를 넘지 않습니다.

> **출력설명**

오름차순으로 정렬된 리스트를 출력합니다.

> **테스트케이스**
 

| 입력예제 | 출력예제 |
| -------- | -------- | 
| 3<br>1 3 5<br>5<br>2 3 6 7 9 | 1 2 3 3 5 6 7 9 | 
| 10<br>1 10 27 39 50 61 65 70 93 93 <br>7<br>7 51 65 66 70 82 93  | 1 7 10 27 39 50 51 61 65 65 66 70 70 82 93 93 93 | 


---
# 해결방법

각각의 리스트를 정렬되어 있는 상태에서 합치기 위해서 정렬 시킬 공간의 `TEMP` 리스트를 만든다.

각각의 리스트의 index 0을 P1 과 P2 의 포인터 위치를 만들고, 순차적으로 값을 비교하는 형태로 한다.

만약 첫번째 리스트의 P1 인덱스의 값과 두번째 리스트의 P2 인덱스의 값중 작은 것이 있을 경우 해당 값을 `TEMP` 리스트에 삽입하고, 작았던 P1 혹은 P2를 + 1 증가 시킨다.

이것을 P1 혹은 P2 중 하나가 리스트의 인덱스를 지날 때 까지하고, 아직 와료하지 못한 P1 혹은 P2를 반복문을 통해서 끝까지 완료 시킨다.

---
# 코드 방법 1
```python
n = int(input())
arr1 = list(map(int, input().split()))

m = int(input())
arr2 = list(map(int, input().split()))

P1 = 0
P2 = 0

TEMP = []

# 큰 것 만큼만 반복
while P1 < n and P2 < m:
    if arr1[P1] < arr2[P2]:
        TEMP.append(arr1[P1])
        P1 = P1 + 1
    else:
        TEMP.append(arr2[P2])
        P2 = P2 + 1

# P1 이 끝나지 않으면
if P1 < n:
    for _ in range(P1, n):
        TEMP.append(arr1[P1])
        P1 = P1 + 1
else:
    for _ in range(P2, m):
        TEMP.append(arr2[P2])
        P2 = P2 + 1

print(*TEMP)
```


# 코드 방법 2 (파이썬 nic 하게)
```python
n = int(input())
arr1 = list(map(int, input().split()))

m = int(input())
arr2 = list(map(int, input().split()))

print(*(sorted(arr1 + arr2)))
```
