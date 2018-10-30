---
layout: dark-post
title: 안드로이드 - 액티비티 생명주기(Life Cycle)
date: 2018-10-02
author: Geunsu Heo
categories: [android]
tags: [android]
sitemap:
  changefraq: daily
  priority: 1.0
---

## 생명주기(Life Cycle)
- 액티비티가 실행부터 종료까지 많은 상태 변화를 거치며 시스템이 상태에 따라 메소드를 호출한다.
1. 활성(activity running) : 액티비티가 화면에 출력되어 있으며 포커스를 가지고 있어 사용자 이벤트에 반응할 수 있음.
2. 일시 정지(pause) : 화면에 보이지만 포커스를 잃은 상태
3. 비활성(stop) : 다른 액티비티에 의해 완전히 가려진 상태  

- 생명주기 그래프  
![Life Cycle](https://kairo96.gitbooks.io/android/content/pic2/2-4-1-1.jpg)
---

1. 활성 상태
	- 생성된 액티비티는 onCreate() -> onStart() -> onResume() 메소드가 호출되면서 활성 상태가 된다.
	- 이 3개의 메소드 안에서 setContentView()를 이용하여 액티비티 화면을 출력한다.
		- 이때 setContentView()의 호출 시점은 화면 출력 순간이 아니라, onResume()까지 실행 후이다.
		- setContentView()를 반복해서 호출하면 마지막 호출된 내용만 출력된다.
		- 무언가를 출력하고 다음에 추가로 출력하고 싶다면 addContentView()를 이용한다.

2. 일시 정지 상태
	- 일시 정지 상태로 멈출 때도 있지만 대부분 정지 상태로 전환되기 전에 호출되어 곧 정지될 것임을 알리기 위해 사용
	- onPause() 호출
	- onPause()에 구현할 내용
		- 애니메이션이나 CPU 소비를 야기할 수 있는 기타 지속적인 작업정지
		- GPS와 같은 센서값 수신, 서버 네트워킹 등 액티비티가 일시 정지된 동안 불필요한 동작 정지  

3. 비활성 상태
	- 다른 액티비티로 화면이 전환되어 안 보이는 경우
	- onPause() -> onstop() 까지 호출
	- 화면을 가렸던 액티비티가 사라지면 다시 활성상태로 돌아오는데 이때는 onRestart() -> onStart() -> onResume() 메서드가 호출  

---
## 액티비티 상태 저장
액티비티 내에 많은 데이터가 유지되며 화면에 출력되다가 종료되면 모두 유실된다. 이런 데이터를 저장하는 방법이다.

### 예) 화면 회전
- onResume() 메서드까지 호출된 액티비티가 회전하면 onPause() -> onStop() -> onDestory() 메서드까지 호출되어 종료된다.
- 그리고 시스템에 의해 다시 호출되어 onCreate() -> onStart() -> onResume() 까지 호출된다.
	- 이때 별 문제가 없어보이지만 사용자 이벤트나 네트워킹으로 데이터가 발생 시 모두 유실된다.

---
### 저장하는 법
액티비티가 종료될 때 유실되면 안 되는 데이터를 저장했다가 다시 액티비티가 시작될 때 복원하여 사용하기 위한 **생명주기 메서드**가 있다.

onResume()까지 실행된 액티비티가 화면 회전 시
- onPause() -> **onSaveInstanceState()** -> onStop() -> onDestory()가 호출된 후
- 다시 시작하면서 onCreate() -> onStart() -> **onRestoreInstanceState()**-> onResume()가 실행된다.
전에 언급한 내용과 달리 추가된 메서드들이 상태 저장, 복원을 위한 생명 주기 메서드이다.

### 데이터 저장 onSaveInstanceState(Bundle)
```java
@Override  
public void onSaveInstanceState(Bundle outState){  
super.onSaveInstanceState(outState);  
outState.putString("data1","hello");  
outState.putInt("data2",100);  
}  
```
- onPause()후 자동 호출되며 데이터를 저장한다.
- 저장 시 Bundle 객체를 이용하여 (key-value)쌍으로 묶어서 저장

---
### 데이터 복원 onRestoreInstanceState(Bundle)
```java
@Override
public void onRestoreInstanceState(Bundle State){
super.onRestoreInstanceState(State);
String data1 = State.getString("data1");
int data2 = State.getInt("data2");
}
```
- 액티비티가 다시 시작되는 시점에서 호출
- 저장된 데이터를 Bundle에 담아 매개변수로 전달된다.
- Bundle에서 데이터를 가져올때 get"자료형"()을 사용하며 key값을 통해 value를 가져올 수 있다.

- API 21 버전부터 매개변수가 2개로 바뀌었다.
	- 매개변수 : Bundle, PersistableBundle
	- 차이점
		- onSaveInstanceState() : 액티비티가 종료되어야만 할 때만 호출
		- onRestoreInstaceState() : Bundle에 저장된 데이터가 없을 시 호출되지 않음.

---
### 참고도서
- 깡샘의 안드로이드 프로그래밍
