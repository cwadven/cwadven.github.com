---
title: "[알고리즘 프로그래머스] 체육복 (LEVEL 1:탐욕법)"
tag:
- 알고리즘
- 프로그래머스 LEVEL1
categories:
- algorithm
---

# (문제) 체육복 [탐욕법]
---

점심시간에 도둑이 들어, 일부 학생이 체육복을 도난당했습니다.

다행히 여벌 체육복이 있는 학생이 이들에게 체육복을 빌려주려 합니다.

학생들의 번호는 체격 순으로 매겨져 있어, 바로 앞번호의 학생이나 바로 뒷번호의 학생에게만 체육복을 빌려줄 수 있습니다.

예를 들어, 4번 학생은 3번 학생이나 5번 학생에게만 체육복을 빌려줄 수 있습니다.

체육복이 없으면 수업을 들을 수 없기 때문에 체육복을 적절히 빌려 최대한 많은 학생이 체육수업을 들어야 합니다.


전체 학생의 수 n, 체육복을 도난당한 학생들의 번호가 담긴 배열 lost, 여벌의 체육복을 가져온 학생들의 번호가 담긴 배열 reserve가 매개변수로 주어질 때, 체육수업을 들을 수 있는 학생의 최댓값을 return 하도록 solution 함수를 작성해주세요.


> **입력설명**

전체 학생의 수는 2명 이상 30명 이하입니다.

체육복을 도난당한 학생의 수는 1명 이상 n명 이하이고 중복되는 번호는 없습니다.

여벌의 체육복을 가져온 학생의 수는 1명 이상 n명 이하이고 중복되는 번호는 없습니다.

여벌 체육복이 있는 학생만 다른 학생에게 체육복을 빌려줄 수 있습니다.

여벌 체육복을 가져온 학생이 체육복을 도난당했을 수 있습니다.

이때 이 학생은 체육복을 하나만 도난당했다고 가정하며, 남은 체육복이 하나이기에 다른 학생에게는 체육복을 빌려줄 수 없습니다.

**첫번째 입력은 학생의 수, 두번째 입력은 체육복을 잃어버린 학생들, 세번째 입력은 예비로 체육복을 가지고 있는 학생들**

> **출력설명**

체육수업을 들을 수 있는 학생의 최댓값을 return 하도록 solution 함수를 작성해주세요.

> **테스트케이스**
 

| 입력예제 | 출력예제 |
| -------- | -------- | 
| 5	[2, 4]	[1, 3, 5] | 5 | 
| 5	[2, 4]	[3] | 4 | 
| 3	[3]	[1] | 2 | 

---
# 해결방법

1. 체육복을 가지고 있는 학생 수를 먼저 구한다. -> 전체 학생 수 - (체육복을 잃어 버린 학생 수)

2. 여벌 체육복을 가져온 학생이 체육복을 도난 당했을 경우 자신이 그 여벌 복을 사용해야 하기 때문에 도난 당한 체육복을 중에서 여벌옷을 가져온 학생이 있으면 해당 학생의 여벌옷을 제거 시키고, 체육복을 가지고 있는 학생 수를 + 1 증가 시킨다.<br>
또한 여벌옷을 사용하여 옷을 도난 당한 학생의 정보가 들어있는 리스트에서 여벌옷을 입었기 때문에 그 학생 정보를 도난 당한 리스트에 지우기 위해 새로운 리스트를 만들어 리스트에 삽입한다.

3. 2번을 다 완료 했을 경우 지우기 위한 리스트에서 반복문을 이용하여 도난을 당한 학생의 리스트에 있는 학생과 같으면 도난을 당한 학생의 정보를 도난을 당한 리스트에서 제거 시킨다.

4. 이제 남은 체육복을 도난 당한 학생의 정보가 남아 있는데, 문제에서 자신의 -1 혹은 +1의 학생에게만 체육복을 빌릴 수 있으니, 여벌의 체육복을 가지고 있는 학생의 리스트의 값 중, 도난을 당한 학생의 + 1 학생이 있을 경우 체육복을 가지고 있는 학생 수를 + 1 증가 시키고 빌려 주었으므로 여벌의 체육복을 가지고 있는 리스트에서 해당 빌려준 학생의 값을 제거한다. 만약 학생의 - 1 학생이 체육복을 가지고 있으면 그 학생에게 빌렸으므로 여벌의 체육복을 가지고 있는 학생의 정보 중 학생의 - 1의 학생 정보를 제거하며 체육복을 가지고 있는 학생 수를  + 1 증가 시킨다.

5. 체육복을 가지고 있는 학생 수를 출력한다.


---

# 코드
```python
def solution(n, lost, reserve):
    # 초기 옷을 기본으로 가지고 있는 사람 수
    count = n - len(lost)
    # 인덱스가 샥 사라지니 지우기 위한 장소를 저장
    later_delete = []
    
    # 자기 자신의 옷이 없을 경우
    # 하지만 자기 자신이 예비 옷을 기지고 있을 경우
    for i in lost:
        if (i in reserve):
            later_delete.append(i)
            reserve.remove(i)
            count = count + 1
            
    for i in later_delete:
        lost.remove(i)
            
    
    # 예비 옷이 만약 내 오른쪽 사람이 가지고 있을 경우
    for i in lost:
        if (i+1 in reserve):
            reserve.remove(i+1)
            count = count + 1
        elif (i-1 in reserve):
            reserve.remove(i-1)
            count = count + 1
            
    return count
```
