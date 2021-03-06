---
title: "[알고리즘 프로그래머스] 자연수 뒤집어 배열로 만들기 (LEVEL 1)"
tag:
- 알고리즘
- 프로그래머스 LEVEL1
categories:
- algorithm
---

# (문제) 자연수 뒤집어 배열로 만들기

---

자연수 n을 뒤집어 각 자리 숫자를 원소로 가지는 배열 형태로 리턴해주세요.

예를들어 n이 12345이면 [5,4,3,2,1]을 리턴합니다.

> **입력설명**

n은 10,000,000,000이하인 자연수입니다.

> **출력설명**

자연수 n을 뒤집어 각 자리 숫자를 원소로 가지는 배열 형태로 리턴

> **테스트케이스**
 
| 입력예제 | 출력예제 |
| -------- | -------- | 
| 12345 | [5,4,3,2,1] | 
| 21485 | [5,8,4,1,2] | 

---
# 해결방법

### 방법 1

입력으로 들어오는 숫자를 % 10 한 값은 배열 형태로 리턴할 값에 대입을 하고, 입력으로 들어오는 숫자를 10으로 나머지 없는 연산을 하여 자기 자신을 변경한다.

이것을 입력으로 들어오는 숫자가 0이 될 때 까지 반복한다.

---
### 방법 2

입력으로 들어오는 숫자를 리스트로 변환하여 그 리스트를 뒤에서 부터 슬라이싱 하여 출력한다.

---
# 코드 방법1
```python
n = int(input())

arr = []

while n:
    arr.append(n % 10)
    n = n // 10

print(arr)
```

# 코드 방법2 (파이썬 nic)
```python
n = input()

print(list(map(int, list(n)[::-1])))
```
