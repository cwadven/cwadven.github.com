---
title: "[알고리즘] 삽입 정렬"
tag:
- 알고리즘
- 중요
categories:
- algorithm
---

# (문제) 삽입 정렬
---

[8, 10, 1, 3, 2, 7, 6, 4] 를 오른차 순으로 삽입 정렬하시오.

> **입력설명**

입력으로 들어온 리스트를 정렬하시오

> **출력설명**

오름차 순으로 삽입 정렬을 하시오

> **테스트케이스**
 

| 입력예제 | 출력예제 |
| -------- | -------- | 
| [8, 10, 1, 3, 2, 7, 6, 4] | [1, 2, 3, 4, 6, 7, 8, 10] | 

---
# 해결방법

#### 1. 준비

리스트의 인덱스 1부터 시작하여 끝 인덱스까지 아래 작업을 반복을 할 것이다.

리스트 0번째 인덱스는 정렬 되어 있다고 가정을하고 시작을 하여 1번째 인덱스 부터 반복을 시작하는 것이다.

---

#### 2. 정렬 시작

각 반복으로 들어오는 인덱스는 정렬을 하려고 하는 값 key이다.

이 key를 정렬 시키기 위해서는 key 요소의 인덱스 바로 전에 있는 인덱스를 저장하는 변수 b_idx에 값을 넣는다.<br>
(key값의 인덱스-1(전에 인덱스))

```python
for i in range(1, len(arr)):
    b_idx = i - 1
    key = arr[i]
```

b_idx 번째 인덱스 요소의 값과 key 값의 크기를 비교하여 만약에 b_idx 번째 인덱스 요소의 값보다 작고 b_idx 가 0보다 작지 않을 경우

b_idx + 1 인덱스 요소에 b_idx 값을 복사한다.

그 후, 전의 b_idx - 1을 하여 그 뒤에 있는 인덱스 또한 존재한다면 즉 b_idx가 0 보다 작지 않으면  반복한다.

```python
for i in range(1, len(arr)):
    b_idx = i - 1
    key = arr[i]
    while arr[b_idx] > key and b_idx >= 0: # <---- 여기
        arr[b_idx + 1] = arr[b_idx]
        b_idx = b_idx - 1
```

만약 b_idx 번째 인덱스 요소의 값보다 key 값이 더 클 경우 key 값은 b_idx + 1 인덱스 요소에 대입한다.

```python
for i in range(1, len(arr)):
    b_idx = i - 1
    key = arr[i]
    while arr[b_idx] > key and b_idx >= 0:
        arr[b_idx + 1] = arr[b_idx]
        b_idx = b_idx - 1
    arr[b_idx + 1] = key < --- 여기
```

이 작업을 for 문이 끝날 때 까지 반복 한다.

## 동작 시각화

#### 인덱스 1 작업

![]({{ 'assets/images/algorithm/insert_sort/insert_sort1.gif' | relative_url }})<br><br>

---

#### 인덱스 2 작업

![]({{ 'assets/images/algorithm/insert_sort/insert_sort2.gif' | relative_url }})<br><br>

---

#### 인덱스 3 작업

![]({{ 'assets/images/algorithm/insert_sort/insert_sort3.gif' | relative_url }})<br><br>

---
# 코드
```python
arr = [100, 10, 50, 60, 70, 15, 1, 5, 3, 11, 10, 8, 7]

for i in range(1, len(arr)):
    b_idx = i - 1
    key = arr[i]
    while arr[b_idx] > key and b_idx >= 0:
        arr[b_idx + 1] = arr[b_idx]
        b_idx = b_idx - 1
    arr[b_idx + 1] = key

print(arr)
```
