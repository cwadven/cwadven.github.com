---
title: "[알고리즘] 수들의 합"
tag:
- 알고리즘
categories:
- algorithm
---

# (문제) 수들의 합
---

N개의 수로 된 수열 A[1], A[2], …, A[N] 이 있다.

이 수열의 i번째 수부터 j번째 수까지의 합 A[i]+A[i+1]+…+A[j-1]+A[j]가 M이 되는 경우의 수를 구하는 프로그램을 작성하시오.

> **입력설명**

첫째 줄에 N(1≤N≤10,000), M(1≤M≤300,000,000)이 주어진다.

다음 줄에는 A[1], A[2], …, A[N]이 공백으로 분리되어 주어진다.

각각의 A[x]는 30,000을 넘지 않는 자연수이다.


> **출력설명**

첫째 줄에 경우의 수를 출력한다.

> **테스트케이스**
 

| 입력예제 | 출력예제 |
| -------- | -------- | 
| 8 3<br>1 2 1 3 1 1 1 2 | 5 | 
| 10 5<br>3 2 2 1 3 1 2 3 2 2  | 5 | 

---
# 해결방법

어디까지 더했는지를 나타내 줄 수 있는 **lt** 와 **rt**의 변수를 만든다.

더한 값을 저장할 **total** 변수를 만든다.

lt를 이용하여 빼고, rt를 이용하여 더하고 하는 방식을 생각한다.

리스트 배열의 첫번째 인덱스의 값을 total에 대입하여 초기화 한다.

이때, total의 값이 만약에 m 보다 `작으면` 더해야하지 않은가?

더하는 것은 그 다음 인덱스 값을 더해야 하기 때문에 rt 인덱스 위치의 값을 더해야한다. 즉 rt 는 다음 위치 라는 것을 의미할 수 있다.

만약 m 보다 `클` 경우는 빼야하지 않은가? 전에 있는 정보를 빼야 하기 때문에 lt 전에 있던 위치에 있는 것을 빼는 것이다.

그렇게 반복하여 결과를 도출하는 것이다.

## 동작 시각화

처음 초기화를 리스트의 첫번째 인덱스의 값으로 total을 선언한다.

![]({{ 'assets/images/algorithm/sum_of_card/sum_of_card1.gif' | relative_url }})<br><br>

그 후 아래에 있는 것을 무한 반복 한다.

m과 비교를 하여 만약 total의 값이 m 보다 작으면 rt 인덱스의 값을 더해준다. 그리고 rt를 하나 더한다.

![]({{ 'assets/images/algorithm/sum_of_card/sum_of_card2.gif' | relative_url }})<br><br>

m과 비교를 하여 만약 total의 값이 m 과 같으면 count를 + 1 하고 rt 인덱스의 값을 더해주고, lt 인덱스의 값을 빼준다. 그 후, lt + 1 그리고 rt + 1을 해준다.

![]({{ 'assets/images/algorithm/sum_of_card/sum_of_card3.gif' | relative_url }})<br><br>

m과 비교를 하여 만약 total의 값이 m 과 같으면 count를 + 1 하고 rt 인덱스의 값을 더해주고, lt 인덱스의 값을 빼준다. 그 후, lt + 1 그리고 rt + 1을 해준다.

![]({{ 'assets/images/algorithm/sum_of_card/sum_of_card4.gif' | relative_url }})<br><br>

m과 비교를 하여 만약 total의 값이 m 보다 크면 lt 인덱스의 값을 빼준다. 그리고 lt를 하나 더한다.

![]({{ 'assets/images/algorithm/sum_of_card/sum_of_card5.gif' | relative_url }})<br><br>

m과 비교를 하여 만약 total의 값이 m 과 같으면 count를 + 1 하고 rt 인덱스의 값을 더해주고, lt 인덱스의 값을 빼준다. 그 후, lt + 1 그리고 rt + 1을 해준다.

![]({{ 'assets/images/algorithm/sum_of_card/sum_of_card6.gif' | relative_url }})<br><br>

이때, 만약 rt가 이미 개수를 넘어 버렸을 경우는 무한 반복 문을 break 한다<br>
(만약 total이 작을 경우 혹은 같을 경우, 즉 rt가 커져야 하는 경우에서 조건을 건다)

![]({{ 'assets/images/algorithm/sum_of_card/sum_of_card7.gif' | relative_url }})<br><br>

---
# 코드
```python
n, m = map(int, input().split())

arr = list(map(int, input().split()))

total = arr[0]

lt = 0
rt = 1

count = 0

while True:
    if total < m:
        if rt >= n:
            break
        total = total + arr[rt]
        rt = rt + 1
    elif total == m:
        count = count + 1
        if rt >= n:
            break
        total = total - arr[lt]
        lt = lt + 1
        total = total + arr[rt]
        rt = rt + 1
    elif total > m:
        total = total - arr[lt]
        lt = lt + 1

print(count)
```
