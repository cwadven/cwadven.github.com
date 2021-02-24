---
title: "[알고리즘 프로그래머스] 타겟넘버 (LEVEL 2)"
tag:
- 알고리즘
- 깊이우선탐색
- dfs
- 프로그래머스 LEVEL2
categories:
- algorithm
---

# (문제) 타겟넘버 [DFS]
---

n개의 음이 아닌 정수가 있습니다.

이 수를 적절히 더하거나 빼서 타겟 넘버를 만들려고 합니다.

예를 들어 [1, 1, 1, 1, 1]로 숫자 3을 만들려면 다음 다섯 방법을 쓸 수 있습니다.

![]({{ 'assets/images/algorithm/target_num/target_num1.PNG' | relative_url }})<br><br>

사용할 수 있는 숫자가 담긴 배열 numbers, 타겟 넘버 target이 매개변수로 주어질 때 숫자를 적절히 더하고 빼서 타겟 넘버를 만드는 방법의 수를 return 하도록 solution 함수를 작성해주세요.

> **입력설명**

첫번째 입력으로는 숫자 리스트가 들어오고, 두번째 입력으로는 만들 숫자가 들어옵니다.

주어지는 숫자의 개수는 2개 이상 20개 이하입니다.

각 숫자는 1 이상 50 이하인 자연수입니다.

타겟 넘버는 1 이상 1000 이하인 자연수입니다.

> **출력설명**

사용할 수 있는 숫자가 담긴 배열 numbers, 타겟 넘버 target이 매개변수로 주어질 때 숫자를 적절히 더하고 빼서 타겟 넘버를 만드는 방법의 수를 return

> **테스트케이스**
 

| 입력예제 | 출력예제 |
| -------- | -------- | 
| [1, 1, 1, 1, 1]	3 | 5 | 


---
# 해결방법

깊이 우선 탐색을 이용해서 문제를 해결해야한다.

![]({{ 'assets/images/algorithm/target_num/target_num2.PNG' | relative_url }})<br><br>

위의 그림 처럼 2갈래 + (더하기) 혹은 - (빼기)로 분기가 나뉜다는 것을 나타낼 수 있다.

분기가 2개로만 나눠진 다면 재귀함수가 안에 들어가는 경우가 총 2번이 된다.

```python
def dfs(L, _sum):
        if L > len(numbers) - 1:
            # 어떤 조건
        else:
            dfs(L+1, _sum+numbers[L])
            dfs(L+1, _sum-numbers[L])
```

dfs를 풀 때, 분기와 계층을 생각하면서 풀어보자!

계층은 L 이라고 생각하고, dfs 함수의 개수는 한 계층이 만들 수 있는 분기가 된다.

그래서 L 이 6번 째 반복하는 순간, 더한 값을 검사하여 만약에 target 값과 같으면 count를 한다.

```
def dfs(L, _sum):
        nonlocal count
        if L > len(numbers) - 1:
            if _sum == target:
                count = count + 1
        else:
            dfs(L+1, _sum+numbers[L])
            dfs(L+1, _sum-numbers[L])
```

---
# 코드
```python
def solution(numbers, target):
    count = 0
    def dfs(L, _sum):
        nonlocal count
        if L > len(numbers) - 1:
            if _sum == target:
                count = count + 1
        else:
            dfs(L+1, _sum+numbers[L])
            dfs(L+1, _sum-numbers[L])
    
    dfs(0, 0)
    
    return count
```
