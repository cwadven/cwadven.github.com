---
title: "[알고리즘] 알파코드(DFS)"
tag:
- dfs
- 깊이우선탐색
- 알고리즘
categories:
- algorithm
---

# (문제) 알파코드(DFS)
---

철수와 영희는 서로의 비밀편지를 암호화해서 서로 주고받기로 했다.

그래서 서로 어떻게 암호화를 할 것인지 의논을 하고 있다

`영희` : 우리 알파벳 A에는 1로, B에는 2로 이렇게 해서 Z에는 26을 할당하여 번호로 보내기로 하자.

`철수` : 정말 바보같은 생각이군!! 생각해 봐!! 만약 내가 “BEAN"을 너에게 보낸다면 그것을 암호화하면 25114이잖아!! 그러면 이것을 다시 알파벳으로 복원할 때는 많은 방법이 존재하는데 어떻게 할건데... 이것을 알파벳으로 바꾸면 BEAAD, YAAD, YAN, YKD 그리고 BEKD로 BEAN말고도 5가지나 더 있군.

당신은 위와 같은 영희의 방법으로 암호화된 코드가 주어지면 그것을 알파벳으로 복원하는데 얼마나 많은 방법인 있는지 구하세요.


> **입력설명**

첫 번째 줄에 숫자로 암호화된 코드가 입력된다.<br>
(코드는 0으로 시작하지는 않는다, 코드의 길이는 최대 50이다) 

0이 입력되면 입력종료를 의미한다.

> **출력설명**

입력된 코드를 알파벳으로 복원하는데 몇 가지의 방법이 있는지 각 경우를 출력한다.

그 가지수도 출력한다.

단어의 출력은 사전순으로 출력한다.

> **테스트케이스**
 

| 입력예제 | 출력예제 |
| -------- | -------- | 
| 25114 | BEAAD<br>BEAN<br>BEKD<br>YAAD<br>YAN<br>YKD<br>6 | 
| 115213102 | AAEBACJB<br>AAEBMJB<br>AAEUCJB<br>AOBACJB<br>AOBMJB<br>AOUCJB<br>KEBACJB<br>KEBMJB<br>KEUCJB<br>9 | 

---
# 해결방법
1. ASCII 코드 이용 (입력의 값을 숫자화 + 64를 하여 ASCII 코드화 시킨다)
2. 1 글자와 2 글자를 순회 할 수 있다는 것을 알게되서 반복문 사용
3. 아래 동작 시각화 처럼 가지를 쳐봄
4. L + i 를 통해 Layer의 깊이를 들어감 (알겠는데, 잘 모르겠음...)
## 동작 시각화

![]({{ 'assets/images/algorithm/alpha_code/alpha_code1.png' | relative_url }})

---
# 코드
```python
def DFS(L, word):
    global count
    if L == len(a):
        count = count + 1
        print(word)
    else:
        # 반복문을 돌린다 a라는 문자열은 1 글자 혹은 2 글자로 나눠지니 1 ~ 2를 반복
        for i in range(1, 3):
            # 문자를 숫자화 시키는데 해당 숫자가 26이 넘지 않을 경우 확인
            if not int(a[L:L+i]) > 26:
                # 만약에 0이 있을 경우 해당 부분은 return 한다
                if int(a[L:L+i]) == 0:
                    return
                # 문자의 길이보다 L + i 가 크지 않을 경우 DFS를 실행한다!
                # 이때 L은 + i를 하여 1칸 혹은 2칸 띄울 수 있도록 설정 한다.
                if not L + i > len(a):
                    # 문자로 바꾸기 위해서 문자를 숫자화 시키고 ASCII 코드를 이용하여 문자로 만든다
                    DFS(L + i, word+chr(int(a[L:L+i])+64))

count = 0

a = input()

DFS(0, '')

print(count)
```
