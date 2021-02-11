---
title: "[알고리즘] 병합정렬 (DFS 후위)"
tag:
- 알고리즘
- dfs
- 깊이우선탐색
- 중요
categories:
- algorithm
---

# (문제) 병합정렬 (DFS 후위)
---


> **입력설명**

23, 11, 45, 36, 15, 67, 33, 21 의 숫자를 가지는 배열을 병합 정렬 하시오!


> **출력설명**

11, 15, 21, 23, 33, 36, 45, 67


> **테스트케이스**
 

| 입력예제 | 출력예제 |
| -------- | -------- | 
| 23, 11, 45, 36, 15, 67, 33, 21 | 11, 15, 21, 23, 33, 36, 45, 67 | 


---
# 해결방법
## 동작 시각화

### 1. 리스트의 맨왼쪽에는 LT와 맨 오른쪽에 RT를 잡는다.

```python
arr = [23, 11, 45, 36, 15, 67, 33, 21]
Dsort(0, len(arr)-1)
```

![]({{ 'assets/images/algorithm/merge/merge1.gif' | relative_url }})

---

### 2. 자신의 리스트 영역을 반으로 나누기 위해서 중앙의 값을 구하기 위해 (LT + RT) // 2 = mid 를 구한다.

```python
def Dsort(LT, RT):
    # 만약 LT가 RT보다 크거나 같을 경우
    if LT < RT:
        # 중앙 위치 찾기
        MID = (LT + RT) // 2
```

![]({{ 'assets/images/algorithm/merge/merge2.gif' | relative_url }})

---

### 3. 구한 MID 기준으로 반으로 나눠서 나눠진 부분의 양 끝부분을 MID 부분이였던 곳을 LT, RT로 바꾼다.

```python
def Dsort(LT, RT):
        # ..............#
        # 반으로 가른다
        Dsort(LT, MID) # <--- 여기 실행
        Dsort(MID + 1, RT)
```

![]({{ 'assets/images/algorithm/merge/merge3.gif' | relative_url }})

---

### 4. 반으로 나눠서 나눠진 부분 중 한쪽을 다시 리스트 영역을 반으로 나누기 위해서 중앙의 값을 구하기 위해 (LT + RT) // 2 = mid 를 구한다.

```python
# 재귀로 반복 한다 !!!!
def Dsort(LT, RT):
    # 만약 LT가 RT보다 크거나 같을 경우
    if LT < RT:
        # 중앙 위치 찾기
        MID = (LT + RT) // 2
```

![]({{ 'assets/images/algorithm/merge/merge4.gif' | relative_url }})

---


### 5. 구한 MID 기준으로 반으로 나눠서 나눠진 부분의 양 끝부분을 MID 부분이였던 곳을 또 LT, RT로 바꾼다.

```python
# 재귀로 반복 된다!!!
def Dsort(LT, RT):
        # ..............#
        # 반으로 가른다
        Dsort(LT, MID) # <--- 여기 실행
        Dsort(MID + 1, RT)
```

![]({{ 'assets/images/algorithm/merge/merge5.gif' | relative_url }})

---

### 6. 또  반으로 나눠서 나눠진 부분 중 한쪽을 다시 리스트 영역을 반으로 나누기 위해서 중앙의 값을 구하기 위해 (LT + RT) // 2 = mid 를 구한다. (이 작업의 RT 값이 LT의 값 보다 클 경우 계속 반복 한다!)

```python
# 재귀로 반복 한다 !!!!
def Dsort(LT, RT):
    # 만약 LT가 RT보다 크거나 같을 경우
    if LT < RT:
        # 중앙 위치 찾기
        MID = (LT + RT) // 2
```

![]({{ 'assets/images/algorithm/merge/merge6.gif' | relative_url }})

---


### 7. 구한 MID 기준으로 반으로 나눠서 나눠진 부분의 양 끝부분을 MID 부분이였던 곳을 또 LT, RT로 바꾼다. (이 때, 작업의 RT 값이 LT 값 보다 작거나 같아지면 멈춘다)

```python
# 재귀로 반복 된다!!!
def Dsort(LT, RT):
        # ..............#
        # 반으로 가른다
        Dsort(LT, MID) # <--- 여기 실행 이제 LT의 값이 MID의 값과 비교해서 같지 않으므로 재귀로 돌아왔던 곳에서 빠져나온다!
        Dsort(MID + 1, RT) # <--- 이제 여기 실행
```

![]({{ 'assets/images/algorithm/merge/merge7.gif' | relative_url }})

---

### 8. RT의 값이 LT의 값보다 작거나 같아지면 TEMP라는 리스트를 생성하여 분리된 값의 처음 부분에 P1과 P2의 영역을 나타내어 작은 값을 TEMP 리스트의 가장 앞에 넣는다.

```python
def Dsort(LT, RT):
    # ........................ #
        # 왼쪽, 오른쪽 자식 다 끝난 후 정렬하기
        # P1의 시작은 맨 앞 LT 인덱스 위치고
        P1 = LT
        # P2의 시작은 자른 다른 반절의 맨 앞 MID + 1 이다
        P2 = MID + 1
        TEMP = []

        # P1의 끝을 넘어가 버리면 P2의 끝을 넘어가버리면 반복 종료
        while P1 <= MID and P2 <= RT:
            if arr[P1] < arr[P2]:
                TEMP.append(arr[P1])
                P1 = P1 + 1
            else:
                TEMP.append(arr[P2])
                P2 = P2 + 1

        # P2가 전부 돌아 한쪽이 끝나면
        # P1이 왼쪽인 기준을 가진 한쪽의 끝은 MID이기 때문에
        # P1이 MID 보다 작으면 남아 있기 때문에 P2가 끝난 경우 이다
        if P1 <= MID:
            # MID 까지므로 MID + 1 까지이다
            TEMP = TEMP + arr[P1:MID+1]
        elif P2 <= RT:
            # arr[P2:]를 하지 않는 이유는
            # 지금 반쪽을 잘라서 인덱스를 하고 있기 때문에
            # arr[P2:]를 하면 잘려있는 것만이 아닌 끝까지 보기 떄문
            TEMP = TEMP + arr[P2:RT+1]
```

![]({{ 'assets/images/algorithm/merge/merge8.gif' | relative_url }})

---

### 9. 만들어진 TEMP 리스트를 기존에 반으로 분리했던 값에 복사한다.



```python
# 재귀로 반복 된다!!!
def Dsort(LT, RT):
    # ...................... #
        for i in range(len(TEMP)):
            # arr[4:8] 부분은 4, 5, 6, 7 의 인덱스를 가지고 있기 때문에
            # 그냥 arr[i]를 넣으면 문제가 생긴다
            # 그래서 시작하는 부분 LT + i를 넣어서 TEMP 값을 넣는다
            arr[LT+i] = TEMP[i]
```


![]({{ 'assets/images/algorithm/merge/merge9.gif' | relative_url }})

---


### 10. 나머지 반쪽 또한 동일한 방법으로 LT와 RT를 이용하여 중앙의 MID 값을 구한다.

```python
# 재귀로 반복 된다!!!
def Dsort(LT, RT):
        # ..............#
        # 반으로 가른다
        Dsort(LT, MID) # <--- 여기 실행 이제 LT의 값이 MID의 값과 비교해서 같지 않으므로 재귀로 돌아왔던 곳에서 빠져나온다!
        Dsort(MID + 1, RT) # <--- 이제 여기 실행
```

```python
# 재귀로 반복 한다 !!!!
def Dsort(LT, RT):
    # 만약 LT가 RT보다 크거나 같을 경우
    if LT < RT:
        # 중앙 위치 찾기
        MID = (LT + RT) // 2
```

![]({{ 'assets/images/algorithm/merge/merge10.gif' | relative_url }})

---

### 11. 반쪽 또한 MID 값 기준으로 반으로 나누어 LT와 RT를 각각 설정한다.

```python
# 재귀로 반복 된다!!!
def Dsort(LT, RT):
        # ..............#
        # 반으로 가른다
        Dsort(LT, MID) # <--- 여기 실행 이제 LT의 값이 MID의 값과 비교해서 같지 않으므로 재귀로 돌아왔던 곳에서 빠져나온다!
        Dsort(MID + 1, RT) # <--- 이제 여기 실행
```

![]({{ 'assets/images/algorithm/merge/merge11.gif' | relative_url }})

---

### 12. RT의 값이 LT의 값보다 작거나 같아지면 TEMP라는 리스트를 생성하여 분리된 값의 처음 부분에 P1과 P2의 영역을 나타내어 작은 값을 TEMP 리스트의 가장 앞에 넣는다.

```python
def Dsort(LT, RT):
    # ........................ #
        # 왼쪽, 오른쪽 자식 다 끝난 후 정렬하기
        # P1의 시작은 맨 앞 LT 인덱스 위치고
        P1 = LT
        # P2의 시작은 자른 다른 반절의 맨 앞 MID + 1 이다
        P2 = MID + 1
        TEMP = []

        # P1의 끝을 넘어가 버리면 P2의 끝을 넘어가버리면 반복 종료
        while P1 <= MID and P2 <= RT:
            if arr[P1] < arr[P2]:
                TEMP.append(arr[P1])
                P1 = P1 + 1
            else:
                TEMP.append(arr[P2])
                P2 = P2 + 1

        # P2가 전부 돌아 한쪽이 끝나면
        # P1이 왼쪽인 기준을 가진 한쪽의 끝은 MID이기 때문에
        # P1이 MID 보다 작으면 남아 있기 때문에 P2가 끝난 경우 이다
        if P1 <= MID:
            # MID 까지므로 MID + 1 까지이다
            TEMP = TEMP + arr[P1:MID+1]
        elif P2 <= RT:
            # arr[P2:]를 하지 않는 이유는
            # 지금 반쪽을 잘라서 인덱스를 하고 있기 때문에
            # arr[P2:]를 하면 잘려있는 것만이 아닌 끝까지 보기 떄문
            TEMP = TEMP + arr[P2:RT+1]
```

![]({{ 'assets/images/algorithm/merge/merge12.gif' | relative_url }})

---

### 13. 만들어진 TEMP 리스트를 기존에 반으로 분리했던 값에 복사한다.

```python
# 재귀로 반복 된다!!!
def Dsort(LT, RT):
    # ...................... #
        for i in range(len(TEMP)):
            # arr[4:8] 부분은 4, 5, 6, 7 의 인덱스를 가지고 있기 때문에
            # 그냥 arr[i]를 넣으면 문제가 생긴다
            # 그래서 시작하는 부분 LT + i를 넣어서 TEMP 값을 넣는다
            arr[LT+i] = TEMP[i]
```

![]({{ 'assets/images/algorithm/merge/merge13.gif' | relative_url }})

---

### 14. 또 크기에 맞는 TEMP 리스트를 생성하여 분리 되어 각각 정령된 값들이 들어 있는 기존 리스트에 P1과 P2를 선언하여 양쪽의 크기를 비교하면서 작은 것 우선으로 TEMP 리스트에 넣는다. (만약 P1에 있는 것이 전부 먼저 들어가고 P2의 값이 많이 있으면 그대로 P2를 순서대로 대입한다)

![]({{ 'assets/images/algorithm/merge/merge14.gif' | relative_url }})

---


### 15. 만들어진 TEMP 리스트를 기존에 반으로 분리했던 값에 복사한다.

![]({{ 'assets/images/algorithm/merge/merge15.gif' | relative_url }})

---

### 16. 이런 작업 또한 계속 반복한다.

![]({{ 'assets/images/algorithm/merge/merge16.gif' | relative_url }})

---

### 17. 이런 작업 또한 계속 반복한다.

![]({{ 'assets/images/algorithm/merge/merge17.gif' | relative_url }})

---

### 18. TEMP 리스트를 생성하여 마지막으로 반으로 전부 분리되어 정렬된 값을 가져와서 각각 P1과 P2로 비교하여 작은 순서대로 TEMP라는 리스트에 대입하여 정렬시킨다.

![]({{ 'assets/images/algorithm/merge/merge18.gif' | relative_url }})

---

### 19. TEMP의 값을 기존의 배열에 복사한다.

![]({{ 'assets/images/algorithm/merge/merge19.gif' | relative_url }})

---

### 20. 병합정렬 끝

![]({{ 'assets/images/algorithm/merge/merge20.png' | relative_url }})

---


---
# 코드
```python
def Dsort(LT, RT):
    # 만약 LT가 RT보다 크거나 같을 경우
    if LT < RT:
        # 중앙 위치 찾기
        MID = (LT + RT) // 2
        # 반으로 가른다
        Dsort(LT, MID)
        Dsort(MID + 1, RT)

        # 왼쪽, 오른쪽 자식 다 끝난 후 정렬하기
        # P1의 시작은 맨 앞 LT 인덱스 위치고
        P1 = LT
        # P2의 시작은 자른 다른 반절의 맨 앞 MID + 1 이다
        P2 = MID + 1
        TEMP = []

        # P1의 끝을 넘어가 버리면 P2의 끝을 넘어가버리면 반복 종료
        while P1 <= MID and P2 <= RT:
            if arr[P1] < arr[P2]:
                TEMP.append(arr[P1])
                P1 = P1 + 1
            else:
                TEMP.append(arr[P2])
                P2 = P2 + 1

        # P2가 전부 돌아 한쪽이 끝나면
        # P1이 왼쪽인 기준을 가진 한쪽의 끝은 MID이기 때문에
        # P1이 MID 보다 작으면 남아 있기 때문에 P2가 끝난 경우 이다
        if P1 <= MID:
            # MID 까지므로 MID + 1 까지이다
            TEMP = TEMP + arr[P1:MID+1]
        elif P2 <= RT:
            # arr[P2:]를 하지 않는 이유는
            # 지금 반쪽을 잘라서 인덱스를 하고 있기 때문에
            # arr[P2:]를 하면 잘려있는 것만이 아닌 끝까지 보기 떄문
            TEMP = TEMP + arr[P2:RT+1]

        for i in range(len(TEMP)):
            # arr[4:8] 부분은 4, 5, 6, 7 의 인덱스를 가지고 있기 때문에
            # 그냥 arr[i]를 넣으면 문제가 생긴다
            # 그래서 시작하는 부분 LT + i를 넣어서 TEMP 값을 넣는다
            arr[LT+i] = TEMP[i]


if __name__ == "__main__":
    arr = [23, 11, 45, 36, 15, 67, 33, 21]
    print("Before sort : ", end="")
    print(arr)
    Dsort(0, len(arr)-1)
    print()
    print("After sort : ", end="")
    print(arr)
```
