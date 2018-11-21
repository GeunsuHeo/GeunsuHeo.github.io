---
layout: dark-post
title: 파이썬 강의 - 파일 입출력
date: 2018-11-21
author: Geunsu Heo
categories: [python lecture]
tags: [python,lecture]
sitemap:
  changefraq: daily
  priority: 1.0
---

---
## 파일 입출력
프로그래밍을 배우면서 절대 빠질 수 없는 것 중 하나가 파일 입출력이다. 파일을 읽고 쓸 줄 알아야 우리가 원하는 데이터를 가져오고 완성된 데이터를 파일로 저장하는 것이 프로그래밍을 하면서 필수적으로 느껴질 것이다. 우리는 파일 입출력 중에서 가장 간단하고 기본적인 텍스트 파일(.txt)을 읽고 쓰고 추가하는 방법에 대해서 배운다.
```python
f = open('./text.txt','w')
print(f) # <_io.TextIOWrapper name='./text.txt' mode='w' encoding='cp949'>
f.close()
```
위에서 open()함수로 만들어 낸 f는 파일을 읽고 가져올 수 있는 기능을 하는 하나의 객체이다. 아직 객체를 배우지 않았으니 이 f라는 것은 파일을 읽고 쓸 수 있도록 해주는 기능을 하는 정도만 이해하자.
open()함수를 다음과 같이 사용할 수 있다.
```
f = open("경로/파일명","모드")
```
그리고 파일입출력 사용이 끝났다면 이를 닫아 주어야한다.
```
f.close()
```
### 모드
open()의 파일 모드에는 3가지가 있다.
- **r** : 읽기모드 (read)
- **w** : 쓰기모드 (write)
- **a** : 추가모드 (add)

읽기모드를 사용하면 존재하는 파일을 읽을 수 있다. 이때 경로나 파일이 존재하지 않는다면 오류가 발생한다.
쓰기모드를 사용하면 파일을 쓸 수 있으며 이전에 파일이 있다면 덮어쓰기를 하여 이전 파일이 사라진다.
추가모드를 사용하면 이전에 있던 파일 뒷 부분부터 추가서 쓸 때 사용한다.

### 경로와 파일명
파일 입출력에서 기본적인 요소를 뽑자면 경로와 파일명에 대해서 이해해야한다.
#### 경로(path)
경로란 절대경로와 상대경로로 나뉘며 파일이 존재하는 위치를 말한다. 즉, 우리가 C드라이브 안에 python36이라는 폴더 안에 있는 data 폴더 안에 있는 text.txt의 경로는 `c:/python36/data`이다. 이처럼 처음부터 끝까지 이 파일이 어디에 존재하는 지를 말해주는 것이 절대경로이다.
반면 상대경로는 우리가 지금 사용하는 .py파일이 있는 폴더를 기준으로 text.txt가 있는 곳을 알려주는 것이다. 만약 우리의 .py파일이  `c:/python36`에 있다면 text.txt의 경로는 `./data`로 나타낼 수 있다. 즉 경로 앞에 있는`./`표시가 지금 현재 .py파일이 존재하는 상대경로를 뜻하며 이는 생략이 가능하다.
그렇다면 만약 .py파일을 새로운 경로인 `c:/python36/main`이라는 경로로 옮겼다고 하자. 그렇다면 상대경로로 text.txt를 찾는 방법은 무엇일까? 바로 상위 폴더로 이동을 의미하는 점 두 개 `..`를 사용하는 것이다. 이 점 두 개로 상위폴더로 이동할 수 있으며 `c:/python36/main`에서 `c:/python36`을 가져올 수 있고 이를 다시 `c:/python36/data`라는 경로로 이동해주면 text.txt가 있는 경로로 가져올 수 있다. 이를 상대경로로 나타내면 `./../data`과 같다.
#### 파일명(filename)
파일명은 경로를 이해하면 쉽다. 단순히 파일명이다. 반드시 파일명과 확장자를 같이 사용해야하며 만약 text.txt를 읽기 위해 파일명만 입력하면 text.txt의 텍스트파일이 아닌 text이라는 일반 파일을 읽으려고 시도하므로 반드시 확장자를 붙여주도록 하자 그리고 무엇보다 중요한 건 `경로명+'/'+파일명`으로 사용해야한다는 것이다. 중간에 구분자인 `/`를 적는 것을 잊으면 안된다.
#### 경로 구분자(/ or \\)
경로 구분을 슬래시(/)냐 역슬래시(\\)이냐는 파이썬에서는 구분을 하지 않는다. 실제로 두 개를 혼용하여 사용해도 정상적으로 작동한다. 하지만 엄격히 구분하자면 개발하고 있는 OS마다 구분자가 다르므로 os모듈에 있는 **os.sep**을 사용하여 구분해주어야 한다. 따라서 `경로명+os.sep+파일명`으로 파일 입출력을 하는 것이 좋다.

---
### 파일 쓰기 (쓰기모드)
이제 파일입출력을 연습해보자. 먼저 파일 객체를 만들고 쓸 준비를 하자.
```python
f = open("./text.txt","w")
```
그리고 `f.write(파일에 쓸 문자열)`을 입력하여 파일에 출력해보자. 이때 print()처럼 자동으로 줄바꿈이 되지 않으므로 줄바꿈을 하고 싶다면 줄바꿈 특수문자인 `/n`을 사용하자.
```python
f = open("./text.txt","w")
f.write("Hello World!! \n")
f.write("I'm python \n")
f.close()
```
test.txt 내용
```
Hello World!!
I'm python
```

---
### 파일 읽기 (읽기모드)
다음은 파일 읽기이다. 파일과 경로는 반드시 존재해야하며 존재하지 않으면 오류가 발생하므로 이 점을 주의하자 파일을 읽는 함수는 한 줄씩 읽는 `readline()`과 전부 읽는 `readlines()`이다.
먼저 한 줄씩 읽는 `readline()`부터 사용해보자 이 함수는 한 줄을 읽고 다음 줄을 읽을 준비를 하는 함수이다. 즉, 첫 번째 호출때는 첫 번째 줄을, 두 번째 호출 때는 두 번째 줄을 읽어간다.
```python
f = open("./text.txt","r")
print(f.readline())
print(f.readline())
f.close()
```
```
Hello World!!

I'm python
```
그렇다면 이 파일에 몇 줄의 텍스트가 들어있을 지 모르는 경우가 대부분일텐데 전부 읽는 방법은 무엇일까? 바로 무한루프를 사용하는 것이다. readline()함수는 읽을 것이 없다면 빈 문자열을 리턴한다. 따라서 묵시적 논리형인 빈 문자열 = False임을 이용하여 탈출조건을 결정하면 된다.
```python
f = open("./text.txt","r")
while True:
  line = f.readline()
  if not line:
    break
  print(line)
f.close()
```
#### readlines()
위 방법처럼 readline()로 모든 문자를 읽을 수 있지만 readlines()를 이용하여 모든 문자열을 가져올 수 있다.
```python
f = open("./text.txt","r")
lines = f.readlines()
print(lines) # ['Hello World!! \n', "I'm python \n"]
f.close()
```
다만 특이한 점이 각 줄을 리스트의 요소들로 넣는다는 것이다. 따라서 모든 문자를 출력하기 위해서는 for문을 사용하는 것이 가장 쉬운 방법일 것이다.
```python
f = open("./text.txt","r")
lines = f.readlines()
for line in lines:
  print(line, end="")
f.close()
```
```
Hello World!!
I'm python
```

---
### 추가모드 (a)
다음은 추가모드이다. 이미 있는 파일 뒤에 입력을 하는 모드이다. 이 또한 추가할 파일이 존재해야한다. 위 예제에서 사용한 text.txt를 그대로 사용해보자. 추가모드도 쓰기모드와 마찬가지로 write()함수를 사용한다.
```python
f = open("./text.txt","a")
f.write("New Line be added after saving")
f.close()
```
```
Hello World!!
I'm python
New Line be added after saving
```

---
### with as 블럭
우리가 파일 입출력을 할 때 반드시 open()후 close()가 있어야 한다고 하였다. 만약 파일 입출력을 잠시 썼다가 끄는 반복적인 경우나 가독성을 좀 더 주고싶다면 with as 블럭을 사용한다. 이 블럭 내에서 만든 open()함수는 블럭이 끝나면 자동으로 닫힌다. 이를 한 번 이용하여 보자.
```python
f = open("./text.txt","r")
while True:
  line = f.readline()
  if not line:
    break
  print(line)
f.close()
```
기존 코드를 with as 블럭으로 구현하면 아래와 같다.
```python
with f as open("./text.txt","r"):
  while True:
    line = f.readline()
    if not line:
      break
    print(line)
```
이 블럭은 블럭 내에서만 파일입출력을 사용할 때 가독성을 높히고 close()함수의 번거러움을 해소할 수 있다. 

---
#### 예제 1
반복문에서 구현했던 구구단을 텍스트 파일로 출력하여보자.

#### 예제 2
예제 1처럼 구구단을 텍스트 파일로 출력하는데 2단 ~ 9단을 각 단별로 홀수단은 홀수단끼리 짝수단은 짝수단끼리 텍스트파일로 출력하시오.

#### 예제 3
다음은 CNN에서 발췌한 구문이다. 이 구문을 텍스트 파일로 만들고 사용자로부터 하나의 알파벳을 입력받아 알파벳을 포함하는 구문을 텍스트파일로 출력하시오. 단, 대소문자 구분없음.
```
It showed a President willing to ignore and prejudge US intelligence assessments that conflict with his political goals.
His readiness to offer impunity to Saudi Arabia represented another blow to the international rule of law and global accountability, concepts Trump has shown little desire to enforce in nearly two years in office.
```

#### 예제 4
파일을 출력할 때마다 파일명을 다르게 하여 텍스트파일의 덮어쓰기를 막을 수 있다. 이때 time.localtime()을 사용하여 현재의 시간을 가져올 수 있는 것을 이용하여 파일을 초 단위로 출력할 때 파일명이 다르게 출력되는 프로그램을 작성하시오.
```python
import time
today = time.localtime()

print(today.tm_hour) # 현재 시간
print(today.tm_min) # 현재 분
print(today.tm_sec) # 현재 초
```


#### 예제 심화 - word count
다음은 CNN에서 발췌한 구문이다. 이 구문에서 모든 숫자, 공백, 첨자, 특수기호들을 제외, 대소문자 구별 없이 나온 단어의 수를 세는 것이다. 이 때 3번 이상 나온 단어들을 사전적으로 오름차순으로 출력하시오. 단, 복수형처럼 문법적인 변형은 고려하지 않는다. (like != likes)
```
The gloom-and-doom on Wall Street has wiped out the stock market's gains for the year.
The Dow dropped 552 points, or 2.2%, on Tuesday. Plunging retailers like Target (TGT) and Kohl's (KSS) led the S&P 500 1.8% lower.
Tech stocks once again got hit hard, with the Nasdaq sinking 1.7%. Apple retreated another 5% after Goldman Sachs dimmed its price target on the iPhone maker for the second time in a week.
All three major indexes have given up their gains on the year. The Dow is nearly 2,500 points off its peak.
"The highways will be crowded this evening as the Thanksgiving rush will begin in earnest, but this morning investors are rushing for the exits," Paul Hickey, co-founder of Bespoke Investment Group, wrote to clients on Tuesday.
The Dow lost nearly 400 points on Monday as well. This week's sell-off marks a continuation of a glum two months on Wall Street. The S&P 500 is down nearly 10% from its record high, flirting with official correction territory.
The losses have been sparked by a flurry of concerns about everything from higher interest rates and crashing oil prices to the US-China trade war. But the overarching theme is that investors are bracing for the end of the fantastic economic and profit growth that marked the past year. Analysts expect a deceleration in 2019 driven by tariffs, the fading impact of the tax cuts and higher borrowing costs caused by the Federal Reserve.
"Put simply, stocks have already started to price in the risk of an economic slowdown," Goldman Sachs chief US equity strategist David Kostin wrote to clients on Tuesday.
President Donald Trump said on Tuesday that the US economy is "doing great," but he urged the Federal Reserve to keep interest rates low.
"I think we have much more of a Fed problem than we do with anyone else," Trump told reporters.
Investors continue to flee from the tech darlings that once carried the market higher. Worries about lackluster demand for the latest iPhones have weighed heavily on Apple (AAPL). Other momentum stocks like Netflix (NFLX) and Amazon (AMZN) closed lower again. Google owner Alphabet (GOOGL) closed on Monday in its first bear market since 2011.
All told, the collective market value of Facebook, Amazon, Netflix, Alphabet, Apple and Microsoft has declined by more than $1.1 trillion.
```
