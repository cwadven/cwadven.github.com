---
title: "[알고리즘] 후위식 연산 (Stack)"
tag:
- stack
- 스택
- 알고리즘
categories:
- algorithm
---

# (문제) 후위식 연산
---
후위연산식이 주어지면 연산한 결과를 출력하는 프로그램을 작성하세요.
만약 3x(5+2)-9 을 후위연산식으로 표현하면 352+x9- 로 표현되며 그 결과는 21입니다.

> **입력설명**

첫 줄에 후위연산식이 주어진다.
연산식의 길이는 50을 넘지 않는다.
식은 1~9의 숫자와 +, -, *, /, (, ) 연산자로만 이루어진다.

> **출력설명**

연산한 결과를 출력

> **테스트케이스**

(예제들과 다르게 곱하기는 x가 아닌 *로 사용한다)

| 입력예제 | 출력예제 | 
| -------- | -------- | 
| 352+x9-     | 12     |
| 35+2x     | 16     |
| 573x+5-323x++     | 30     |
| 58+65x+32+-73x-5-323x++     | 21     |
| 58+65x+32+-73x-5-323x++53+2+52x-+3+     | 24     |

---
# 해결방법
입력받은 수식을 반복문을 통해 순회하여 **숫자**는 `stack`이라는 리스트에 저장하고 **연산자**는 `stack`에 저장된 요소를 뽑아서 연산 후 다시 `stack`에 넣는다.

## 동작 시각화
> **예제) 352+x9-**
 
 ![]({{ 'assets/images/algorithm/postfix_expression_reverse/postfix_expression_reverse1.PNG' | relative_url }})
 
 ![]({{ 'assets/images/algorithm/postfix_expression_reverse/postfix_expression_reverse2.PNG' | relative_url }})

![]({{ 'assets/images/algorithm/postfix_expression_reverse/postfix_expression_reverse3.PNG' | relative_url }})

![]({{ 'assets/images/algorithm/postfix_expression_reverse/postfix_expression_reverse4.PNG' | relative_url }})

![]({{ 'assets/images/algorithm/postfix_expression_reverse/postfix_expression_reverse5.PNG' | relative_url }})

![]({{ 'assets/images/algorithm/postfix_expression_reverse/postfix_expression_reverse6.PNG' | relative_url }})

![]({{ 'assets/images/algorithm/postfix_expression_reverse/postfix_expression_reverse7.PNG' | relative_url }})

![]({{ 'assets/images/algorithm/postfix_expression_reverse/postfix_expression_reverse8.PNG' | relative_url }})

---

# 코드
```python
a = input()
stack = []

for x in a:
    if x.isdecimal():
        stack.append(int(x))
    else:
        if x == '+':
            # 슬라이싱으로 바꾸기
            stack[-2:] = [stack[-2] + stack[-1]]
        elif x == '-':
            stack[-2:] = [stack[-2] - stack[-1]]
        elif x == '*':
            stack[-2:] = [stack[-2] * stack[-1]]
        elif x == '/':
            stack[-2:] = [stack[-2] / stack[-1]]

print(stack[0])
```
