---
title: "[알고리즘] 퀵정렬 (DFS 전위)"
tag:
- dfs
- 깊이우선탐색
- 알고리즘
categories:
- algorithm
---

# (문제) 퀵정렬 (DFS 전위)
---


> **입력설명**

45, 21, 23, 36, 15, 67, 11, 60, 20, 33 의 숫자를 가지는 배열을 병합 정렬 하시오!


> **출력설명**

11, 15, 20, 21, 23, 33, 36, 45, 60, 67


> **테스트케이스**
 

| 입력예제 | 출력예제 |
| -------- | -------- | 
| 45, 21, 23, 36, 15, 67, 11, 60, 20, 33 | 11, 15, 20, 21, 23, 33, 36, 45, 60, 67 | 

---
# 해결방법

## 동작 시각화


 <h3>1. 정렬할 영역의 가장 왼쪽과 오른쪽 인덱스 번호를 LT와 RT로 설정하고, 값을 비교하기 위한 PIVOT을 RT 그리고 PIVOT과 값을 비교 후, 교체하는 작업을 하기 위한 POS 위치를 지정한다.</h3>
 
 ```python
 arr = [45, 21, 23, 36, 15, 67, 11, 60, 20, 33]
 Qsort(0, len(arr)-1)
 
 # Qsort()함수
 def Qsort(LT, RT):
    if LT < RT:
        # 파티션을 하기 위해서 POS와 PIVOT을 설정
        # 분할된 영역의 시작 인덱스 LT
        # 분할된 영역 비교할 '값' RT로 우리는 기준 했다.
        POS = LT
        PIVOT = arr[RT]
 ```

![]({{ 'assets/images/algorithm/quick/quick1.gif' | relative_url }})

---

### 2. PIVOT 인덱스 위치 전까지 반복문을 돌려서 PIVOT과 그 전까지의 과정을 비교한다.

PIVOT 보다 작으면 POS 위치에 있는 값과 현재 반복문을 통해서 비교한 값의 위치를 교환하고, POS 위치를  + 1 한다.

PIVOT 보다 크면 그냥 넘어간다.

```python
def Qsort(LT, RT):
    if LT < RT:
        # ........................... #
        for i in range(LT, RT):
            # arr[i] 값이 PIVOT 값 보다 작거나 같을 경우
            if arr[i] <= PIVOT:
                # 값 교체
                arr[i], arr[POS] = arr[POS], arr[i]
                POS = POS + 1
```

![]({{ 'assets/images/algorithm/quick/quick2.gif' | relative_url }})

---

### 3. 반복문이 완료되면 POS 위치에 있는 값과 PIVOT의 값과 교체한다.

이러면 POS 기준으로 딱 파티션이 분리가 된다 (왼쪽은 작고, 오른쪽은 크고)

```python
def Qsort(LT, RT):
    if LT < RT:
        # ................ #
        # PIVOT에 있는 값과 교체를 하니 RT의 값을 교체 하는 것
        arr[POS], arr[RT] = arr[RT], arr[POS]
```

![]({{ 'assets/images/algorithm/quick/quick3.gif' | relative_url }})

---

### 4. POS 위치에서 -1 을 RT로 POS 위치에서 +1 을 LT로 하여 재귀 할 수 있도록 새로 LT와 RT를 구분 지어서 작업을 한다

(왼쪽 부분 먼저 확인)

```python
def Qsort(LT, RT):
    if LT < RT:
        # .................... #
        
        # 파티션 완료

        # DFS 사용하여 옆쪽까지 적용한다.
        Qsort(LT, POS-1) # <---- 여기 실행
        Qsort(POS, RT)
```

![]({{ 'assets/images/algorithm/quick/quick4.gif' | relative_url }})

---

### 5. 파티션으로 분리된 왼쪽 부분을 다시 위에 있는 1번을 작업을 다시한다.

```python
 def Qsort(LT, RT):
    if LT < RT:
        # 파티션을 하기 위해서 POS와 PIVOT을 설정
        # 분할된 영역의 시작 인덱스 LT
        # 분할된 영역 비교할 '값' RT로 우리는 기준 했다.
        POS = LT
        PIVOT = arr[RT]
 ```

![]({{ 'assets/images/algorithm/quick/quick5.gif' | relative_url }})

---

### 6. 파티션으로 분리된 왼쪽 부분을 다시 위에 있는 2번을 작업을 다시한다.

```python
def Qsort(LT, RT):
    if LT < RT:
        # ........................... #
        for i in range(LT, RT):
            # arr[i] 값이 PIVOT 값 보다 작거나 같을 경우
            if arr[i] <= PIVOT:
                # 값 교체
                arr[i], arr[POS] = arr[POS], arr[i]
                POS = POS + 1
```

![]({{ 'assets/images/algorithm/quick/quick6.gif' | relative_url }})

---

### 7. 파티션으로 분리된 왼쪽 부분을 다시 위에 있는 3번을 작업을 다시한다.

```python
def Qsort(LT, RT):
    if LT < RT:
        # ................ #
        # PIVOT에 있는 값과 교체를 하니 RT의 값을 교체 하는 것
        arr[POS], arr[RT] = arr[RT], arr[POS]
```

![]({{ 'assets/images/algorithm/quick/quick7.gif' | relative_url }})

---

### 8. 파티션으로 분리된 왼쪽 부분을 다시 위에 있는 4번을 작업을 다시한다.

```python
def Qsort(LT, RT):
    if LT < RT:
        # .................... #
        
        # 파티션 완료

        # DFS 사용하여 옆쪽까지 적용한다.
        Qsort(LT, POS-1) # <---- 여기 실행
        Qsort(POS, RT)
```

![]({{ 'assets/images/algorithm/quick/quick8.gif' | relative_url }})

---

### 9. 파티션으로 분리된 왼쪽 부분을 다시 위에 있는 1번을 작업을 다시한다.

```python
 def Qsort(LT, RT):
    if LT < RT:
        # 파티션을 하기 위해서 POS와 PIVOT을 설정
        # 분할된 영역의 시작 인덱스 LT
        # 분할된 영역 비교할 '값' RT로 우리는 기준 했다.
        POS = LT
        PIVOT = arr[RT]
 ```

![]({{ 'assets/images/algorithm/quick/quick9.gif' | relative_url }})

---

### 10. 파티션으로 분리된 왼쪽 부분이 2개여서 반복문을 해도 1개 밖에 없어 그대로이고 마지막으로 POS와 PIVOT과의 값 교환을 한다.

```python
def Qsort(LT, RT):
    if LT < RT:
        # .................. #
        for i in range(LT, RT):
            # arr[i] 값이 PIVOT 값 보다 작거나 같을 경우
            if arr[i] <= PIVOT:
                # 값 교체
                arr[i], arr[POS] = arr[POS], arr[i]
                POS = POS + 1
        
        # PIVOT에 있는 값과 교체를 하니 RT의 값을 교체 하는 것
        arr[POS], arr[RT] = arr[RT], arr[POS]
```

![]({{ 'assets/images/algorithm/quick/quick10.gif' | relative_url }})

---

### 11. POS 위치에서 -1 을 RT로 POS 위치에서 +1 을 LT로 하여 재귀 할 수 있도록 새로 LT와 RT를 구분 지어서 작업을 하는데, RT가 LT보다 작아져서 해당 재귀를 끝마친다.

```python
def Qsort(LT, RT):
    if LT < RT:
```

![]({{ 'assets/images/algorithm/quick/quick11.gif' | relative_url }})

---

### 12. 파티션으로 분리된 오른쪽 부분을 다시 위에 있는 1번을 작업을 다시한다.

```
def Qsort(LT, RT):
    if LT < RT:
        # .................... #
        
        # 파티션 완료

        # DFS 사용하여 옆쪽까지 적용한다.
        Qsort(LT, POS-1) # <---- 여기 끝
        Qsort(POS, RT) # <---- 여기 실행
```

![]({{ 'assets/images/algorithm/quick/quick12.gif' | relative_url }})

---

### 13. 파티션으로 분리된 오른쪽 부분이 2개여서 반복문을 해도 1개 밖에 없어 그대로이고 마지막으로 POS와 PIVOT과의 값 교환을 한다.

```python
def Qsort(LT, RT):
    if LT < RT:
        # .................. #
        for i in range(LT, RT):
            # arr[i] 값이 PIVOT 값 보다 작거나 같을 경우
            if arr[i] <= PIVOT:
                # 값 교체
                arr[i], arr[POS] = arr[POS], arr[i]
                POS = POS + 1
        
        # PIVOT에 있는 값과 교체를 하니 RT의 값을 교체 하는 것
        arr[POS], arr[RT] = arr[RT], arr[POS]
```

![]({{ 'assets/images/algorithm/quick/quick13.gif' | relative_url }})

---

### 14. POS 위치에서 -1 을 RT로 POS 위치에서 +1 을 LT로 하여 재귀 할 수 있도록 새로 LT와 RT를 구분 지어서 작업을 하는데, RT가 LT보다 작아져서 해당 재귀를 끝마친다.

```python
def Qsort(LT, RT):
    if LT < RT:
```

![]({{ 'assets/images/algorithm/quick/quick14.gif' | relative_url }})

---

### 15. 해당 작업을 완료하면 맨 처음에 분리했던 왼쪽 부분이 정렬된다.

#### 그 후, 오른쪽 부분 또한 다시 정렬할 영역의 가장 왼쪽과 오른쪽 인덱스 번호를 LT와 RT로 설정하고, 값을 비교하기 위한 PIVOT을 RT 그리고 PIVOT과 값을 비교 후, 교체하는 작업을 하기 위한 POS 위치를 지정한다.

```python
 def Qsort(LT, RT):
    if LT < RT:
        # 파티션을 하기 위해서 POS와 PIVOT을 설정
        # 분할된 영역의 시작 인덱스 LT
        # 분할된 영역 비교할 '값' RT로 우리는 기준 했다.
        POS = LT
        PIVOT = arr[RT]
 ```

![]({{ 'assets/images/algorithm/quick/quick15.gif' | relative_url }})

---

### 16. 위 작업을 재귀가 끝날 때 까지 반복하면 정렬이 된다.

---
# 코드

```python
def Qsort(LT, RT):
    if LT < RT:
        # 파티션을 하기 위해서 POS와 PIVOT을 설정
        # 분할된 영역의 시작 인덱스 LT
        # 분할된 영역 비교할 '값' RT로 우리는 기준 했다.
        POS = LT
        PIVOT = arr[RT]

        for i in range(LT, RT):
            # arr[i] 값이 PIVOT 값 보다 작거나 같을 경우
            if arr[i] <= PIVOT:
                # 값 교체
                arr[i], arr[POS] = arr[POS], arr[i]
                POS = POS + 1
        
        # PIVOT에 있는 값과 교체를 하니 RT의 값을 교체 하는 것
        arr[POS], arr[RT] = arr[RT], arr[POS]
        
        # 파티션 완료

        # DFS 사용하여 옆쪽까지 적용한다.
        Qsort(LT, POS-1)
        Qsort(POS, RT)


if __name__ == "__main__":
    arr = [45, 21, 23, 36, 15, 67, 11, 60, 20, 33]

    print("정렬 전 :", arr)
    Qsort(0, len(arr)-1)
    print("정렬 후 :", arr)
```
