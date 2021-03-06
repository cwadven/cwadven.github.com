---
title: "[알고리즘 프로그래머스] 숫자의 표현 (LEVEL 2)"
tag:
- 알고리즘
- 프로그래머스 LEVEL2
categories:
- algorithm
---

# (문제) 숫자의 표현 (LEVEL 2)
---

Finn은 요즘 수학공부에 빠져 있습니다.

수학 공부를 하던 Finn은 자연수 n을 연속한 자연수들로 표현 하는 방법이 여러개라는 사실을 알게 되었습니다.

예를들어 15는 다음과 같이 4가지로 표현 할 수 있습니다.

* 1 + 2 + 3 + 4 + 5 = 15
* 4 + 5 + 6 = 15
* 7 + 8 = 15
* 15 = 15

자연수 n이 매개변수로 주어질 때, 연속된 자연수들로 n을 표현하는 방법의 수를 return하는 solution를 완성해주세요.


> **입력설명**

첫번째 입력으로는 n이 들어옵니다.

n은 10,000 이하의 자연수 입니다.

> **출력설명**

자연수 n이 매개변수로 주어질 때, 연속된 자연수들로 n을 표현하는 방법의 수를 return

> **테스트케이스**
 

| 입력예제 | 출력예제 |
| -------- | -------- | 
| 15 | 4 | 


---
# 해결방법

1 부터 N 까지의 수열 중 순차적으로 더했을 때, 우리가 선택한 N 까지의 개수가 몇개 있는지 확인을 하는 문제이다.

문제를 해결하기 위해서 위치를 저장해 놓는 포인팅 lt 변수와 rt 변수를 만들겠다.

lt 변수는 시작하는 인덱스 0, rt 변수는 바로 그 옆의 인덱스 1로 초기화 하겠다.

또한 개수를 알기 위해 count 변수를 0으로 초기화 하겠다.

rt가 우리가 선택한 N 보다 커지지 않을 때 까지 계속 반복할 것이다.

만약에 N 값 보다 값이 작으면 rt 를 + 1 위치를 늘릴 것이고,

만약에 N 값 보다 값이 크면 lt를 + 1 위치에 늘릴 것이다.

만약 N 값과 같을 경우는 count 에 + 1 후, lt 와 rt 둘다 + 1 위치를 늘린다.

그리고 count를 return 한다.


---
# 코드
```python
def solution(n):
    arr = list(range(1, n+1))
    
    count = 0
    
    lt = 0
    rt = 1
    
    while n >= rt:
        num = sum(arr[lt:rt+1])
        if num == n:
            count = count + 1
            lt = lt + 1
            rt = rt + 1
        elif num < n:
            rt = rt + 1
        elif num > n:
            lt = lt + 1
    
    return count
```
