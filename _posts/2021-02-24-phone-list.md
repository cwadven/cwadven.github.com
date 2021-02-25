---
title: "[알고리즘 프로그래머스] 전화번호 목록 (LEVEL 2)"
tag:
- 알고리즘
- 프로그래머스 LEVEL2
categories:
- algorithm
---

# (문제) 전화번호 목록 [해시]
---

전화번호부에 적힌 전화번호 중, 한 번호가 다른 번호의 접두어인 경우가 있는지 확인하려 합니다.

전화번호가 다음과 같을 경우, 구조대 전화번호는 영석이의 전화번호의 접두사입니다.

* 구조대 : 119
* 박준영 : 97 674 223
* 지영석 : 11 9552 4421
* 
전화번호부에 적힌 전화번호를 담은 배열 phone_book 이 solution 함수의 매개변수로 주어질 때, 어떤 번호가 다른 번호의 접두어인 경우가 있으면 false를 그렇지 않으면 true를 return 하도록 solution 함수를 작성해주세요.


> **입력설명**

phone_book의 길이는 1 이상 1,000,000 이하입니다.

각 전화번호의 길이는 1 이상 20 이하입니다.

> **출력설명**


> **테스트케이스**
 

| 입력예제 | 출력예제 |
| -------- | -------- | 
| ["119", "97674223", "1195524421"]	 | false | 
| ["123","456","789"] | true | 
| ["12","123","1235","567","88"] | false | 

---
# 해결방법

해시 방법으로 해결해야하므로 해시적으로 생각해보자.

하나의 딕셔너리를 생성한다.

이제 이 딕셔너리 안에는 phone_book의 번호가 들어갈 것이다.

반복문을 통해서 phone_book안에 있는 번호를 순회해서 접근하자.

접근을 할 때, 반복문을 이용하여 phone_book안에 고른 하나의 번호를 각 뒷자리를 하나씩 빼가면서 만든 딕셔너리 안의 key 값과 비교한다.

만약 phone_book 안의 숫자들을 이렇게 가정하자 ["119", "97674223", "1195524421"] 여기서 하나를 빼면

"119"가 나오는데 우선 딕셔너리에 119를 가지는 키 값이 있는지 확인을 한다.

없을 경우 뒷자리를 하나 빼고, 11을 키 값으로 가지고 있는지 확인한다.

이것도 없을 경우 1을 키 값으로 가지고 있는지 확인한다.

총 이 반복은 "119" 숫자의 길이 만큼 반복하고, 만약에 없을 경우 끝날 때 이 "119" 값을 키로 가지는 딕셔너리로 하나 생성한다.

나머지 모든 리스트 안에 있는 것들도 똑같이 한다.

**단!!! 이 작업을 하기 전에 phone_book은 정렬시켜 줘야한다!! 간단한 이유는 만약**

["10","1"] 이 있다고 해보자.

10 먼저 처리를 하면 일단 1이 없어서 10 안에 들어가게 된다.

그러고 1을 보면 1 자체도 딕셔너리 안에 없기 때문에 이것은 접두어라고 판단을 잘 못하는 코드가 된다!

이런 작업을 마치고 만약 끝까지 순회를 하면 True를 return 하면 된다.


---
# 코드
```python
def solution(phone_book):
    phone_book.sort()
    phone_dict = {}
    for phone in phone_book:
        for j in range(len(phone)):
            if phone_dict.get(phone[:-j]):
                return False
            else:
                phone_dict[phone] = True
    return True
```