---
title: "[파이썬] 정규표현식 7 (compile 같은 정규표현식 패턴 저장)"
tag:
- 정규표현식
categories:
- python
- regular_expression
---

> **같은 정규표현식 패턴을 자주 사용할 때 compile 사용**

```python
import re

test1 = re.match('[0-9]{2,3}-[0-9]{3,4}-[0-9]{4}', '010-1111-3333')
test2 = re.match('[0-9]{2,3}-[0-9]{3,4}-[0-9]{4}', '02-855-4567')
test3 = re.match('[0-9]{2,3}-[0-9]{3,4}-[0-9]{4}', '063-857-4567')

print(test1, test2, test3, sep='\n')
```

~~~
<re.Match object; span=(0, 13), match='010-1111-3333'>
<re.Match object; span=(0, 11), match='02-855-4567'>
<re.Match object; span=(0, 12), match='063-857-4567'>
~~~

위의 예제는 매번 match나 search 함수에 정규표현식 패턴을 지정하는 방법은 비효율적이다.


```python
import re

r = re.compile('[0-9]{2,3}-[0-9]{3,4}-[0-9]{4}')
test1 = r.match('010-1111-3333')
test2 = r.match('02-855-4567')
test3 = r.match('063-857-4567')

print(test1, test2, test3, sep='\n')
```

~~~
<re.Match object; span=(0, 13), match='010-1111-3333'>
<re.Match object; span=(0, 11), match='02-855-4567'>
<re.Match object; span=(0, 12), match='063-857-4567'>
~~~

compile 을 이용하여 패턴을 저장해 놓고 객체를 생성하면, 해당 객체에서 문자열만 match 하면 판단 완료 (search 또한 가능)
