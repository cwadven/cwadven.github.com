---
title: "[알고리즘] 재귀함수 이용한 이진수 출력 (Recursive)"
tag:
- 재귀함수
- recursive
- 알고리즘
categories:
- algorithm
- python
---

# (문제) 재귀함수 이용한 이진수 출력
---

10진수 N이 입력되면 2진수로 변환하여 출력하는 프로그램을 작성하세요.

단 **재귀함수**를 이용해서 출력해야 합니다.

> **입력설명**

첫 번째 줄에 10진수 N(1<=N<=1,000)이 주어집니다.

> **출력설명**

첫 번째 줄에 이진수를 출력하세요.

> **테스트케이스**
 

| 입력예제 | 출력예제 |
| -------- | -------- | 
| 11 | 1011 | 
| 23 | 10111 | 
| 120 | 1111000 | 
| 360 |101101000 |

---
# 해결방법
재귀함수에 이용할 **점화식(재귀식)**을 찾는다.

**점화식 :**<br>

![]({{ 'assets/images/algorithm/recursive_2bit/recursive_2bit1.png' | relative_url }})
# 코드
```python
# 재귀함수 이용
def retrieve(x):
    if x == 0:
        return 0
    elif x == 1:
        return 1
    return str(retrieve(x//2)) + str(x%2)

n = int(input())

print(retrieve(n))
```
