---
layout: dark-post
title: 안드로이드 - 이벤트 처리
date: 2018-10-30
author: Geunsu Heo
categories: [android]
tags: [android]
sitemap:
  changefraq: daily
  priority: 1.0
---

## 이벤트 처리 이해하기
스마트폰 화면에서 발생하는 사용자 이벤트는 크게 두 가지 모델로 나눌 수 있다.
1. 델리게이트 이벤트 모델 : 뷰에서 발생하는 이벤트를 처리하기 위한 모델
2. 하이어라키 이벤트 모델 : 액티비티에서 발생하는 사용자의 터치나 키 이벤트를 직접 처리하기 위한 모델

---
## 델리게이션 이벤트 모델

### 이벤트 프로그램 구조 
이벤트 소스(Event Source)와 이벤트 핸들러(Event Handler)를 리스너(Listener)로 연결하여 처리하는 구조  
1. 이벤트 소스(Event Source) : 이벤트가 발생한 뷰 객체
2. 이벤트 핸들러(Event Handler) : 이벤트 처리 내용을 가지는 객체
3. 리스너(Listener) : 이벤트 소스와 이벤트 핸들러를 연결하는 작업

모든 뷰의 이벤트는 터치 이벤트로 처리할 수 있지만 조금 더 명료하게 처리하기 위한 것이다. 이벤트가 발생하는 뷰를 직접 지칭하여 각 이벤트의 성격별로 이벤트 이름을 다르게 처리하면 훨씬 명료해진다.

`setOnXXXListener()부분이 이벤트 소스와 이벤트 핸들러를 리스너로 연결하는 부분이다.`


```java
class MyEventHandler implements CompoundButton.OnCheckedChangeListener{
  @Override
  public void OnCheckedChanged(CompoundButton buttonView, boolean isChecked){
    
  }
} 
```

---
## 다양한 이벤트 처리
클릭 이벤트 이외에도 다양한 이벤트를 제공
- OnClickListener : 뷰 클릭 시 발생하는 이벤트
- OnLongClickListener : 뷰를 오래 클릭했을 때 발생하는 이벤트
- OnCheckedChangeListener : CheckBox의 상태 변경 이벤트
- OnItemClickListener : ListView의 항목 선택 이벤트
- OnDateSetListener : DatePicker의 날짜 선택 이벤트
- OnTimeSetListener : TimePicker의 시간 선택 이벤트

#### OnClickListener는 모든 뷰에 적용할 수 있다.
이벤트 종류가 많다고 해도 델리게이션 이벤트 모델만 이해한다면, 이벤트를 처리하는 구조는 같다.  
`이벤트 소스와 이벤트 핸들러를 setOnXXXListener()함수로 연결하고, 이벤트 핸들러는 OnXXXListener를 구현해서 작성`  
대표적인 뷰가 Button이며 Button이외에 TestView, ImageView 등 모든 뷰에 등록할 수 있다.

```java
btn.setOnClickListener(new View.OnClickListener(){
  @Override
  public void onClick(View v){
    
  }
});
```
#### OnLongClickListener
클릭 이벤트와 더불어 모든 뷰에 등록할 수 있다. 뷰를 오래 눌렀을 때 발생하는 이벤트
```java
btn.setOnLongClickListener(new View.OnLongClickListener(){
  @Override
  public boolean onLongClick(View v){
    return false;
  }
});
```  

#### OnCheckedChangeListener
```java
checkbox.setOnCheckedListener(new CompoundButton.OnCheckedChangeListener(){
  @Override
  public void OnCheckedChanged(CompoundButton buttonView, boolean isChecked){
    
  }
});
```

---

## 하이어라키 이벤트(Hierarchy Event Model)
하이어 이벤트 모델은 액티비티가 화면에 출력되었을 때 발생하는 사용자의 키 이벤트와 화면 터치 이벤트를 처리하기 위한 모델  
델리게이션 이벤트 모델처럼 이벤트 소스와 이벤트 핸들러를 리스너로 연결하여 처리하는 구조가 아니다. 이벤트 발생 시 자동 호출 되는 함수만 액티비티 내에 재정의하면 된다.

### 터치 이벤트(Touch Event)
액티비티에 보이는 내용을 사용자가 손가락으로 조작하는 일은 터치 이벤트로 처리한다.
터치 이벤트가 발생할 때 콜백 함수를 액티비티 내에 정의하는 것으로 구현
```java
@Override
public boolean onTouchEvent(MotionEvent event){
  return super.onTouchEvent(event);
}
```
onTouchEvent가 호출되는 터치 이벤트는 3가지가 있으며 이 메서드의 매개변수를 식별하여 사용가능.
1. ACTION_DOWN : 화면에 터치된 순간
2. ACTION_UP : 터치를 떼는 순간
3. ACTION_MOVE : 터치한 후 이동하는 순간

또한 터치 이벤트가 발생한 지점의 x,y좌표값을 얻을 수 있다.  

#### 이벤트가 발생한 뷰 내에서의 좌푯값
- getX()
- getY()  
 
#### 화면에서의 좌표값
- getRawX()
- getRewY()

```java
@Override
public boolean onTouchEvent(MotionEvent event){
  if(event.getAction()==MotionEvent.ACTION_DOWN){
    initX=event.getRawX();
  }
  return true;
}
```
---

### 키 이벤트(Key Event)
사용자가 안드로이드 스마트폰의 키를 눌렀을 때 이벤트 처리. 스마트폰에 보이는 **소프트 키보드(Soft Keyborad)** 는 키 이벤트로 처리할 수 없지만 하드웨어 키보드는 처리 가능.
또한 시스템에서 제공하는 버튼을 처리하는데 사용. 뒤로가기 버튼과 메뉴, 검색, 오버뷰 버튼 등이 제공
- onKeyDown: 키가 눌린 순간의 이벤트
- onKeyUp: 키를 떼는 순간의 이벤트
- onKeyLongPress: 키를 오래 누르는 순간의 이벤트

```java
public boolean onKeyDown(int keyCode, KeyEvent event) {
  if(keyCode==KeyEvent.KEYCODE_BACK){

  }
  return super.onKeyDown(keyCode, event);
}
```
매개변수로 keyCode값이 전달되어 어느 버튼을 누른 건지 식별 가능.

#### onBackPressed()
onBackPressed()함수는 뒤로가기 버튼 제어만을 목적이므로 다른 키는 처리 불가능.
```java
public void onBackPressed() {
  super.onBackPressed();
}
```

---
## 제스처 이벤트(Gesture Event)
터치 이벤트 중에서 스크롤 등을 구별한 후 알려주는 이벤트
GestureDetector 객체를 만들고 터치 이벤트를 전달하면 GestureDetector 객체에서 각 상황에 맞는 메소드를 호출합니다.
- 스크롤(Scroll): 손가락으로 드래그하는 일반적인 경우
- 플링(Fling): 빠른 속도로 스크롤을 하는 경우

---
## 포커스 이벤트(Focus Event)
키를 입력할 때 발생하는 이벤트는 포커스(Focus)를 가진 뷰에게 전달
xml내에서 <selector>태그는 뷰의 상태에 따라 다른 속성을 지정할 수 있도록 한다.
```xml
<?xml version="1.0" encoding="UTF-8"?>
<selector xmlns:android="http://schemas.android.com/apk/res/android">
  <item android:drawable="@drawable/red" android:state_pressed="true" android:state_focused="true"/>
  <item android:drawable="@drawable/red" android:state_pressed="true" android:state_focused="false"/>
  <item android:drawable="@drawable/blue"/>
</selector>
```
---
### 참고자료
깡샘의 안드로이드 프로그래밍(루비페이퍼)
Doit 안드로이드 프로그래밍(이지스)
