---
layout: dark-post
title: 파이썬 강의 - 딕셔너리
date: 2018-10-30
author: Geunsu Heo
categories: [python lecture]
tags: [python,lecture]
sitemap:
  changefraq: daily
  priority: 1.0
---

---
## 딕셔너리 자료형
이전에 배운 문자열, 리스트, 튜플과 유사하 순서가 아닌 고유의 이름을 가지고 있는 값을 담는 자료형
- 파이썬에서 가장 강력한 데이터 컬렉션
- **키:값** 쌍이 한 개의 요소로 가짐
- 요소들을 **중괄호( `{ }` )** 로 묶음
- 리스트와 다르게 순서가 없고 값을 찾기 위해 **<u>키</u>** 를 사용한다.

```python
dic = {}
dic['age'] = 18
dic['name'] = 'Heo'
dic[1] = 'number'
print(dic) # {'age': 18, 'name': 'Heo', 1: 'number'}
```
|키|값|
|:---:|:---:|
|'age'|18|
|'name'|'Heo'|

---
### 딕셔너리 추가, 삭제
#### 딕셔너리 요소 쌍 추가

```python
dic = {}
dic['age'] = 18
dic['name'] = 'Heo'
dic[1] = 'number'
print(dic) # {'age': 18, 'name': 'Heo', 1: 'number'}
dic['age'] = 20
print(dic) # {'age': 20, 'name': 'Heo', 1: 'number'}
```
위에서 살펴 봤던 예제이다. key와 value를 위와 같이 입력하여 key값에 대한 내용이 없다면 추가, 있다면 변경

#### 딕셔너리 요소 삭제하기
```python
dic = {}
dic['age'] = 18
dic['name'] = 'Heo'
dic[1] = 'number'
print(dic) # {'age': 18, 'name': 'Heo', 1: 'number'}

del dic['age']
print(dic) # {'name': 'Heo', 1: 'number'}
```
이전에 배웠던 del을 사용.

>#### 딕셔너리 만들 때 주의사항
>**Key** 는 고유의 값이어야하며 변하지 않는 값이 들어가야한다. 그래서 튜플은 되지만 리스트는 되지 않는다.

---
### 딕셔너리 관련 함수들
딕셔너리 자료형을 잘 활용할 수 있도록 반드시 관련 함수를 익혀두도록 하자.

#### 키로 값 얻기 - get()
```python
dic = {'age': 18, 'name': 'Heo', 1: 'number'}
print(dic.get('name')) # 'Heo'
```

#### 키 리스트 - keys()
이때 keys()의 결과값은 dict_keys라는 객체이므로 list로 변경해주었다.
```python
dic = {'age': 18, 'name': 'Heo', 1: 'number'}
print(list(dic.keys())) # ['age', 'name', 1]
```

#### 값 리스트 - values()
이때 keys()의 결과값은 dict_values라는 객체이므로 list로 변경해주었다.
```python
dic = {'age': 18, 'name': 'Heo', 1: 'number'}
print(list(dic.values())) # [18, 'Heo', 'number']
```

#### 키:값 쌍 얻기 - items()
이때 items()의 결과값은 dict_items라는 객체이므로 list로 변경해주었다. 
```python
dic = {'age': 18, 'name': 'Heo', 1: 'number'}
print(list(dic.items())) # [('age', 18), ('name', 'Heo'), (1, 'number')]
```

#### 해당 키가 딕셔너리 안에 있는지 조사 - in
```python
dic = {'age': 18, 'name': 'Heo', 1: 'number'}
print('age' in dic) # True
print('id' in dic) # False
```

---
### 참고자료
`[점프 투 파이썬](https://wikidocs.net/16)`  
`모두를 위한 파이썬 PY4E`
