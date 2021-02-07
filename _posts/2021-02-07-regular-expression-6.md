---
title: "[파이썬] 정규표현식 6 ([]범위 간단 설정)"
tag:
- 정규표현식
categories:
- python
- regular_expression
---

> **[] 범위 약어로 간단 설정**

```python
import re

test1 = re.match('\d+', '12345hello')
test2 = re.match('\D+', 'Hello12345')
test3 = re.match('\w+', 'Hello12345')
test4 = re.match('\W+', '():Hello1245')
test5 = re.match('\s+', '     Hello')
test6 = re.match('\S+', 'Hello   my')

print(test1, test2, test3, test4, test5, test6, sep='\n')
```

~~~
<re.Match object; span=(0, 5), match='12345'>
<re.Match object; span=(0, 5), match='Hello'>
<re.Match object; span=(0, 10), match='Hello12345'>
<re.Match object; span=(0, 3), match='():'>
<re.Match object; span=(0, 5), match='     '>
<re.Match object; span=(0, 5), match='Hello'>
~~~

* \d : [0-9]의 의미 (모든 숫자)
* \D : [^0-9]의 의미 (모든 숫자 제외)
* \w : [a-zA-Z0-9_]의 의미 (대소문자, 숫자, 밑줄)
* \W : [^a-zA-Z0-9_]의 의미 (대소문자, 숫자, 뭍줄 제외)
* \s : [ \t\n\r\f\v]의 의미 (스페이스, 탭, 새줄, 캐리지 리턴, 폼피드, 수직탭)
* \S : [^ \t\n\r\f\v]의 의미 (스페이스, 탭, 새줄, 캐리지 리턴, 폼피드, 수직탭 제외)
