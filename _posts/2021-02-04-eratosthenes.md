---
title: "[알고리즘] 소수(에라토스테네스 체)"
tag:
- 알고리즘
categories:
- algorithm
---

# (문제) 소수(에라토스테네스 체)
---

자연수 N이 입력되면 1부터 N까지의 소수의 개수를 출력하는 프로그램을 작성하세요.

만약 20이 입력되면 1부터 20까지의 소수는 2, 3, 5, 7, 11, 13, 17, 19로 총 8개입니다.

제한시간은 1초입니다. 

> **입력설명**

첫 줄에 자연수의 개수 N(2<=N<=200,000)이 주어집니다.


> **출력설명**

첫 줄에 소수의 개수를 출력합니다.


> **테스트케이스**
 

| 입력예제 | 출력예제 |
| -------- | -------- | 
| 20 | 8 | 
| 2 | 1 | 
| 200000 | 17984 | 
| 150000 | 13848 | 
| 90000 | 8713 | 
| 100000 | 9592 | 

---
# 해결방법

N + 1개 만큼의 0으로 초기화 된 리스트를 생성한다.<br>
(N+1 인 이유는 0부터 인덱스를 생각하지 않고 1부터 생각하기 위함)

**2중 반복문 + 초기 리스트 이용**

큰 반복문을 2에서 N+1 번 반복한다.

만약 반복문을 진행할때 그 부분이 0 이면 소수이므로 count + 1 하여 소수라고 나타내는 변수에 나타낸다.

큰 반복문 에서 받은 값을 시작으로 작은 반복문을 생성하여 그 값만큼 배수로 껑충 껑충 뛴다.

![]({{ 'assets/images/algorithm/eratos/Sieve_of_Eratosthenes_animation.gif' | relative_url }})<br><br>


그림의 경우, 11의 제곱>120 이므로 11보다 작은 수의 배수들만 지워도 충분하다.

이유는 2에서부터 배수로 확인을 한다. 그러면 2 * 1, 2 * 2, 2 * 3, 2 * 5 .... 처럼 확인을 하는데,

만약 다음 3에서 배수로 확인을 할 때, 이전에 2에서 이미 2 * 3을 했으니 3 * 3 부터 확인을 하면 된다. 3 * 3, 3 * 4, 3 * 5 ...

다음 4는 이미 2를 가지고 있는 배수여서 넘어가고 5에서는 이미 뒤에, 2, 3 을 확인 했으니 5 * 5 부터 5 * 6 ... 이런 식으로 확인하면 된다.

즉, 120보다 작거나 같은 수 가운데 2, 3, 5, 7의 배수를 지우고 남는 수는 모두 소수이다.

[나무위키 : 에라토스테너스의 체 정의 (링크)](https://ko.wikipedia.org/wiki/%EC%97%90%EB%9D%BC%ED%86%A0%EC%8A%A4%ED%85%8C%EB%84%A4%EC%8A%A4%EC%9D%98_%EC%B2%B4 "에라토스테너스의 체 링크")

---

# 코드 방법 1 (2부터 n까지의 순회)
```python
# n까지의 소수의 개수를 구하기
n = int(input())

# 에라토스테너스의 체는 리스트 하나를 생성한다
n_arr = [0] * (n + 1)
# 소수 개수 세기
count = 0

# 2~20 까지 반복 소수의 시작은 2부터 이므로
for i in range(2, n+1):
    # 소수가 아니면 1

    # 맨처음에 소수인지 확인한다 (소수 시작 2)
    # 소수는 0
    if n_arr[i] == 0:
        count = count + 1

        # 배수로 돌음
        # 해당 소수를 찾으면 그것을 이용하여 반복문을 그 소수의 배수로 돈다
        for j in range(i, n+1, i):
            # 첫번째는 빼고 다 1로
            n_arr[j] = 1

print(count)
```
# 코드 방법 2 (2부터 int(n**0.5)+1까지의 순회)

```python
# n까지의 소수의 개수를 구하기
n = int(input())

# 에라토스테너스의 체는 리스트 하나를 생성한다
n_arr = [0] * (n + 1)
count = 0

for i in range(2, int(n**0.5)+1):
    # 소수이다
    if n_arr[i] == 0:
        for j in range(i*2, n+1, i):
            # 체크를 했고, 또한 배수가 되는 것들 소수가 아니다
            n_arr[j] = 1

print(len([i for i in range(2, len(n_arr)) if n_arr[i] == False]))
```