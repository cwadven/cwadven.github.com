---
title: "[알고리즘] 후위표기식 만들기 (Stack)"
tag:
- 알고리즘
- 스택
- stack
categories:
- algorithm
- python
---

# (문제) 후위표기식 만들기
---
**중위표기식**이 입력되면 **후위표기식**으로 변환하는 프로그램을 작성하는 것.

> **중위표기식** :
> 연산자가 피연산자 사이에 있는 것.

예) 3+5x2  (우리가 일반적으로 이용하는 수학적 연산 방법)

> **후위표기식**:
> 연산자가 피연산자 뒤에 있는 것.

예) 3+5x2  --> 352x+

아래의 그림과 같이 연산자를 피연산자 끼리 우선 순위에 따라 연산자를 뒤로 보내는 방식이다.

![]({{ 'assets/images/algorithm/postfix_expression/postfix_expression1.PNG' | relative_url }})

>  **입력설명**  

첫 줄에 중위표기식이 주어진다. 길이는 100을 넘지 않는다.
식은 1~9의 숫자와 +, -, *, /, (, ) 연산자로만 이루어진다.

>  **출력설명**  

후위 표기식을 출력한다


> **테스트케이스**

(**예제들과 다르게 곱하기는 x가 아닌 *로 사용한다**)

| 입력예제 | 출력예제 |
| -------- | -------- |
| 3+5x2/(7-2)     | 352x72-/+     |
| 3x(5+2)-9     | 352+x9-     |
| (3+5)x2     | 35+2x     |
| 5+7x3-5+(3+2x3)     | 573x+5-323x++     |
| 5+8+6x5-(3+2)-7x3-5+(3+2x3)     | 58+65x+32+-73x-5-323x++     |

---
# 해결방법
수식을 문자열로 입력을 받아와서 받아온 문자열을 반복문으로 순회를 돌린다.

### (조건)
* `숫자`일 경우 결과 값을 나타낼 `res` 변수에 문자를 붙인다.
* `'('` 일 경우 연산자를 저장하는 `stack`이라는 리스트에 `'('`를 저장한다.
* 순회 시, 연산자가 `'*'`, `'/'` 일 경우, 연산자를 저장하는 `stack`이라는 리스트 안의 요소중 마지막 요소가 `'*'` 혹은  `'/'`이면 `stack` 마지막 요소를 pop 시켜서 해당 pop된 값을 `res` 변수 안에 연산자를 붙인다.
* 그 후에 연산자를 `stack`리스트 안에 삽입.
* 순회 시, 연산자가 `'+'`, `'-'` 일 경우, 연산자를 저장하는 `stack`이라는 리스트 안의 요소중 마지막 요소가 `'('` 를 제외하고 다른 것이면 `stack` 마지막 요소를 pop 시켜서 해당 pop된 값을 `res` 변수 안에 연산자를 붙인다.
(`stack`안에 값이 존재하고 `'('`가 아닐 때까지 반복)
* 그 후에 연산자를 `stack`리스트 안에 삽입.
* 순회 시, 연산자가 `')'` 일 경우, 연산자를 저장하는 `stack`이라는 리스트 안의 요소중 마지막 요소가 `'('` 를 제외하고 다른 것이면 `stack` 마지막 요소를 pop 시켜서 해당 pop된 값을 `res` 변수 안에 연산자를 붙인다.
(`stack`안에 값이 존재하고 `'('`가 아닐 때까지 반복)
* 그 후에 연산자를 `stack`리스트 가장 나중에 들어온 값을 pop
(`'('`를 `stack`리스트에서 삭제하기 위해서)

## 동작 시각화
> **예제) 3+5x2/(7-2)**

![]({{ 'assets/images/algorithm/postfix_expression/postfix_expression2.PNG' | relative_url }})

![]({{ 'assets/images/algorithm/postfix_expression/postfix_expression3.PNG' | relative_url }})

![]({{ 'assets/images/algorithm/postfix_expression/postfix_expression4.PNG' | relative_url }})

![]({{ 'assets/images/algorithm/postfix_expression/postfix_expression5.PNG' | relative_url }})

![]({{ 'assets/images/algorithm/postfix_expression/postfix_expression6.PNG' | relative_url }})

![]({{ 'assets/images/algorithm/postfix_expression/postfix_expression7.PNG' | relative_url }})

![]({{ 'assets/images/algorithm/postfix_expression/postfix_expression8.PNG' | relative_url }})

![]({{ 'assets/images/algorithm/postfix_expression/postfix_expression9.PNG' | relative_url }})

![]({{ 'assets/images/algorithm/postfix_expression/postfix_expression10.PNG' | relative_url }})

![]({{ 'assets/images/algorithm/postfix_expression/postfix_expression11.PNG' | relative_url }})

![]({{ 'assets/images/algorithm/postfix_expression/postfix_expression12.PNG' | relative_url }})

![]({{ 'assets/images/algorithm/postfix_expression/postfix_expression13.PNG' | relative_url }})

![]({{ 'assets/images/algorithm/postfix_expression/postfix_expression14.PNG' | relative_url }})

![]({{ 'assets/images/algorithm/postfix_expression/postfix_expression15.PNG' | relative_url }})

---

# 코드
```python
# 식 입력예제 값
a = input()
# 연산자 저장하는 스택
stack = []
# 결과값 저장
res = ''

# 순회하기
for x in a:
    # 숫자일 경우 결과값에 바로 붙이기
    if x.isdecimal():
        res += x
    # 숫자가 아닐 경우
    else:
        # '(' 일 경우 stack에 그냥 넣기
        if x == '(':
            stack.append(x)
        elif x == '*' or x == '/':
	# 우선 순위가 높은 *와 /는 같은 *와 /가 일 경우에만 pop을 한다. 그 후 해당 연산자를 넣는다
            while stack and (stack[-1] == '*' or stack[-1] == '/'):
                res += stack.pop()
            stack.append(x)
        elif x == '+' or x == '-':
	# 우선 순위가 낮은 +와 -는 '('전 까지 모든 연산자를 pop을 한다. 그 후 해당 연산자를 넣는다
            while stack and stack[-1] != '(':
                res += stack.pop()
            stack.append(x)
        elif x == ')':
	# ')'일 경우 '(' 전 까지 모든 연산자를 pop 시키고 마지막에 '('또한 pop 따로 시킨다
            while stack and stack[-1] != '(':
                res += stack.pop()
            stack.pop()

# stack안에 연산자가 남아있을 경우 pop를 하여 모든 것을 빼서 res에 붙인다
while stack:
    res += stack.pop()

print(res)
```
