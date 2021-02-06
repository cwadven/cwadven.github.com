---
title: "[알고리즘 프로그래머스] 문자열 내 마음대로 정렬하기 (LEVEL 1)"
tag:
- 알고리즘
- 프로그래머스 LEVEL1
categories:
- algorithm
---

# (문제) 문자열 내 마음대로 정렬하기
---

문자열로 구성된 리스트 strings와, 정수 n이 주어졌을 때, 각 문자열의 인덱스 n번째 글자를 기준으로 오름차순 정렬하려 합니다.

예를 들어 strings가 ["sun", "bed", "car"]이고 n이 1이면 각 단어의 인덱스 1의 문자 "u", "e", "a"로 strings를 정렬합니다.


> **입력설명**

strings는 길이 1 이상, 50이하인 배열입니다.

strings의 원소는 소문자 알파벳으로 이루어져 있습니다.

strings의 원소는 길이 1 이상, 100이하인 문자열입니다.

모든 strings의 원소의 길이는 n보다 큽니다.

**인덱스 1의 문자가 같은 문자열이 여럿 일 경우, 사전순으로 앞선 문자열이 앞쪽에 위치합니다.**


> **출력설명**

리스트 strings와, 정수 n이 주어졌을 때, 각 문자열의 인덱스 n번째 글자를 기준으로 오름차순 정렬

인덱스 1의 문자가 같은 문자열이 여럿 일 경우, 사전순으로 앞선 문자열이 앞쪽에 위치합니다.

> **테스트케이스**
 

| 입력예제 | 출력예제 |
| -------- | -------- | 
| ["sun", "bed", "car"] 1 | ["car", "bed", "sun"] | 
| ["abce", "abcd", "cdx"] 2 | ["abcd", "abce", "cdx"] | 
| ["kind", "man", "maam", "every", "can", "canon", "cancel"] 2 | ["maam","every","can","cancel","canon","kind","man"] | 

---
# 해결방법

### 방법 1

입력으로 들어오는 `strings` 리스트를 우선 사전 정렬을 한다.

그 후, `n` 번째 인덱스의 문자를 새로운 `문자용` 리스트를 생성하여 대입한다.

`문자용` 리스트를 사전 정렬 시킨다.

그러면 `문자용` 리스트를 순회하여 `strings`에 있는 단어들 중에 `n`번째 인덱스와 `문자용` 값과 같을 경우 `정답` 리스트에 대입한다. 이때, 이미 `정답` 리스트에 해당 값이 있을 경우는 건너 뛴다.

끝나면 `정답` 리스트를 출력한다.

### 방법 2 (파이썬 정렬 중 key 를 이용하여 정렬 시키기)

`strings` 리스트를 우선 사전형으로 정렬한다.

파이썬에 있는 정렬하는 메서드에 key를 이용하여 문자 기준으로 정렬할 수 있도록 메서드를 이용하여 정답을 출력한다.

---
# 코드 방법 1
```python
def solution(strings, n):
    # 사전 순으로 우선 정렬
    # 정렬 리스트의 정렬된 위치를 저장할 인덱스
    main_arr = strings

    main_arr.sort()
    
    # 같은 것 끼리 묶어서 그 len을 구하기
    x = []
    
    for word in main_arr:
        x.append(word[n])
        
    x.sort()
    
    answer= []
    
    for i in x:
        for j in main_arr:
            if i == j[n] and not j in answer:
                answer.append(j)
    
    return answer
```


# 코드 방법 2 (파이썬 nic 하게)
```python
def solution(strings, n):
    return sorted(sorted(strings), key=lambda x: x[n])
```
