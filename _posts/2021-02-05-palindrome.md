---
title: "[알고리즘] 회문 문자열 검사"
tag:
- 알고리즘
categories:
- algorithm
---

# (문제) 회문 문자열 검사
---

N개의 문자열 데이터를 입력받아 앞에서 읽을 때나 뒤에서 읽을 때나 같은 경우(회문 문자열)이면 YES를 출력하고 회문 문자열이 아니면 NO를 출력하는 프로그램을 작성한다.

단 회문을 검사할 때 대소문자를 구분하지 않습니다.

> **입력설명**

첫 줄에 정수 N(1<=N<=20)이 주어지고, 그 다음 줄부터 N개의 단어가 입력된다.

각 단어의 길이는 100을 넘지 않는다.

> **출력설명**

각 줄에 해당 문자열의 결과를 YES 또는 NO로 출력한다.

> **테스트케이스**
 

| 입력예제 | 출력예제 |
| -------- | -------- | 
| 5<br>level<br>moon<br>abcba<br>soon<br>gooG | #1 YES<br>#2 NO<br>#3 YES<br>#4 NO<br>#5 YES | 
| 7<br>stts<br>moon<br>abcba<br>yes<br>goodboy<br>stttttts<br>tttttttttttttt | #1 YES<br>#2 NO<br>#3 YES<br>#4 NO<br>#5 NO<br>#6 YES<br>#7 YES | 

---
# 해결방법

반복문을 입력으로 들어오는 문자열의 길이 반절만큼 하여 앞과 뒤의 문자를 비교하면서 확인한다.

이때, 대소문자는 구분하지 않는다.

---

# 코드 방법 1
```python
n = int(input())

for i in range(n):
    # 대소문자 구분 안함
    word = input().lower()
    # 반절까지 비교
    for j in range(len(word)//2):
        # 맨 앞과 맨뒤에 비교
        # 만약 회문이 아니면 바로 끝
        if word[j] != word[len(word)-1-j]:
            print(f'#{i+1} NO')
            break
    # 반복문이 제대로 끝나면 출력
    else:
        print(f'#{i+1} YES')
```

# 코드 방법 2 (파이썬 nic 하게)
```python
n = int(input())

# 슬라이싱 이용하기
for i in range(n):
    word = input().lower()
    if word == word[::-1]:
        print(f'#{i+1} YES')
    else:
        print(f'#{i+1} NO')
```
