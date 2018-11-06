---
layout: dark-post
title: 파이썬 강의 - 조건문 if
date: 2018-11-06
author: Geunsu Heo
categories: [python lecture]
tags: [python,lecture]
sitemap:
  changefraq: daily
  priority: 1.0
---

## 조건문
조건에 따라 구문을 실행할 지 실행하지 않을 지를 나타내는 문장이다.
```python
if 조건:
  a = 1
  #조건이 True일때 실행되는 문장
else:
  a = 2
  #조건이 False일때 실행되는 문장
```

### 블럭
파이썬의 구문을 블럭 단위로 묶을 때 `탭 혹은 공백4개` 를 사용하여 들여쓰기로 나타낸다.
```python
if 조건1:
  a = 1
  # 탭 혹은 공백 4개로 들여쓰기를 하면
  # if문에 묶이는 블럭이 된다.
a = 2
# 들여쓰기를 하지 않으면 블럭에 들어가지 않는다.
```

---
## 필요한 연산자
if문에서 사용되는 조건은 참과 거짓을 구분짓는 연산자를 많이 사용하며 아래에서는 4가지 연산자를 소개한다.

### 비교 연산자
좌항과 우항을 비교하는 연산자이며 같다, 크다, 작다가 참인지 거짓인지 나타낸다.
- 같다 (`==`)  

```python
print(1==2) # False
print(1==1) # True
```

- 같지 않다. (`!=`)  

```python
print(1==2) # False
print(1==1) # True
```

- 크다 (`>`)

```python
print(1>4) # False
print(1>1) # False
print(4>1) # True
```

- 크거나 같다. (`>=`)

```python
print(1>=4) # False
print(1>=1) # True
print(4>=1) # True
```

- 작다. (`<`)

```python
print(1<4) # True
print(1<1) # False
print(4<1) # False
```

- 작거나 같다. (`<=`)

```python
print(1<=4) # True
print(1<=1) # True
print(4<=1) # False
```

### 논리 연산자
논리 연산자에는 and, or, not이 있으며 좌우항에는 True 혹은 False가 온다.
- and
  - 둘 다 참일 때만 참이고 나머지는 거짓이다.  

```python
print(True and True) # True
print(False and True) # False
print(True and False) # False
print(False and False) # False
```
- or
  - 둘 다 거짓일 때만 거짓이고 나머지는 참이다.  

```python
print(True and True) # True
print(False and True) # True
print(True and False) # True
print(False and False) # False
```

- or
  - True일 경우 False, False일 경우 True이다.

```python
print(not True) # False
print(not False) # True
```

### in 연산자
in 연산자는 좌측 요소가 우측 컬렉션에 속해 있는지를 판단한다.  
- `in` : 있을 때 True 없을 때 False
- `not in` : 없을 때 True 있을 때 False

```python
li = [1,2,3,4]
print(1 in li) # True
print(5 in li) # False
print(1 not in li) # False
print(5 not in li) # True
```

### is 연산자
양측 요소가 같은 객체를 가르키는지를 판단. 여기서는 간단하게 언급만 한다.
> 주의점 : 값이 같다(==)와 같은 객체를 가르키는 것(is)은 다르다. 객체에 대해서는 뒤에서 다룬다.

```python
a = "python is good"
b = "python " + "is good"
print(a == b) # True
print(a is b) #False
```

---
## 조건문의 다양한 형태
조건문의 형태는 대표적으로 if else문, if elif else문이라 할 수 있다.
### if else
if문의 조건이 참이면 if문 안의 구문이, 조건이 거짓이면 else문의 구문이 실행된다. 이때 else문 없이 if문을 단독으로 사용해도 된다.

```python
if 조건:
  print("조건이 참입니다.")
else:
  print("조건이 거짓입니다.")
```
```python
if 조건:
  print("조건이 참입니다.")
```
### if elif else
if문의 조건이 거짓이면 다음 elif의 조건이 참인지 거짓인지 판단하고 참이면 elif의 구문이 거짓이면 넘어간다. 이때 else문은 생략이 가능하지만 맨 처음 if문은 생략이 불가능하다.
```python
if 조건1:
  print("조건1이 참입니다.")
elif 조건2:
  print("조건2가 참입니다.")
else:
  print("조건1,2 둘 다 거짓입니다.")
```
elif는 여러 번 사용할 수 있으며, 그렇다면 아래처럼 구문이 진행된다.
```python
if 조건1:
  print("조건1이 참입니다.")
elif 조건2:
  print("조건2가 참입니다.")
elif 조건3:
  print("조건3이 참입니다.")
else:
  print("조건1,2,3 전부 거짓입니다.")
```

---
### 예제
#### 문제 1 정수가 10이상인가
정수 한 개를 입력받고 그 정수가 10이상인지를 판단하여 아래와 같은 출력결과가 나오도록 프로그램을 작성하시오.
```
정수를 입력하세요 : 11
정수 11은 10이상입니다.
```
```
정수를 입력하세요 : 1
정수 1은 10이상이 아닙니다.
```
#### 문제 2 문자열 포함 문제
문자열을 입력받고 문자열에 a가 포함되어있는지 판단하여 아래와 같은 출력결과가 나오도록 프로그램을 작성하시오.
```
문자열을 입력하세요 : apple
a가 포함되어있습니다.
문자열을 입력하세요 : pie
a가 포함되어있지 않습니다.
```
#### 문제 3 패스워드 문제
처음 입력받은 문자열을 패스워드로 설정하고 다음 입력받은 문자열과 비교하여 패스워드와 같은지를 판단하여 아래와 같은 결과가 나오도록 프로그램을 작성하시오.
```
패드워드를 설정하세요 : apple
패스워드를 입력하세요 : pie
일치하지 않습니다.
```
```
패드워드를 설정하세요 : apple
패스워드를 입력하세요 : apple
패스워드가 일치 합니다.
```
#### 문제 4 등급 매기기
0부터 100까지 점수를 입력하여 80점 이상이면 A, 70~79점이면 B, 50~69점이면 C, 30~49점이면 D, 30점 미만이면 F를 출력하시오.
```
점수를 입력하세요 : 100
등급 : A
```
```
점수를 입력하세요 : 50
등급 : C
```
#### 문제 5 홀짝문제
입력한 정수가 홀수인지 짝수인지 나타는 프로그램을 작성하시오.
```
정수를 입력하세요 : 1
1은 홀수입니다.
```
```
정수를 입력하세요 : 6
6은 짝수입니다.
```
#### 문제 6 (심화) 가위바위보
Alice와 Bob이 가위바위보를 한다. 가위를 0, 바위를 1, 보를 2라고 할때 Alice와 Bob의 각각 가위, 바위, 보를 정수로 입력하여 누가 이겼는지를 출력하시오.
```
Alice (가위 0, 바위 1, 보 2) : 0
Bob   (가위 0, 바위 1, 보 2) : 1
Bob win!
```
```
Alice (가위 0, 바위 1, 보 2) : 1
Bob   (가위 0, 바위 1, 보 2) : 1
draw!
```
```
Alice (가위 0, 바위 1, 보 2) : 2
Bob   (가위 0, 바위 1, 보 2) : 1
Alice win!
```

---
### 참고도서
점프투파이썬
