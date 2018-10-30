---
layout: dark-post
title: 파이썬 강의 - 튜플
date: 2018-10-30
author: Geunsu Heo
categories: [python lecture]
tags: [python,lecture]
sitemap:
  changefraq: daily
  priority: 1.0
---

---
## 튜플 자료형
1. 튜플은 소괄호( `( )` )로 감싸 요소들을 콤마(,)로 구분하여 순서대로 나열한 자료형이다.
  - 이때 괄호는 생략할 수 있다.

```python
tu1=(1,2,3)
print(tu1) # (1, 2, 3)
tu2=1,2,3
print(tu2) # (1, 2, 3)
tu3=()
print(tu3) # () #빈 튜플
```

2. 리스트와 매우 유사한 자료형이나 리스트와 다르게 변경이 불가능하다.

```python
tu=(1,2,3)
tu[1] = 3
```
```                              
TypeError: 'tuple' object does not support item assignment
```

```python
tu=(1,2,3)
tu.sort()
```

```
AttributeError: 'tuple' object has no attribute 'sort'
```

- 리스트와 차이점 살펴보기
사용 가능한 함수들을 dir()로 찾을 수 있는데 리스트와 튜플의 차이를 살펴보자. 확실히 리스트와 다르게 변경이 불가능하여 사용할 수 있는 함수가 제한되어있다.  

```python
li = []
print(dir(li))
tu = ()
print(dir(tu))
```
```
['append', 'clear', 'copy', 'count', 'extend', 'index', 'insert', 'pop', 'remove', 'reverse', 'sort']
['count', 'index']
```

- 튜플의 장점
  - 리스트와 비교하여 메모리 사용량과 성능 측면에서 훨씬 단순하고 효율적이다.
  
---
### 튜플 인덱싱 및 슬라이싱
튜플의 각각 요소에 접근하는 방법인 인덱싱과 슬라이싱은 리스트와 문자열과 동일하다.
#### 인덱싱

```python
tu=(1,2,3)
print(tu[1]) # 2
```
#### 슬라이싱

```python
tu=(1,2,3,4,5,6)
print(tu[1:3]) # (2,3)
```

---
### 튜플 연산자
튜플의 연산도 문자열, 리스트와 유사하다.
#### 더하기(+) `튜플 + 튜플`
- 두 튜플이 이어진다.

```python
tu1 = (1,2)
tu2 = (3,4)
print(tu1+tu2) # (1, 2, 3, 4)
```
#### 곱하기(\*) `튜플*정수`
- 튜플이 정수만큼 반복해서 연결

```python
tu1 = (1,2)
print(tu1*3) # (1, 2, 1, 2, 1, 2)
```

#### 비교 연산
- 숫자형 자료형에서 사용했던 수학적 비교 연산자들을 튜플에 사용이 가능하다.
- 첫 요소가 같다면 다음 요소를 비교하며 다른 요소가 나타날 때까지 비교

```python
print((0,1,2) > (0,1,3)) #False
print((0,1,2) == (0,1,2)) #True
print((0,1,2) <= (5,1,3)) #True
print(('apple','banana') > ('abs','star')) #True
``` 

---
### 참고자료
`[점프 투 파이썬](https://wikidocs.net/15)`
`모두를 위한 파이썬 PY4E`
