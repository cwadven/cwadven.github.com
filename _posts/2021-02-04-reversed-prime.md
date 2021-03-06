---
title: "[알고리즘] 뒤집은 소수"
tag:
- 알고리즘
categories:
- algorithm
---

# (문제) 뒤집은 소수
---

N개의 자연수가 입력되면 각 자연수를 뒤집은 후 그 뒤집은 수가 소수이면 그 수를 출력하는 프로그램을 작성하세요.

예를 들어 32를 뒤집으면 23이고, 23은 소수이다. 그러면 23을 출력한다.

단 910를 뒤집으면 19로 숫자화 해야 한다. 첫 자리부터의 연속된 0은 무시한다.

뒤집는 함수인 def reverse(x) 와 소수인지를 확인하는 함수 def isPrime(x)를 반드시 작성하여 프로그래밍 한다.


> **입력설명**

첫 줄에 자연수의 개수 N(3<=N<=100)이 주어지고, 그 다음 줄에 N개의 자연수가 주어진다.

각 자연수의 크기는 100,000를 넘지 않는다.


> **출력설명**

첫 줄에 뒤집은 소수를 출력합니다. 출력순서는 입력된 순서대로 출력합니다.


> **테스트케이스**
 

| 입력예제 | 출력예제 |
| -------- | -------- | 
| 5<br>32 55 62 3700 250 | 23 73 | 
| 12<br>50 91 457 52 699 170 413 54 416 97 199 33  | 5 19 71 79 991 | 

---
# 해결방법

1. 숫자를 뒤집는 코드를 생성 -> 뒤에서 부터 읽으면 된다.

2. 뒤집은 숫자를 int형으로 만들어서 앞에 0이 있는 것들을 삭제 및 숫자화 시킨다.

3. 만약 그 숫자가 소수가 아닐 경우 -> 자기 자신 전까지 반복문을 해서 나눠서 떨어지는 것이 있을 경우 그것을 출력한다.<br>
(추가 : 반복할때, 만약 반복하는 값 의 제곱이 소수인지 알려고 하는 값 보다 크면 이 값을 소수이다, 소수의 수학적 기법....)

~~~
이유 : 만약 8이라는 값이 소수인지 알아보자

2, 3, 4, 5, 6, 7 까지 확인을 해야하는데,  8의 약수는 1, 2, 4, 8 이다. 그러면 자기자신을 빼면 1, 2, 4 이다 여기서 1을 빼면 2와 4가 남는다.

그러면이 8이라는 숫자는 2의 제곱 까지만 확인 하면 된다. 만약 3의 제곱이 되면 8을 넘어가고 값이 없으니...

이해를 못하면 다른 예를 들어보겠다.

12를 예로 들어보자! 12까지의 값들은

2, 3, 4, 5, 6, 7, 8, 9, 10, 11 을 12로 나눠서 만약 나누어 떨어지는게 있으면 소수가 아니게 된다.

12의 약수는 1, 2, 3, 4, 6, 12 이다.

여기서 자기 1과 자기자신을 제외하자 -> 2, 3, 4, 6 이 남는다.

그러면 확인을 해도 3까지만 확인하면 된다. 4를 확인하면 4의 제곱을 하여 16이 12를 넘는다.

즉, 2,3 만 확인하면 이 숫자가 소수인지 아닌지를 알 수 있다는 말이 된다.
~~~

---

# 코드
```python
# 뒤집혀서 int로 만들기
def reverse(x):
    return int(x[::-1])

def isPrime(x):
    # 만약 x가 1일 경우 소수가 아님
    if x == 1:
        return False

    # 2~ 시작하여 나눠서 떨어지는게 있을 경우는 소수
    # 나 자신 전 까지
    for i in range(2, x):

        # (추가) 소수 최적의 방법 O(log N)
        if i * i > x:
            return True

        if x % i == 0:
            return False

    return True

n = int(input())

arr = list(map(reverse, input().split()))

for x in arr:
    if isPrime(x):
        print(x, end=' ')
```
