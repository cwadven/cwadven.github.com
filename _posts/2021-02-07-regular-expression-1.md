---
title: "[파이썬] 정규표현식 1 (match, search, ^, $, OR)"
tag:
- 정규표현식
- ''
categories:
- regular_expression
- python
---

### 정규표현식 : "일정한 규칙"을 가진 문자열을 표현하는 방법

Python에서는 import re를 하여 정규표현식을 나타낼 수 있다.

> **re.match**
> 
>  re.match("패턴", "문자열")

```python
import re

test1 = re.match("hello", "hello")
test2 = re.match("hello", "hello world")
test3 = re.match("hello", "world hello")

print(test1, test2, test3, sep='\n')
```

~~~
<re.Match object; span=(0, 5), match='hello'>
<re.Match object; span=(0, 5), match='hello'>
None
~~~

`re.match` 함수는 문자열의 처음부터 시작하여 패턴이 일치되는 것이 있는지를 확인한다.

위의 예시에서 첫번째는 패턴과 문자열이 동일하므로 매치되는 것을 확인할 수 있다.

두번째 예시는 문자열이 `'hello'`로 시작하기 때문에 매치가 된다.

나머지는 `'hello'`로 시작하지 않아 패턴 `'hello'`와 매치되지 않는다.

매치되지 않을 때 `re.match` 함수는 `None`을 반환한다.


> **re.search**
> 
>  re.match("패턴", "문자열")

```python
import re

test1 = re.search("^Hello", "My Hello Friend")
test2 = re.search("^Hello", "Hello My Friend")
test3 = re.search("Hello$", "Hello My Friend")
test4 = re.search("Hello$", "My Friend Hello")
test5 = re.search("Hello", "My Hello Friend")

print(test1, test2, test3, test4, test5, sep='\n')
```

~~~
None
<re.Match object; span=(0, 5), match='Hello'>
None
<re.Match object; span=(10, 15), match='Hello'>
<re.Match object; span=(3, 8), match='Hello'>
~~~

패턴 앞에 `^` 가 있을 경우 이 패턴이 문자열의 맨 앞에 오는지 판단

패턴 뒤에 `$` 가 있을 경우 이 패턴이 문자열의 맨 뒤에 오는지 판단

패턴 앞 뒤에 아무것도 없을 경우 이 패턴이 문자열의 어디에 오는지 판단

**`re.search`, `re.match` 차이점 :<br>re.search는 반드시 문자열의 처음부터 일치해야 하는 것은 아니다.**

---

> **OR 연산 `|`**
> 
>  re.match("패턴 `|` 패턴", "문자열")
>  
>    re.search("패턴 `|` 패턴", "문자열")

```python
import re

test1 = re.search("Friend|Hello", "My Hello Friend")
test2 = re.search("Friend|Hello", "My Friend Hello")

print(test1, test2, sep='\n')
```

~~~
<re.Match object; span=(3, 8), match='Hello'>
<re.Match object; span=(3, 9), match='Friend'>
~~~

패턴에 | 는 하나라도 있을 경우 그것의 위치를 찾는다.

test1은 Hello가 먼저 발견 되어서 Hello

test2는 Friend가 먼저 발견 되어서 Friend
