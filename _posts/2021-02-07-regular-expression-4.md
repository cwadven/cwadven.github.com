---
title: "[파이썬] 정규표현식 4 (영문 숫자 한글 특수문자 범위 포함)"
tag:
- 정규표현식
categories:
- python
- regular_expression
---

> **패턴 영문 숫자 범위로 포함**

```python
import re

test1 = re.match('[a-zA-Z0-9]+', 'Hello1234')
test2 = re.match('[A-Z0-9]+', 'hello')

print(test1, test2, sep='\n')
```

~~~
<re.Match object; span=(0, 9), match='Hello1234'>
None
~~~

문자와 숫자 까지 같이 범위로 나타낼 수 있다

---

> **패턴 한글 범위로 포함**

```python
import re

test1 = re.match('[가-힣]+', '안녕하세요')

print(test1, sep='\n')
```

~~~
<re.Match object; span=(0, 5), match='안녕하세요'>
~~~

한글 또한 범위로 나타낼 수 있다!

범위를 가 ~ 힣 까지 하면 된다.

---

> **패턴 특수문자 범위로 포함**

```python
import re

test1 = re.match('[$()a-zA-Z0-9]+', '$(document)')
test2 = re.match('\*+', '****@naver.com')

print(test1, test2, sep='\n')
```

~~~
<re.Match object; span=(0, 11), match='$(document)'>
<re.Match object; span=(0, 4), match='****'>
~~~

`[ ]` 범위 안에는 `\` 를  입력할 필요없지만, 아닐 경우는 이스케이프를 이용하여 \ 를 꼭 붙여줘야한다.
