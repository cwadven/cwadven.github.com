---
title: "[알고리즘] 숫자만 추출"
tag:
- 알고리즘
categories:
- algorithm
---

# (문제) 숫자만 추출
---

문자와 숫자가 섞여있는 문자열이 주어지면 그 중 숫자만 추출하여 그 순서대로 자연수를 만듭니다.

만들어진 자연수와 그 자연수의 약수 개수를 출력합니다.

만약 “t0e0a1c2h0er”에서 숫자만 추출하면 0, 0, 1, 2, 0이고 이것을 자연수를 만들면 120이됩니다.

즉 첫 자리 0은 자연수화 할 때 무시합니다. 출력은 120를 출력하고, 다음 줄에 120의 약수의 개수를 출력하면 됩니다.

추출하여 만들어지는 자연수는 100,000,000을 넘지 않습니다.


> **입력설명**

첫 줄에 숫자가 썩인 문자열이 주어집니다. 문자열의 길이는 50을 넘지 않습니다.


> **출력설명**

첫 줄에 자연수를 출력하고, 두 번째 줄에 약수의 개수를 출력합니다.

> **테스트케이스**
 

| 입력예제 | 출력예제 |
| -------- | -------- | 
| g0en2Ts8eSoft | 28<br>6 | 
| kdk1k0kdjfkj0kkdjkfj0fkd | 1000<br>16 | 
| dkf0jkk0dkjkgjljl1kgh0ekjlkjf2lkjsklfjlkdj | 102<br>8 | 
| Akdj0Gk1djADG2SDGkdjf | 12<br>6 |
| Akdj0Gk1djADG2SDGkdj0f | 120<br>16 |


---
# 해결방법

ASCII 코드로 0은 48이므로 9 까지는 58 이므로 58보다 큰 녀석만 문자열 더해서 다른 문자열에 합친다.

구해진 숫자를 int로 형변환을 하고, 약수를 구하기 위해서 자기 자신의 반절까지 반복문을 돌려서 나누어 떨어지는 것이 있으면 count + 1을 해서 약수의 개수를 저장하는 count 변수를 증가 시킨다.

끝나면 마지막에 자기 자신까지 약수에 포함하니 count + 1을 하여 약수의 총 개수를 구한다.


---

# 코드
```python
mixed = input()
number = ""
count = 0

for word in mixed:
    # ASCII CODE 사용
    if ord(word) < 59:
        number += word

number = int(number)

# 숫자 출력
print(number)

# 약수의 개수
# 반절까지 없으면 약수 없음
for i in range(1, number//2+1):
    if number % i == 0:
        count = count + 1

# 약수들을 구하고 자기 자신 까지
print(count+1)
```
