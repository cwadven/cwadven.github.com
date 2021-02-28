---
title: "[알고리즘 프로그래머스] 가장 큰 정사각형 찾기 (LEVEL 2)"
tag:
- 알고리즘
- 프로그래머스 LEVEL2
- dp
categories:
- algorithm
---

# (문제) 가장 큰 정사각형 찾기 (LEVEL 2) [DP]
---

1와 0로 채워진 표(board)가 있습니다.

표 1칸은 1 x 1 의 정사각형으로 이루어져 있습니다.

표에서 1로 이루어진 가장 큰 정사각형을 찾아 넓이를 return 하는 solution 함수를 완성해 주세요.<br>
(단, 정사각형이란 축에 평행한 정사각형을 말합니다.)

예를 들어

![]({{ 'assets/images/algorithm/biggest_square/biggest_square1.PNG' | relative_url }})<br><br>

가 있다면 가장 큰 정사각형은

![]({{ 'assets/images/algorithm/biggest_square/biggest_square2.PNG' | relative_url }})<br><br>

가 되며 넓이는 9가 되므로 9를 반환해 주면 됩니다.

> **입력설명**

입력으로는 2차원 리스트가 들어옵니다.

표(board)는 2차원 배열로 주어집니다.

표(board)의 행(row)의 크기 : 1,000 이하의 자연수

표(board)의 열(column)의 크기 : 1,000 이하의 자연수

표(board)의 값은 1또는 0으로만 이루어져 있습니다.


> **출력설명**

가장 큰 정사각형을 찾아 넓이를 return

> **테스트케이스**
 

| 입력예제 | 출력예제 |
| -------- | -------- | 
| [[0,1,1,1],[1,1,1,1],[1,1,1,1],[0,0,1,0]]	| 9 | 
| [[0,0,1,1],[1,1,1,1]]	| 4 | 

~~~
입출력 예 설명
입출력 예 #1
위의 예시와 같습니다.

입출력 예 #2
| 0 | 0 | 1 | 1 |
| 1 | 1 | 1 | 1 |
로 가장 큰 정사각형의 넓이는 4가 되므로 4를 return합니다.
~~~

---
# 해결방법

우리는 어떻게 DP로 정사각형의 크기를 정할 수 있냐에 관한 생각을 할 수 있다.

DP는 대체로 누적한다는 생각을 가지면 된다.

자, 우선 정사각형은 모서리의 크기가 같으면 생기는 것이다.

그러면 이렇게 생각할 수 있다.

![]({{ 'assets/images/algorithm/biggest_square/biggest_square4.PNG' | relative_url }})<br><br>

상, 좌, 대각 상/좌 가 전부 1 이면 정사각형이라는 것을 알 수가 있다.

하지만 이러면 1이 4개인 정사각형 밖에 모른다... 이럴 경우 우리는 기존의 값을 누적해서 가져가 생각할 수 있다.

현재 위치의 사각형의 상, 좌, 대각 상/좌 가 전부 1이면 현재 위치의 사각형은 2가 될 수 있다.

![]({{ 'assets/images/algorithm/biggest_square/biggest_square5.PNG' | relative_url }})<br><br>

이유는 상, 좌, 대각 상/좌 가 전부 1이기 때문이다.

그러면 그 옆에 사각형은 어떻게 되겠나?

![]({{ 'assets/images/algorithm/biggest_square/biggest_square6.PNG' | relative_url }})<br><br>

이 또한 2가 될 것이다.

만약 모든 상, 좌, 대각 상/좌 의 가장 최소 값에서 + 1을 하는 값이 현재 위치의 사각형 값이 될 것이다.

만약 주변이 전부 2 이면 ...

![]({{ 'assets/images/algorithm/biggest_square/biggest_square7.PNG' | relative_url }})<br><br>

이렇게 3이 될 것이다.

그리고 만약 현재 위치에 있는 사각형의 값이 0이면 이 과정을 이용하지 않는다.

![]({{ 'assets/images/algorithm/biggest_square/biggest_square8.PNG' | relative_url }})<br><br>

이유는 해당 위치는 값이 없기 때문이다.

그래서 이 문제의 시작은 인덱스 1 열과 1 행부터 시작을 한다.

이유는 상, 좌, 대각 상/좌를 비교해야하기 때문이다.

![]({{ 'assets/images/algorithm/biggest_square/biggest_square3.PNG' | relative_url }})<br><br>

현재 위치에 있는 값이 1 이면 초기화 되어있는 것이기 때문에 `상, 좌, 대각 상/좌 값 중 가장 작은 값` + 1이 현재 위치 값으로 덮어쓴다.

완료 후, 리스트 안에 있는 가장 큰 수에 제곱을 하면 넓이를 구할 수 있다.

이 때 큰 수를 알기 위해 각 행 마다 최대 값을 저장할 수 있는 변수를 0으로 초기화 하여 큰 값이 있으면 대입하면서 저장 후, 그 값을 제곱하여 출력한다.



---
# 코드
```python
def solution(board):
    res = 0

    for i in range(1, len(board)):
        for j in range(1, len(board[0])):
            current = min(board[i-1][j], board[i][j-1], board[i-1][j-1])
            if board[i][j] == 1:
                board[i][j] = current + 1
    
    for x in board:
        _max = max(x)
        if res < _max:
            res = _max
            
    return res ** 2
```
