---
title: "[알고리즘] 공주 구하기 (Queue)"
tag:
- queue
- 큐
- 알고리즘
categories:
- algorithm
- python
---

# (문제) 공주 구하기
---

정보 왕국의 이웃 나라 외동딸 공주가 숲속의 괴물에게 잡혀갔습니다.

정보 왕국에는 왕자가 N명이 있는데 서로 공주를 구하러 가겠다고 합니다.

정보왕국의 왕은 다음과 같은 방법으로 공주를 구하러 갈 왕자를 결정하기로 했습니다.

왕은 왕자들을 나이 순으로 1번부터 N번까지 차례로 번호를 매긴다.

그리고 1번 왕자부터 N번 왕자까지 순서대로 시계 방향으로 돌아가며 동그랗게 앉게 한다.

그리고 1번 왕자부터 시계방향으로 돌아가며 1부터 시작하여 번호를 외치게 한다.

한 왕자가 K(특정숫자)를 외치면 그 왕자는 공주를 구하러 가는데서 제외되고 원 밖으로 나오게 된다.

그리고 다음 왕자부터 다시 1부터 시작하여 번호를 외친다.

이렇게 해서 마지막까지 남은 왕자가 공주를 구하러 갈 수 있다.

![]({{ 'assets/images/algorithm/save_princess/save_princess1.PNG' | relative_url }})

예를 들어 총 8명의 왕자가 있고, 3을 외친 왕자가 제외된다고 하자.

처음에는 3번 왕자가 3을 외쳐 제외된다.

이어 6, 1, 5, 2, 8, 4번 왕자가 차례대로 제외되고 마지막까지 남게 된 7 번 왕자에게 공주를 구하러갑니다.

N과 K가 주어질 때 공주를 구하러 갈 왕자의 번호를 출력하는 프로그램을 작성하시오.

> **입력설명**
 
첫 줄에 자연수 N(5<=N<=1,000)과 K(2<=K<=9)가 주어진다.

> **출력설명**

첫 줄에 마지막 남은 왕자의 번호를 출력합니다.

> **테스트케이스**


| 입력예제 | 출력예제 |
| -------- | -------- |
| 8 3    | 7     |
| 20 3    | 20     |
| 100 3    | 91     |
| 500 8    | 494     |
| 700 9    | 212     |
| 1000 9   | 329     |

---

# 해결방법
입력 받은 예제를 통해 1 ~ `N` 까지의 숫자를 `리스트` 안에 넣고, 해당 `리스트`의 요소가 1개가 되기 전 까지 계속 `리스트` 요소의 처음 부터 시작하여 `K` 번째 요소가 아닌 것은 pop을 시켜 `리스트` 맨 뒤로 삽입하고, `K` 번째 이면 해당 요소를 pop 시켜 제거 한다.

## 동작 시각화
> **예제) 8 3**

![]({{ 'assets/images/algorithm/save_princess/save_princess2.PNG' | relative_url }})

![]({{ 'assets/images/algorithm/save_princess/save_princess3.PNG' | relative_url }})

![]({{ 'assets/images/algorithm/save_princess/save_princess4.PNG' | relative_url }})

![]({{ 'assets/images/algorithm/save_princess/save_princess5.PNG' | relative_url }})

![]({{ 'assets/images/algorithm/save_princess/save_princess6.PNG' | relative_url }})

---

# 코드
```python
n, k = map(int, input().split())

# 자료구조 큐를 만들기 위한 리스트 생성
a = [i for i in range(1, n+1)]

# 리스트의 길이가 1이 아닐 때 계속 반복
while len(a) != 1:
    # k 번을 말하는 사람을 찾기 위해서 k-1을 통해 pop을 시킨다
    for _ in range(k-1):
        a.append(a.pop(0))
    # k 번을 말하는 사람이기에 pop 시킨다
    a.pop(0)

print(a[0])
```
