---
title: "[알고리즘] 응급실 (Queue)"
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
메디컬 병원 응급실에는 의사가 한 명밖에 없습니다.

응급실은 환자가 도착한 순서대로 진료를 합니다.

하지만 위험도가 높은 환자는 빨리 응급조치를 의사가 해야 합니다.

이런 문제를 보완하기 위해 응급실은 다음과 같은 방법으로 환자의 진료순서를 정합니다.

* 환자가 접수한 순서대로의 목록에서 제일 앞에 있는 환자목록을 꺼냅니다.
* 나머지 대기 목록에서 꺼낸 환자 보다 위험도가 높은 환자가 존재하면 대기목록 제일 뒤로 다시 넣습니다. 그렇지 않으면 진료를 받습니다.

현재 N명의 환자가 대기목록에 있습니다.

N명의 대기목록 순서의 환자 위험도가 주어지면, 대기목록상의 M번째 환자는 몇 번째로 진료를 받는지 출력하는 프로그램을 작성하세요.

대기목록상의 M번째는 대기목록의 제일 처음 환자를 0번째로 간주하여 표현한 것입니다.


> **입력설명**

첫 줄에 자연수 N(5<=N<=100)과 M(0<=M<N) 주어집니다.

두 번째 줄에 접수한 순서대로 환자의 위험도(50<=위험도<=100)가 주어집니다.

위험도는 값이 높을 수록 더 위험하다는 뜻입니다. 같은 값의 위험도가 존재할 수 있습니다.

> **출력설명**

M번째 환자의 몇 번째로 진료받는지 출력하세요.


> **테스트케이스**
 

| 입력예제 | 출력예제 |
| -------- | -------- | 
| 5 2 <br> 60 50 70 80 90 | 3     | 
| 6 0 <br>   60 60 90 60 60 60  | 5     | 
| 15 5 <br>   63 53 87 91 83 72 83 92 63 68 88 74 51 82 89   | 10     | 

---
# 해결방법
* 각 환자의 위험도의 위치를 저장하기 위해서 "인덱스"를 각 위험도에 삽입
* 출구에 가장 가까운 환자를 꺼내 해당 위험도가 다른 위험도 보다 클 경우 해당 환자를 pop 시키고 `cnt`를 1 더한다.
* 만약 다른 위험도 보다 작을 경우 해당 환자를 pop 시킨 후, pop 한  환자를 `리스트` 입구에 삽입 시킨다.
* 해당 작업은 환자의 인덱스 정보가 입력의 m 정보와 같고, pop 시킨 환자가 가장 큰 값일 경우 반복을 종료 시킨다.
## 동작 시각화

> 예제 ) <br>
> 6 0 <br> 60 60 90 60 60 60

![]({{ 'assets/images/algorithm/emergency/emergency1.png' | relative_url }})

![]({{ 'assets/images/algorithm/emergency/emergency2.png' | relative_url }})

![]({{ 'assets/images/algorithm/emergency/emergency3.png' | relative_url }})

![]({{ 'assets/images/algorithm/emergency/emergency4.png' | relative_url }})

![]({{ 'assets/images/algorithm/emergency/emergency5.png' | relative_url }})

![]({{ 'assets/images/algorithm/emergency/emergency6.png' | relative_url }})

![]({{ 'assets/images/algorithm/emergency/emergency7.png' | relative_url }})

![]({{ 'assets/images/algorithm/emergency/emergency8.png' | relative_url }})

---
# 코드
```python
n, m = map(int, input().split())

# 환자의 위치를 인덱스화하여 비교하기 위해
patients = [(pos, val) for pos, val in enumerate(list(map(int, input().split())))]

cnt = 0

while True:
    cur = patients.pop(0)
    # any는 안의 값중에서 1개라도 참일 경우 참!
    if any(cur[1]<x[1] for x in patients):
        patients.append(cur)
    else:
        cnt = cnt + 1
        if m == cur[0]:
            break

print(cnt)
```
