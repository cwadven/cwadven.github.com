---
title: "[알고리즘] 가장 큰 수 (Stack)"
tag:
- 알고리즘
- stack
- 스택
categories:
- algorithm
---

[stack]
# (문제) 가장 큰 수
---
선생님은 현수에게 숫자 하나를 주고, 해당 숫자의 자릿수들 중 m개의 숫자를 제거하여 가장 큰 수를 만들라고 했다.

만약 5276823 이 주어지고 3개의 자릿수를 제거한다면 7823이 가장 큰 숫자가 된다.
(단, 숫자의 순서는 유지해야 한다)

> **입력설명 :**

첫째 줄에 숫자(길이는 1000을 넘지 않는다)와 제거해야 할 자릿수의 개수가 주어진다.

> **출력설명 :**

가장 큰 수를 출력한다.

> **테스트 케이스**

| 입력 예제 | 출력 예제 |
| -------- | -------- |
| 5276823,3     | 7823   |
| 9977252641,5    | 99776    |
| 948096783986983,5    | 9983986983    |
| 84836543798739827589237689348957893758937689437896743489673489673986,30    | 99999978937689437896743489673489673986    |
| 123456789,6    | 789    |
| 987654321,3    | 987654    |

(입력 예제의 앞의 값은 숫자, 뒤의 값은 제거해야할 숫자 개수)

---
# 해결 방법
* 숫자를 문자화 시켜서 각 자릿수를 리스트 `num` 요소로 넣는다. (넣을 때, 다시 숫자로 변경)
* 제거할 숫자를 판별하기 위한 `stack` 리스트를 생성한다.
* `num` 의 요소를 통해서 `stack` 제거 및 삽입할 숫자를 판별한다.
* 반복문을 통해 `num` 값을 `stack`의 요소와 비교한다.
*  `stack`에 값이 있고, `m`이 0보다 크고, `stack`의 마지막 요소가 `num` 요소의 값보다 작을 경우 `stack`의 요소를 삭제
*  아닐 경우 `stack`에 `num`요소의 값을 삽입. 
* 위의 작업을 반복한다.
* `num` 요소의 반복문이 끝날 때 까지 반복한다.

( 예외 : `m`이 0이 되지 않았을 경우, stack의 마지막 부분을 `m`만큼 자른다 )
## 동작 시각화

![]({{ 'assets/images/algorithm/most_largest/most_largest1.png' | relative_url }})
![]({{ 'assets/images/algorithm/most_largest/most_largest2.png' | relative_url }})
![]({{ 'assets/images/algorithm/most_largest/most_largest3.png' | relative_url }})
![]({{ 'assets/images/algorithm/most_largest/most_largest4.png' | relative_url }})
![]({{ 'assets/images/algorithm/most_largest/most_largest5.png' | relative_url }})
![]({{ 'assets/images/algorithm/most_largest/most_largest6.png' | relative_url }})
![]({{ 'assets/images/algorithm/most_largest/most_largest7.png' | relative_url }})
# 코드
```python
num, m = map(int, input().split(',')) # 입력값을 숫자로 입력 받는다
num = list(map(int, str(num))) # num의 리스트를 만들기 위해서 각 자리수를 리스트의 요소로 만든다
stack = [] # 빈 stack 리스트를 만든다

for x in num: # 각 요소를 전부 순회하기 위해서 num 리스트를 반복문으로 돌린다
    while stack and m > 0 and stack[-1] < x: 
		# stack에 값이 있고, m(삭제할 개수)가 0 보다 크고, stack의 마지막 값이 num의 요소보다 작을 경우
		# stack의 요소를 제거한다.
        stack.pop()
        m -= 1 # 제거를 하면 삭제할 개수가 -1이 된다
    stack.append(x) # 해당 조건에 만족하지 않을 경우 stack에 num요소를 삽입
		
if m != 0: # 끝났음에도 불구하고 m이 0이 아닐 경우
    stack=stack[:-m] # 남은 m 개수만큼 stack의 마지막 부분을 자른다
		
res=''.join(map(str, stack)) # 해당 리스트를 join을 이용하여 문자열로 변환한다

print(res) # 출력한다
```
