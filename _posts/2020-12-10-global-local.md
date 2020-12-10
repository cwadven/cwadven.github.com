---
title: "[코드] 전역변수와 지역변수 란?"
tag:
- 전역변수
- 지역변수
- global variable
- local variable
categories:
- python
---

# 전역변수와 지역변수 란?
---

파이썬은 변수를 소스코드에 선언하는 경우 전역변수로 잡힌다.

**전역변수**는 모든 함수에서 접근할 수 있고, 해당 변수를 변경도 할 수 있다.

**전역변수**는 '공용'이라고 생각하면 된다.

## 예제1 (전역변수 방식)

<<소스코드 예제>>

```python
def dfs1():
    print(cnt)

def dfs2():
    if cnt == 5:
        print(cnt)

cnt = 5
dfs1()
dfs2()
print(cnt)
```

---

```python
cnt = 5
dfs1()
```

`전역변수`를 생성하고, dfs1()을 접근을 한다.

```python
def dfs1():
    print(cnt)
```

dfs1()을 접근한 후, 함수안에 있는 변수가 함수에서 선언된 `지역변수`인지 먼저 확인한다.

만약 `지역변수`로 확인이 된다면 해당 변수를 이용한다.

하지만 함수 안에  `지역변수`가 없을 경우, `전역변수`인지를 파악하여 `전역변수`로 사용을 한다.

**<<참조하는 순서>>**

`지역변수` > `전역변수` 

결국 예제의 소스코드 출력은

```python
5
5
5
```

로 나온다.

## 예제2 (지역변수 방식)

<<소스코드 예제>>

```python
def dfs1():
    cnt = 3
    print(cnt)

def dfs2():
    if cnt == 5:
        print(cnt)

cnt = 5
dfs1()
dfs2()
print(cnt)
```
---

```python
def dfs1():
    cnt = 3
    print(cnt)
```

cnt라는 변수를 만들고, 그곳에 3이라는 값을 할당한다.

이렇게 된다면 cnt라는 변수는 dfs1()의 `지역변수`가 되는 것이다.

결국 예제의 소스코드 출력은

```python
3
5
5
```

로 나온다.


## 예제3 (전역변수, 지역변수 느낌 global)

<<소스코드 예제>>

```python
def dfs1():
    cnt = 3
    print(cnt)

def dfs2():
    if cnt == 5:
        # 추가한 정보
        cnt = cnt + 1
        print(cnt)

cnt = 5
dfs1()
dfs2()
print(cnt)
```
---

```python
def dfs2():
    if cnt == 5:
        cnt = cnt + 1
        print(cnt)
```

파이썬의 인터프리터로 **언어 번역**을 했을 때, dfs2() 함수 조건문 안에 cnt라는 변수를 선언 하여 cnt + 1로 넣었다.<br>
(즉, `지역변수`를 선언했다.)

하지만 cnt `지역변수`로 선언 했지만, if cnt == 5: 를 실행하기 전에 cnt 변수에 값이 없기 때문에 에러가 나온다.

![]({{ 'assets/images/global_local1.PNG' | relative_url }})

로 나온다.

하지만 위와 같이 코드를 짤 경우 우리는 cnt라는 변수가 `전역변수`라는 가정으로 짠다. 

이럴 경우 "cnt가 `전역변수`이다. " 라고 함수에게 알려주면 된다.

```python
def dfs2():
    global cnt
    if cnt == 5:
        # 추가한 정보
        cnt = cnt + 1
        print(cnt)
```

위의 dfs2() 함수에서 cnt의 `전역변수`를 +1로 더해줬기 때문에 cnt는 6이 된다.

결국 예제의 소스코드 출력은

```python
3
6
6
```

로 나온다.

---
# 파이썬 리스트
파이썬의 리스트는 지역변수로 잡히지 않고, 전역 변수로 잡힌다.

## 예제1 (리스트)

<<소스코드 예제>>

```python
def dfs():
    a[0] = 7
    print(a)

a = [1, 2, 3]
dfs()
print(a)
```

아래 코드는 dfs() 함수의 내용이다.

```python
def dfs():
    a[0] = 7
    print(a)
```

여기서 `a[0] = 7` 의미는 변수를 할당하는게 아니라 `전역리스트`의 인덱스 값을 변경한다 라는 '참조'라고 생각하면 된다.

그래서 출력은

```python
[7, 2, 3]
[7, 2, 3]
```

이 된다.

---

## 예제2 (리스트)

<<소스코드 예제>>

```python
def dfs():
    a = [7, 8]
    print(a)

a = [1, 2, 3]
dfs()
print(a)
```

아래 코드는 dfs() 와 같이 a라는 리스트를 새로 선언한다면 a라는 리스트는 `지역리스트`가 되는 것이다!

```python
def dfs():
    a = [7, 8]
    print(a)
```

그래서 출력은

```python
[7, 8]
[1, 2, 3]
```

이 된다.

---

## 예제3 (리스트 오류 뜨는 경우)

<<소스코드 예제>>

```python
def dfs():
    a = a + [4]
    print(a)

a = [1, 2, 3]
dfs()
print(a)
```

아래 코드는 a라는 리스트를 새로 선언하는데 a 라는 리스트에 + `[4]` 를 하는 것이다.

```python
def dfs():
    a = a + [4]
    print(a)
```

이때 '언어번역'에서 a를 `지역변수`로 선언하여 그 안에 값을 넣으려고 하는데 a를 더한다고 하니

하지만 그전에 `지역변수` a는 정의가 되어 있지 않기 때문에 문제가 생긴다.

애러를 방지하기 위해서는 

```python
def dfs():
    global a
    a = a + [4]
    print(a)
```

로 하면 된다.
