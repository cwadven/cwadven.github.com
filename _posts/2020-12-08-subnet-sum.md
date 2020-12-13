---
title: "[알고리즘] 합이 같은 부분집합 (DFS)"
tag:
- dfs
- 깊이우선탐색
- 알고리즘
categories:
- algorithm
---

# (문제) 합이 같은 부분집합 (DFS)
---

N개의 원소로 구성된 자연수 집합이 주어지면, 이 집합을 두 개의 부분집합으로 나누었을 때

두 부분집합의 원소의 합이 서로 같은 경우가 존재하면 “YES"를 출력하고, 그렇지 않으면 ”NO"를 출력하는 프로그램을 작성하세요.

둘로 나뉘는 두 부분집합은 서로소 집합이며, 두 부분집합을 합하면 입력으로 주어진 원래의 집합이 되어 합니다.

예를 들어 {1, 3, 5, 6, 7, 10}이 입력되면 {1, 3, 5, 7} = {6, 10} 으로 두 부분집합의 합이 16으로 같은 경우가 존재하는 것을 알 수 있다.


> **입력설명**

첫 번째 줄에 자연수 N(1<=N<=10)이 주어집니다.

두 번째 줄에 집합의 원소 N개가 주어진다. 각 원소는 중복되지 않는다.

> **출력설명**

첫 번째 줄에 “YES" 또는 ”NO"를 출력한다.

> **테스트케이스**
 

| 입력예제 | 출력예제 |
| -------- | -------- | 
| 6<br>1 3 5 6 7 10  | YES | 
| 6<br>2 4 5 10 12 13 | YES  | 
| 7<br>1 2 3 4 5 6 7 | YES | 
| 9<br>3 6 1 4 7 16 34 23 12 | YES | 
| 9<br>3 6 13 11 7 16 34 23 12 | NO | 
| 10<br>3 6 9 13 11 7 16 34 23 12 | YES | 

---
# 해결방법

![]({{ 'assets/images/algorithm/subnet_sum/subnet_sum1.png' | relative_url }})
<br><br>
![]({{ 'assets/images/algorithm/subnet_sum/subnet_sum2.png' | relative_url }})
<br><br>
![]({{ 'assets/images/algorithm/subnet_sum/subnet_sum3.png' | relative_url }})
<br><br>
![]({{ 'assets/images/algorithm/subnet_sum/subnet_sum4.png' | relative_url }})
<br><br>
![]({{ 'assets/images/algorithm/subnet_sum/subnet_sum5.png' | relative_url }})
<br><br>
![]({{ 'assets/images/algorithm/subnet_sum/subnet_sum6.png' | relative_url }})
<br><br>
![]({{ 'assets/images/algorithm/subnet_sum/subnet_sum7.png' | relative_url }})
<br><br>
![]({{ 'assets/images/algorithm/subnet_sum/subnet_sum8.png' | relative_url }})
<br><br>
![]({{ 'assets/images/algorithm/subnet_sum/subnet_sum9.png' | relative_url }})
<br><br>
![]({{ 'assets/images/algorithm/subnet_sum/subnet_sum10.png' | relative_url }})
<br><br>
![]({{ 'assets/images/algorithm/subnet_sum/subnet_sum11.png' | relative_url }})
<br><br>
![]({{ 'assets/images/algorithm/subnet_sum/subnet_sum12.png' | relative_url }})
<br><br>
![]({{ 'assets/images/algorithm/subnet_sum/subnet_sum13.png' | relative_url }})


---
# 코드
```python
import sys

def dfs(x, _sum):
    if _sum > total//2:
        return
    if x == n:
        if _sum == total - _sum:
            print("YES")
            # python py를 끝낸다
            sys.exit(0)
    else:
        dfs(x+1, _sum+a[x])
        dfs(x+1, _sum)

n = int(input())
a = list(map(int, input().split()))
total = sum(a)
dfs(0, 0)
print("NO")
```
