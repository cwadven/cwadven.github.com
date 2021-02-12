---
title: "[알고리즘 프로그래머스] 프린터 (LEVEL 2)"
tag:
- 프로그래머스 LEVEL2
- 알고리즘
categories:
- algorithm
---

# (문제) 프린터 [스택/큐]
---

일반적인 프린터는 인쇄 요청이 들어온 순서대로 인쇄합니다.

그렇기 때문에 중요한 문서가 나중에 인쇄될 수 있습니다.

이런 문제를 보완하기 위해 중요도가 높은 문서를 먼저 인쇄하는 프린터를 개발했습니다.

이 새롭게 개발한 프린터는 아래와 같은 방식으로 인쇄 작업을 수행합니다.

~~~
1. 인쇄 대기목록의 가장 앞에 있는 문서(J)를 대기목록에서 꺼냅니다.
2. 나머지 인쇄 대기목록에서 J보다 중요도가 높은 문서가 한 개라도 존재하면 J를 대기목록의 가장 마지막에 넣습니다.
3. 그렇지 않으면 J를 인쇄합니다.
~~~

예를 들어, 4개의 문서(A, B, C, D)가 순서대로 인쇄 대기목록에 있고 중요도가 2 1 3 2 라면 C D A B 순으로 인쇄하게 됩니다.

내가 인쇄를 요청한 문서가 몇 번째로 인쇄되는지 알고 싶습니다. 위의 예에서 C는 1번째로, A는 3번째로 인쇄됩니다.


> **입력설명**

첫번째 입력으로는 리스트가 들어옵니다, 두번째 입력으로는 위치가 들어옵니다.

현재 대기목록에는 1개 이상 100개 이하의 문서가 있습니다.

인쇄 작업의 중요도는 1~9로 표현하며 숫자가 클수록 중요하다는 뜻입니다.

location은 0 이상 (현재 대기목록에 있는 작업 수 - 1) 이하의 값을 가지며 대기목록의 가장 앞에 있으면 0, 두 번째에 있으면 1로 표현합니다.

> **출력설명**

현재 대기목록에 있는 문서의 중요도가 순서대로 담긴 배열 priorities와 내가 인쇄를 요청한 문서가 현재 대기목록의 어떤 위치에 있는지를 알려주는 location이 매개변수로 주어질 때, 내가 인쇄를 요청한 문서가 몇 번째로 인쇄되는지 return 하도록 solution 함수를 작성해주세요.

> **테스트케이스**
 

| 입력예제 | 출력예제 |
| -------- | -------- | 
| [2, 1, 3, 2] 2 | 1 | 
| [1, 1, 9, 1, 1, 1] 0 | 5 | 

예제 #1

문제에 나온 예와 같습니다.

예제 #2

6개의 문서(A, B, C, D, E, F)가 인쇄 대기목록에 있고 중요도가 1 1 9 1 1 1 이므로 C D E F A B 순으로 인쇄합니다.

---
# 해결방법

### 동작 시각화

##### 1. 리스트의 각 값에 인덱스 정보 또한 추가해서 새로운 리스트를 생성한다. 또한 빠져나온 개수를 구하기 위해 count 변수를 만든다.

![]({{ 'assets/images/algorithm/printer_prog/printer_prog1.gif' | relative_url }})<br><br>

---

##### 2. popleft를 하여 이 값이 다른 리스트 안의 값중에서 가장 큰 수가 아니면 다시 리스트 안에 넣는다.

![]({{ 'assets/images/algorithm/printer_prog/printer_prog2.gif' | relative_url }})<br><br>

![]({{ 'assets/images/algorithm/printer_prog/printer_prog3.gif' | relative_url }})<br><br>

---

##### 3. 가장 큰 수면 우선순위이기 때문에 해당 값을 버린다. 이때 count + 1을 한다.

![]({{ 'assets/images/algorithm/printer_prog/printer_prog4.gif' | relative_url }})<br><br>

---

##### 4.  이 과정을 계속 반복한다.

---
##### 5. 만약 이 값이 가지고 있는 인덱스 정보가 우리가 찾는 location과 맞다면 count + 1과 동시에 지금까지 count 한 수를 출력한다.

![]({{ 'assets/images/algorithm/printer_prog/printer_prog5.gif' | relative_url }})<br><br>


---
# 코드
```python
from collections import deque

arr = [1,1,9,1,1,1]
location = 0

arr = list(enumerate(arr))

arr = deque(arr)
cnt = 0

while True:
    w = arr.popleft()
    # 하나라도 뽑은 것 보다 리스트 안에 큰게 있다면
    if any(w[1] < x[1] for x in arr):
        arr.append(w)
    else:
        cnt = cnt + 1
        if w[0] == location:
            break

print(cnt)
```
