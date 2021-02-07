---
title: "[파이썬] 정규표현식 9 (findall, sub, sub 교체함수, sub 찾은 문자열 사용)"
tag:
- 정규표현식
categories:
- python
- regular_expression
---

> **패턴에 매칭되는 모든 문자열 가져오기 findall**

`re.findall('패턴', '문자열')`

```python
import re

r = re.compile('[0-9]+')
test1 = r.findall("12 2 Fizz 4 Buzz Fizz 7 8")

print(test1, sep='\n')
```

~~~
['12', '2', '4', '7', '8']
~~~

그룹 지정 없이 패턴에 매칭되는 모든 문자열을 가져오기

findall 함수를 사용하며 매칭된 문자열을 리스트로 반환

---

> **문자열 바꾸기 sub**

`re.sub('패턴', '바꿀문자열', '문자열', 바꿀횟수)`

문자열을 바꿀 때는 sub 함수를 사용

바꿀 횟수를 넣으면 지정된 횟수만큼 바꾸며 바꿀 횟수를 생략하면 찾은 문자열을 모두 바꾼다

```python
import re

r = re.compile('[0-9]+')
test1 = r.sub("CHANGE", "12 2 Fizz 4 Buzz Fizz 7 8")
test2 = r.sub("CHANGE", "12 2 Fizz 4 Buzz Fizz 7 8", 2)

print(test1, test2, sep='\n')
```

~~~
CHANGE CHANGE Fizz CHANGE Buzz Fizz CHANGE CHANGE
CHANGE CHANGE Fizz 4 Buzz Fizz 7 8
~~~

test2는 2번만 바꾸려고 하기 때문에 2개만 바꿔진 것이다.

---

> **문자열 바꾸기 sub 교체함수**

```python
import re

def multiple10(m):
    return str(int(m.group()) * 10)

r = re.compile('[0-9]+')
# 함수로
test1 = r.sub(multiple10, "12 2 Fizz 4 Buzz Fizz 7 8")
# lambda 로
test2 = r.sub(lambda m: str(int(m.group()) * 10), "12 2 Fizz 4 Buzz Fizz 7 8", 2)

print(test1, test2, sep='\n')
```

~~~
120 20 Fizz 40 Buzz Fizz 70 80
120 20 Fizz 4 Buzz Fizz 7 8
~~~

위와 같이 sub 함수는 바꿀 문자열 대신 `교체 함수`를 지정할 수도 있다

`교체 함수`는 매개변수로 match 객체를 받으며 바꿀 결과를 문자열로 반환

---

> **찾은 문자열을 결과에 다시 사용하기**
 
 `re.sub('그룹패턴', '\\그룹숫자', '문자열', 바꿀횟수)`
 
 **형태 : `\\숫자`**
 
 **정규표현식을 그룹으로 묶는다**
 
```python
import re

test = re.sub('([a-z]+) ([0-9]+)', '\\2 \\1 \\2 \\1', 'hello 1234')

print(test)
```

~~~
1234 hello 1234 hello
~~~

**정규표현식을 그룹으로 묶는다**

바꿀 문자열에서 **`\\숫자`** 형식으로 매칭된 문자열을 가져와서 사용할 수 있다

---


> **찾은 문자열을 결과에 다시 사용하기 활용**
 

```python
import re

test = re.sub('({\s*)\"(\w+)\"\s*:\s*\"?(\w+)\"?(\s*})', '<\\2>\\3</\\2>', '{ "name" : "james" }')

print(test)
```

~~~
<name>james</name>
~~~

딕셔너리를 태그 처럼 바꾸는 느낌

![]({{ 'assets/images/algorithm/regular_expression/regular_expression2.png' | relative_url }})<br><br>
