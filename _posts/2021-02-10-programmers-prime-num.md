---
title: |-
  [알고리즘 프로그래머스] 소수 찾기
   (LEVEL 1)
tag:
- 알고리즘
- 프로그래머스 LEVEL1
- 중요
categories:
- algorithm
---

# (문제) 소수 찾기
---

1부터 입력받은 숫자 n 사이에 있는 소수의 개수를 반환하는 함수, solution을 만들어 보세요.

소수는 1과 자기 자신으로만 나누어지는 수를 의미합니다.<br>
(1은 소수가 아닙니다.)

> **입력설명**

입력으로 n이 들어옵니다

n은 2이상 1000000이하의 자연수입니다.

> **출력설명**

1부터 입력받은 숫자 n 사이에 있는 소수의 개수를 반환

> **테스트케이스**
 

| 입력예제 | 출력예제 |
| -------- | -------- | 
| 10 | 4 | 
| 5 | 3 | 

---
# 해결방법

**에라토스테네스의 체 활용**

[링크 바로가기 : 에라토스테네스의 체 활용 문제](https://cwadven.github.io/algorithm/eratosthenes/)


---
# 코드
```python
n = int(input())

arr = [0] * (n+1)

for i in range(2, int(n**0.5)+1):
    if arr[i] == 0:
        for j in range(i+i, n+1, i):
            arr[j] = 1

print(arr[2:].count(0))
```
