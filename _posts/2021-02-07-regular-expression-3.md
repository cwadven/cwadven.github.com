---
title: "[파이썬] 정규표현식 3 ((), {})"
tag:
- 정규표현식
categories:
- python
- regular_expression
---

> **패턴 개수 직접 정해주기 {} (글자)**

```python
import re

test1 = re.match('ooo', 'oooh hello!')
test2 = re.match('[0-9][0-9][0-9]-[0-9][0-9][0-9][0-9]-[0-9][0-9][0-9][0-9]', '010-1111-3333 입니다!')

print(test1, sep='\n')
```

~~~
<re.Match object; span=(0, 3), match='ooo'>
<re.Match object; span=(0, 13), match='010-1111-3333'>
~~~

위와 같이 test1의 문자와 test2의 휴대전화 번호를 예를 들어보자 이렇게 사용할 수 있겠지만, 가독성이 너무 좋지 않다!

```python
import re

test1 = re.match('o{3}', 'oooh hello!')
test2 = re.match('[0-9]{3}-[0-9]{4}-[0-9]{4}', '010-1111-3333 입니다!')

print(test1, test2, sep='\n')
```

~~~
<re.Match object; span=(0, 3), match='ooo'>
<re.Match object; span=(0, 13), match='010-1111-3333'>
~~~

이렇게 작성을 하면 패턴에 `'글자{개수}'` 혹은 `[범위]{개수}` 를 적으면 그 개수 만큼 확인을 한다.

---

> **패턴 개수 직접 정해주기 {} (단어)**

```python
import re

test1 = re.match('(hello){3}', 'hellohellohelloworld')

print(test1, sep='\n')
```

~~~
<re.Match object; span=(0, 15), match='hellohellohello'>
~~~

글자 뿐만 아니라 단어 또한 가능하다.

단어를 묶을 때는 ( ) 로 묶어야 한다.

---

> **패턴 개수 직접 정해주기 {} (개수 유동적으로 정하기)**

```python
import re

test1 = re.match('[0-9]{2,3}-[0-9]{3,4}-[0-9]{4}', '010-1111-3333')
test2 = re.match('[0-9]{2,3}-[0-9]{3,4}-[0-9]{4}', '063-811-3223')
test3 = re.match('[0-9]{2,3}-[0-9]{3,4}-[0-9]{4}', '02-811-3311')

print(test1, test2, test3, sep='\n')
```

~~~
<re.Match object; span=(0, 13), match='010-1111-3333'>
<re.Match object; span=(0, 12), match='063-811-3223'>
<re.Match object; span=(0, 11), match='02-811-3311'>
~~~

위처럼 휴대폰 전화번호 및 집 전화 번호로 예를 들어보자.

휴대폰 전화번호는 중간에 4개가 들어가야하지만 집 전화번호는 상황에 따라 3개 혹은 4개가 될 수 있다.

또한 집전화 번호는 앞 숫자가 서울은 02 이므로 2글자도 가능하다. 

이렇게 유동적으로 판단하고 싶을 경우 `문자{시작개수, 끝개수}` 를 선정하여 유동적으로 개수를 선택할 수 있다.
