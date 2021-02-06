---
title: "[파이썬] 정규표현식 5 ([] 범위 제외)"
tag:
- 정규표현식
categories:
- python
- regular_expression
---

> **패턴 범위 제외**

```python
import re

test1 = re.match('[^A-Z]+', 'Hello')
test2 = re.match('[^A-Z]+', 'hello')

print(test1, test2, sep='\n')
```

~~~
None
<re.Match object; span=(0, 5), match='hello'>
~~~

범위 [] 안에 ^를 앞에 넣으면 의미는 제외가 된다.

```python
import re

test1 = re.match('[^A-Z]+', 'Hello')
test2 = re.match('[^A-Z]+', 'hello')

test3 = re.search('^[A-Z]+', 'HELlo')

print(test1, test2, test3, sep='\n')
```

~~~
None
<re.Match object; span=(0, 5), match='hello'>
<re.Match object; span=(0, 3), match='HEL'>
~~~

`search` 의 ^와 헷갈릴 수 있지만 `search`의 ^는 시작할 때, 해당 문자로 시작하는지 아는 것이고

범위 [] 안에 ^를 앞에 넣으면 범위는 포함하지 않는다는 의미이다.
