---
layout: dark-post
title: 파이썬 강의 - 집합
date: 2018-10-30
author: Geunsu Heo
categories: [python lecture]
tags: [python,lecture]
sitemap:
  changefraq: daily
  priority: 1.0
---

---
## 집합 자료형
- 2.3버전부터 지원되기 시작하였으나 그리 많이 사용되어지진 않는다.
- 중복과 순서가 없다.
- 중괄호(`{}`) 안에 요소들을 콤마로 나열하거나 `set()`으로 만든다.

```python
a = {1,2,3,1} 
print(a) # {1,2,3}
b = set([1,2,3,1])
print(b) # {1,2,3}
```

---
### 집합 자료형 활용
집합 자료형은 수학적 연산인 합집합, 교집합, 차집합을 구할 때 활용된다.

#### 합집합 |
기호 `|`혹은 함수 union()을 사용한다.
```python
a = {1,2,3} 
b = {2,3,4}
print(a | b) # {1, 2, 3, 4}
print(a.union(b)) # {1, 2, 3, 4}
```

#### 교집합 &
기호 `&`혹은 함수 intersection()을 사용한다.
```python
a = {1,2,3} 
b = {2,3,4}
print(a & b) # {2, 3}
print(a.intersection(b)) # {2, 3}
```

#### 차집합 -
기호 `-`혹은 함수 difference()를 사용한다.
```python
a = {1,2,3} 
b = {2,3,4}

print(a - b) # {1}
print(a.difference(b)) # {1}

print(b - a) # {4}
print(b.difference(a)) # {4}
```

---
### 집합 관련 함수
#### 값 1개 추가 - add()
```python
a = {1,2,3} 
a.add(4)
print(a) # {1, 2, 3, 4}
a.add(1)
print(a) # {1, 2, 3, 4}
```

#### 값 여러 개 추가 - update()
```python
a = {1,2,3} 
a.update([4,5])
print(a) # {1, 2, 3, 4, 5}
a.update([5,6])
print(a) # {1, 2, 3, 4, 5, 6}
```

#### 값 제거 - remove()
```python
a = {1,2,3} 
a.remove(2)
print(a) # {1, 3}
```

---
### 참고자료
[점프 투 파이썬](https://wikidocs.net/1015)  
`모두를 위한 파이썬 PY4E`
