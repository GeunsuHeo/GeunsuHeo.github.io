---
layout: dark-post
title: 파이썬 강의 - Bool
date: 2018-10-30
author: Geunsu Heo
categories: [python lecture]
tags: [python,lecture]
sitemap:
  changefraq: daily
  priority: 1.0
---

---
## 불 자료형
참(True)과 거짓(False), 단 두 가지만 나타내는 자료형
- 반드시 첫 글자는 대문자로 사용해야 한다.  

예제들을 통해 살펴보도록 하자
```python
print(1==1) # True
```
```python
print(1>=2) # False
```
```python
print(3>=2) # True
```

---
### 자료형의 참과 거짓
이제까지 배웠던 자료형들의 참과 거짓을 구분지어보자. 각 자료형들은 각각 참과 거짓을 의미하는 형태가 존재한다.
1. 숫  자 : 0은 False, 0이 아닌 모든 수는 True
2. 문자열 : 빈 문자열(`""`)이 False, 비어있지 않은 문자열은 True
3. 리스트 : 빈 리스트(`[]`)가 False, 비어있지 않은 리스트는 True
4. 튜  플 : 빈 튜플(`()`)은 False, 비어있지 않은 튜플은 True
5. 딕셔너리 : 빈 딕셔너리(`{}`)은 False, 비어있지 않은 딕셔너리는 True
6. NoneType : `None`은 거짓

---
### 참고자료
[점프 투 파이썬](https://wikidocs.net/17)  
`모두를 위한 파이썬 PY4E`
