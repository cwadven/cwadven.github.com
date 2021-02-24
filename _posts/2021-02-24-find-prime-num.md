---
title: "[알고리즘 프로그래머스] 소수 찾기 (LEVEL 2)"
tag:
- 알고리즘
- 프로그래머스 LEVEL2
categories:
- algorithm
---

# (문제) 소수 찾기 (LEVEL 2) [DFS]
---

한자리 숫자가 적힌 종이 조각이 흩어져있습니다.

흩어진 종이 조각을 붙여 소수를 몇 개 만들 수 있는지 알아내려 합니다.

각 종이 조각에 적힌 숫자가 적힌 문자열 numbers가 주어졌을 때, 종이 조각으로 만들 수 있는 소수가 몇 개인지 return 하도록 solution 함수를 완성해주세요.

> **입력설명**

입력으로는 문자열인 숫자 형태가 들어온다.

numbers는 길이 1 이상 7 이하인 문자열입니다.

numbers는 0~9까지 숫자만으로 이루어져 있습니다.

013은 0, 1, 3 숫자가 적힌 종이 조각이 흩어져있다는 의미입니다.

> **출력설명**

각 종이 조각에 적힌 숫자가 적힌 문자열 numbers가 주어졌을 때, 종이 조각으로 만들 수 있는 소수가 몇 개인지 return 하도록 solution 함수를 완성

> **테스트케이스**
 

| 입력예제 | 출력예제 |
| -------- | -------- | 
| "17"	| 3 | 
| "011"	| 2 | 

~~~
입출력 예 설명
예제 #1
[1, 7]으로는 소수 [7, 17, 71]를 만들 수 있습니다.

예제 #2
[0, 1, 1]으로는 소수 [11, 101]를 만들 수 있습니다.

11과 011은 같은 숫자로 취급합니다.
~~~

---
# 해결방법

문제에서 해결해야 하는 것이 2가지가 있다.

1. 순열 구하기
2. 소수 인지 판별

총 방법은 Python 모듈을 이용해서 순열을 구하는 방법과 DFS를 이용해가지고 순열을 구하는 방법이 있다.

필자는 두가지 전부 다 해보려고 한다.

### 방법 1 : DFS 를 이용해서 순열 구하기

DFS로 순열을 구하기 위해서 순열을 구하기 위한 방법을 생각해 보아야 한다.

아래 그림과 같이 우선 그림을 그릴 수 있다.

![]({{ 'assets/images/algorithm/prime_dfs/prime_dfs1.PNG' | relative_url }})<br><br>

여기서 우리가 생각해야하는 것은 순열은 이용했던 것은 사용할 수 없는 것이다.

![]({{ 'assets/images/algorithm/prime_dfs/prime_dfs2.PNG' | relative_url }})<br><br>

그러면 어떻게 이렇게 막을 수 있을 지를 생각해보자...

numbers ==> [3, 7, 8] 이런 식으로 있을 경우, 이 숫자를 1번이라도 썻는지 안 썻는지를 알 수 있는 체크할 수 있는 무언가가 필요하다.

필자는 ch 라는 새로운 리스트를 만들었고, 크기는 numbers 크기와 같이 [0, 0, 0] 0으로 안을 초기화 했다.

그러면 이런 조건을 생각할 수 있다.

만약 numbers의 인덱스를 이용하려고 할 때, 똑같이 ch의 인덱스를 봐서 이게 만약 0일 경우 사용할 수 있다. 즉, 아직 한번도 이용하지 않았다! 라고 가정 할 수 있다.

만약 해당 numbers 인덱스를 사용하면 ch의 인덱스의 값을 1로 바꿔주면 여기를 돌았다! 라는 것을 알 수 있을 것이다.

```python
numbers = [3, 7, 8]
# 순열 구하기 위한 체크하기 위한 용
ch = [0] * len(numbers)
nPr = []
only_numbers = set()
   
# 순열 구하기
def dfs(L):
    if L > len(numbers):
        True
    else:
        for i in range(len(numbers)):
            if ch[i] == 0:
                nPr.append(numbers[i])
                only_numbers.add(int("".join(nPr)))
                ch[i] = 1
                # 계층 올리기
                dfs(L+1)
                nPr.pop()
                ch[i] = 0
dfs(0)
```

우리가 알아야 하는 것은 순열이니, 이 각 1개를 접근 할 때 마다 순열이 되는 것이다.

이게 무슨 말이냐면

아래 그림과 같이 인덱스를 접근할 때마다 순열이 된다는 것이다!

![]({{ 'assets/images/algorithm/prime_dfs/prime_dfs3.PNG' | relative_url }})<br><br>

그래서 순열을 저장할 리스트를 만들어서 한 인덱스 마다 append() 를 하도록 하고 DFS여서 다시 밖으로 나와야 하므로 pop() 하고 ch의 해당 인덱스를 다시 0으로 초기화 한다!

참고로 해당 순열을 구해야하는데, 그 중에서 중복이 되는 숫자도 생길 수 있으므로 중복되지 않는 값을 넣어야 하므로 구한 수열을 .join을 통해서 문자열로 만들어서 그 해당 문자열을 set() 집합 자료형에 add() 한다.

중복 된다는 말은 이런 경우가 아래와 같은 0, 1, 1로 할 경우 중복이 생길 수 있다는 의미이다.

![]({{ 'assets/images/algorithm/prime_dfs/prime_dfs4.PNG' | relative_url }})<br><br>

이렇게 순열을 구했다면 이제 소수를 구하면 되는데 이 경우는 기존에 소수 구하는 방법을 작성한 글이 있으니 그곳을 참고하면 될 것 같다!

[소수 구하기 참고 링크](https://cwadven.github.io/algorithm/programmers-prime-num/)

### 방법 2 : python itertools 모듈 사용

파이썬에는 순열과 조합을 제공하는 함수가 존재한다.

import itertools 안에 내장되어 있는 함수이다.

사용을 할 때는 itertools.permutations(리스트혹은연속된자료형, 구하려는 순열 자리수)

구하려는 순열 자리수라는 의미는 만약 1, 2, 3을 이용하여 순열 자리수를 2로 지정했다면

1, 2 / 1, 3 / 2, 1 / 2, 3 / 3, 1 / 3, 2 와 같이 2자리로 구한다는 의미이다.

우리는 모든 순열을 구해야하므로

반복문을 이용해서 1 부터 구하려는 문자의 개수 만큼 반복문을 돌려서 구하려는 순열 자리수를 증가시켜가면 된다.

이렇게 구한 값은 각 리스트로 묶여져 나오므로 set() 자료형에 삽입하면 된다.

이렇게 구했으면 소수를 구하면 된다.


---
# 코드 방법 1
```python
def solution(numbers):
    # 순열 구하기 위한 체크하기 위한 용
    ch = [0] * len(numbers)
    nPr = []
    only_numbers = set()
    
    # 순열 구하기
    def dfs(L):
        if L > len(numbers):
            True
        else:
            for i in range(len(numbers)):
                if ch[i] == 0:
                    nPr.append(numbers[i])
                    only_numbers.add(int("".join(nPr)))
                    ch[i] = 1
                    # 계층 올리기
                    dfs(L+1)
                    nPr.pop()
                    ch[i] = 0
    dfs(0)
    
    # 0과 1은 소수가 될 수 없으니
    only_numbers = only_numbers - {0, 1}
    
    count = 0
    # 구한 순열들로 소수 구하기
    for i in only_numbers:
        for j in range(2, int(i**0.5)+1):
            if i % j == 0:
                break
        else:
            count = count + 1
        
    return count
```


# 코드 방법 2
```python
import itertools

def solution(numbers):
    answer = set()

    # 모든 순열을 만든다
    for i in range(1, len(numbers)+1):
        nPr = itertools.permutations(numbers, i)
        for j in nPr:
            answer.add(int("".join(j)))

    count = 0

    answer = answer - {0, 1}

    for i in answer:
        # 소수인지 판별 하는 거지
        for j in range(2, int(i ** 0.5)+1):
            if i % j == 0:
                break
        else:
            count = count + 1

    return count
```
