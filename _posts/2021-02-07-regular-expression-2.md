---
title: "[파이썬] 정규표현식 2 ([], *, +, ?, .)"
tag:
- 정규표현식
categories:
- regular_expression
- python
---

> **범위[]  추가 기호 * +**


```python
import re

test1 = re.match('[0-9]', "12345678")
test2 = re.match('[0-9]*', "12345678")
test3 = re.match('[0-9]+', "12345678")
test4 = re.match('[0-9]*', "abc123abc")
test5 = re.match('[0-9]+', "abc123abc")

print(test1, test2, test3, test4, test5, sep='\n')
```

~~~
<re.Match object; span=(0, 1), match='1'>
<re.Match object; span=(0, 8), match='12345678'>
<re.Match object; span=(0, 8), match='12345678'>
<re.Match object; span=(0, 0), match=''>
None
~~~

패턴에 `[]`는 `[0-9]`면 0~9 까지의 숫자 범위 의미이다.

test1의 의미는 1 글자가 0~9 까지 범위의 숫자가 있나? 라고 묻는 것이다.<br>

`[]` 에는 `*` 와  `+` 를 넣을 수 있다 각각 의미하는 바는 다르다.<br>
`*` 는 해당 `[]` 안의 패턴이 없어도 되는 것이고, `+` 는 해당 `[]` 패턴이 1개라도 있어야 한다는 것이다.

test2의 의미는 패턴이(0~9 까지의 범위의 숫자) 문자열의 문자 0개 이상 있는지 판단<br>
test3의 의미는 패턴이(0~9 까지의 범위의 숫자) 문자열의 문자 1개 이상 있는지 판단<br>
test4는 없기 때문에 0 ~ 0 까지라고 알려줌 (즉, 없어도 일단 돌아간다는 의미)<br>
test5는 문자열 1개 이상 패턴과 맞은게 없으니 None 출력 (즉, 1개 이상은 무조건 있어야 한다는 의미)

---

> **범위[]  추가 기호 * + 활용**

```python
import re

test1 = re.match('이*창우', '창우')
test2 = re.match('이+창우', '창우')
test3 = re.match('이*창우', '이이이이창우')
test4 = re.match('이+창우', '이이이이창우')

print(test1, test2, test3, test4, sep='\n')
```

~~~
<re.Match object; span=(0, 2), match='창우'>
None
<re.Match object; span=(0, 6), match='이이이이창우'>
<re.Match object; span=(0, 6), match='이이이이창우'>
~~~

test1 은 패턴의 `*` `'이'` 가 **0개 이상** 이면 되어서 `'창우'` 까지 판단<br>
test2 는 패턴의 `+` `'이'` 가 **무조건 1개 이상** 들어가야해서 `None` 이 뜬다<br>
test3 은 패턴의 `*` `'이'` 가 **0개 이상** 이면 되어서 `'이이이이창우'` 의 `'이이이이'`를 보고 `'창우'` 까지 판단<br>
test4 는 패턴의 `+` `'이'` 가 **무조건 1개 이상** 들어가야해서 `'이이이이창우'` 의 `'이이이이'`를 보고 `'창우'` 까지 판단



> **? 및 . 사용**

```python
import re

test1 = re.match('abc?d', 'abd')
test2 = re.match('ab[0-9]?d', 'ab3d')
test3 = re.match('ab.d', 'abxd')
test4 = re.match('ab.d', 'abd')

print(test1, test2, test3, test4, sep='\n')
```

~~~
<re.Match object; span=(0, 3), match='abd'>
<re.Match object; span=(0, 4), match='ab3d'>
<re.Match object; span=(0, 4), match='abxd'>
None
~~~

? 앞의 문자(범위)가 0개 또는 1개 가 있는지 판단<br>
. 은 . 이 있는 위치에 아무 문자(숫자)가 1개 있는지 판단
