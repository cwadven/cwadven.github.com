---
title: "[알고리즘 프로그래머스] 두 정수 사이의 합 (LEVEL 1)"
tag:
- 알고리즘
- 프로그래머스 LEVEL1
categories:
- algorithm
---

# (문제) 두 정수 사이의 합
---

두 정수 a, b가 주어졌을 때 a와 b 사이에 속한 모든 정수의 합을 리턴하는 함수, solution을 완성하세요.

예를 들어 a = 3, b = 5인 경우, 3 + 4 + 5 = 12이므로 12를 리턴합니다.


> **입력설명**

입력으로는 a 와 b 가 들어옵니다.

a와 b가 같은 경우는 둘 중 아무 수나 리턴하세요.

a와 b는 -10,000,000 이상 10,000,000 이하인 정수입니다.

a와 b의 대소관계는 정해져있지 않습니다.


> **출력설명**


a와 b 사이에 속한 모든 정수의 합을 리턴하는 함수, solution을 완성


> **테스트케이스**
 

| 입력예제 | 출력예제 |
| -------- | -------- | 
| 3	5 | 	12 | 
| 3	3 | 3 | 
| 5	3 | 12 | 

---
# 해결방법

### 방법1 (range 반복문으로 더하기)

`a`와 `b` 중 큰 값을 찾아서 반복문으로 작은 값부터 큰 값 까지를 더한다.



### 방법2 (인수분해 사용)

일정한 수열의 특징을 이용한다.

만약 3 ~ 5 까지의 연속된 수들의 합을 구하려면

1 ~ 2 까지 그리고 1 ~ 5 까지의 수열 2개에서 `(큰 값 수열) - (작은 값 수열)`을 한다.<br>
(입력 받은 수 중 작은 값은 -1 한 수열이다)

5 : 5 4 3 ~~2 1~~<br>
2 :             ~~2 1~~

그러면 위 같이 원하는 수열의 값들을 얻을 수 있다.

그러면 수열을 전부다 더하는 공식을 이용하여 생각을 해보자!

![]({{ 'assets/images/algorithm/two_decimal/two_decimal.PNG' | relative_url }})<br><br>

그러고 위의 식을 대입하여 생각을 해보자.<br>
(b 가 큰 수라고 생각하고 a는 이미 입력으로 받은 값 중 작은 값은데  -1 했다고 가정을 하자)

![]({{ 'assets/images/algorithm/two_decimal/two_decimal1.PNG' | relative_url }})<br><br>

![]({{ 'assets/images/algorithm/two_decimal/two_decimal2.PNG' | relative_url }})<br><br>

![]({{ 'assets/images/algorithm/two_decimal/two_decimal3.PNG' | relative_url }})<br><br>

**인수분해**

![]({{ 'assets/images/algorithm/two_decimal/two_decimal4.PNG' | relative_url }})<br><br>

![]({{ 'assets/images/algorithm/two_decimal/two_decimal5.PNG' | relative_url }})<br><br>

![]({{ 'assets/images/algorithm/two_decimal/two_decimal6.PNG' | relative_url }})<br><br>

이렇게 우리는 a 와 b 만으로 수식을 구해 코드를 만들 수 있다.

```python
(b-a)*(a+b+1)//2
```


---
# 코드 방법 1
```python
def solution(a, b):
    return sum(range(min([a,b]),max([a+1,b+1])))
```

# 코드 방법 2
```python
def solution(a, b):
    if a > b:
        a, b = b, a
    a = a - 1
    return (b-a)*(a+b+1)//2
```
