---
title: "[자료구조] Hash Table (해시 테이블) 란?"
tag:
- hash
- 자료구조
- 해시
categories:
- data_structures
---

# Hash Table (해시 테이블) 이란?

해시 테이블은 **연관배열 구조**로 키(key)에 값(value)을 저장하는 자료구조다.

> **연관배열 구조(associative array)란?**<br>
키(key) 1개와 값(value) 1개가 연관되어 있는 자료구조다. <br>그러므로 키(key)를 이용해 값(value)을 얻을 수 있다.

![](https://upload.wikimedia.org/wikipedia/commons/thumb/b/bf/Hash_table_5_0_1_1_1_1_0_SP.svg/450px-Hash_table_5_0_1_1_1_1_0_SP.svg.png)

출처 - https://ko.wikipedia.org/wiki/해시_테이블 ( 해시 테이블)

해시 테이블은 키(key)에 해시 함수를 이용하여 배열에 index를 적용하고, 해당 index를 활용하여 값(value)을 저장하거나 탐색한다.<br>값이 저장되는 곳을 버킷(bucket)이나 슬롯(slot)이라고 한다.

Python 에서는 `딕셔너리(Dictionary)`가 해시 테이블과 같은 구조이다.

```python
# 딕셔너리 생성
hash_table1 = {"Loved":1, "Love":0}
hash_table2 = dict(Loved=1, Love=0)
hash_table3 = dict([("Loved", 1), ("Love", 0)])

# 전부 {'Loved': 1, 'Love': 0} 출력
print(hash_table1)
print(hash_table2)
print(hash_table3)
```

위와 같은 코드를 통해 해시 테이블과 같은 구조 `딕셔너리` 자료형을 생성할 수 있다.
