---
layout: dark-post
title: 안드로이드 - 액션바
date: 2018-11-11
author: Geunsu Heo
categories: [android]
tags: [android]
sitemap:
  changefraq: daily
  priority: 1.0
---
---
## ActionBar
액션바는 API Level 11부터 추가된 기능으로 능력이 많은 타이틀 바로 생각하면 된다. 기존에 액티비티를 구성할 때를 보면 기본적으로 ActionBar를 출력을 해주지만 우리가 아무런 구성을 하지 않아 마치 타이틀만 표시되는 '타이틀 바'처럼 보인 것이다. 하지만 이 액션바에 여러가지를 추가할 수 있다.
### 액티비티 화면 구성
액티비티 화면 전체는 Window라 부르며, Window는 크게 Content 영역과 ActionBar영역으로 나뉜다.
- **Content영역:** setCountView()로 출력하는 내용이 출력이 되어 나타나는 곳
- **ActionBar영역:** Window 상단에 출력되며 App Icon, View Control, Action Button, Overflow Meun 등이 나오도록 구성 가능.
<center><img src="https://user-images.githubusercontent.com/11483057/48311730-ae57dd00-e5e7-11e8-9200-ee1835df14af.png" width="50%" height="50%"></center>

### ActionBar구성
- **App Icon** : 앱의 아이콘이 나타나는 부분
- **View Control** : Navigation Mode 지정으로 List Navigation, Tab Navigation을 제공하지만 API Level 21부터 deprecation
- **Action Button** : 사용자 액션을 위한 버튼
- **Overflow Meun** : 표시가능한 버튼이 제한적이므로 표시가 안되는 버튼을 메뉴를 따로 만들어서 나타낸다.

---
### ActionBar 표시하지 않기
ActionBar를 출력하고 싶지 않다면 res/values/styles.xml 파일에 적용되는 테마에서 아래와 같이 지정하면 된다.
```xml
<style name="AppTheme" parent="Theme.AppCompat.Light.DarkActionBar">
    <!-- Customize your theme here. -->
    <item name="colorPrimary">@color/colorPrimary</item>
    <item name="colorPrimaryDark">@color/colorPrimaryDark</item>
    <item name="colorAccent">@color/colorAccent</item>
    <item name="widowNoTitle">true</item>
    <item name="windowActionBar">false</item>
</style>
```
또는 Java 코드에서 ActionBar를 객체로 가져와 show(),hide()를 이용해 사라지거나 나타나게 할 수 있다.
```Java
ActionBar actionBar = getSupportActionBar();
```
```java
@Override
public void onClick(View v){
  if(v==btn1){
    actionBar.show();
  }
  else if(v==btn2){
    actionBar.hide();
  }
}
```
<br>

### ActionBar를 Content 영역에 떠있듯 보이기
ActionBar가 content영역 위에 떠있듯 표현할 수 있다. 이는 테마를 조정하여 구현한다.
- 액션바의 색을 투명하게 한다(#00000000)
- windowActionBarOverlay속성을 true로 한다.

```xml
<style name="AppTheme" parent="Theme.AppCompat.Light.DarkActionBar">
    <!-- Customize your theme here. -->
    <item name="colorPrimary">#00000000</item>
    <item name="colorPrimaryDark">@color/colorPrimaryDark</item>
    <item name="colorAccent">@color/colorAccent</item>
    <item name="windowActionBarOverlay">true</item>
</style>
```

---
### 표시 옵션
ActionBar에서는 App Icon이나 타이틀 문자열 등 여러 항목이 표시되는데 이 요소들을 어떻게 구상을 할 것인지에 대한 함수를 제공한다.
- **AndroidManifest.xml**에서 activity 태그의 label 속성을 설정  

```xml
<activity android:name=".MainActiviy" android:label="상세 보기">
```
위와 같이 지정하면 ActionBar의 타이틀 문자열은 label속성으로 지정한 문자열이 된다. 또한 자바코드의 setter함수를 사용하여 구성요소가 화면에 나와야 하는지를 제어한다.

#### 설정
```Java
actionBar = getSupportActionBar();
actionBar.setDisplayShowHomeEnabled(true); //홈 아이콘 표시 설정
actionBar.setDisplayHomeAsUpEnabled(true); //아이콘을 Up 이미지로 표시 설정
actionBar.setShowCustomEnabled(true); //CustomView 표시 설정
actionBar.setDisplayShowTitleEnabled(true); //타이틀 문자열 표시 설정
actionBar.setDisplayUseLogoEnabled(true); //로고 표시 설정
```

#### 지정
- **setLogo(int resId)** or **setLogo(Drawable logo)** : 로그 지정
- **setTitle(int resId)** or **setTitle(CharSequence title)** : 타이틀 지정
- **setSubtitle(int resId)** or **setSubtitle(CharSequence subtitle)** : 서브타이틀 지정
- **setCustomView(int resId)** or **setCustomView(View view)** : 커스텀 뷰 지정

```Java
actionBar.setIcon(R.drawable.icon); //로고 아이콘 지정
actionBar.setTitle("새로운 타이틀"); //타이틀 지정
actionBar.setSubtitle("새로운 서브타이틀"); //서브타이틀 지정
actionBar.setCustomView(customView); //커스텀 뷰 지정
```

#### 이벤트 처리
아이콘을 클릭했을 때 이벤트를 처리하려면 onOptionsItemSelected()함수 사용.
```Java
@Override
public boolean onOptionsItemSelected(MenuItem item) {
    if(item.getItemId()==android.R.id.home/*지정한 id*/){
      /* 구현할 부분 */
      return true;
    }
    return super.onOptionsItemSelected(item);
}
```

---
### 참고도서
깡샘의 안드로이드 프로그래밍(루비페이퍼,2017)

---
