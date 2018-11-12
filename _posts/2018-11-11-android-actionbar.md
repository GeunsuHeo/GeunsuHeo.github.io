---
layout: dark-post
title: 안드로이드 - 액션바와 메뉴
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
또는 java 코드에서 ActionBar를 객체로 가져와 show(),hide()를 이용해 사라지거나 나타나게 할 수 있다.

```java
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
- **AndroidManifest.xml** 에서 activity 태그의 label 속성을 설정

```xml
<activity android:name=".MainActiviy" android:label="상세 보기">
```
위와 같이 지정하면 ActionBar의 타이틀 문자열은 label속성으로 지정한 문자열이 된다. 또한 자바코드의 setter함수를 사용하여 구성요소가 화면에 나와야 하는지를 제어한다.

#### 설정
```java
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

```java
actionBar.setIcon(R.drawable.icon); //로고 아이콘 지정
actionBar.setTitle("새로운 타이틀"); //타이틀 지정
actionBar.setSubtitle("새로운 서브타이틀"); //서브타이틀 지정
actionBar.setCustomView(customView); //커스텀 뷰 지정
```

#### 이벤트 처리
아이콘을 클릭했을 때 이벤트를 처리하려면 onOptionsItemSelected()함수 사용.
```java
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
### 안드로이드 API Level과 하위 호환성
우리가 배우고 있는 ActionBar는 API Level 11부터 제공하는 클래스이므로 이보다 하위인 안드로이드 버전에 대해서는 호환성 문제가 발생할 수 있습니다. 따라서 하위 호환성 문제를 짚고 넘어갈 필요가 있습니다.
**minSdkVersion** : 최소 요구 안드로이드 버전, 이 아래의 안드로이드에서는 앱 설치 자체가 되지 않는다. 개발 할때 반드시 minSdkVersion으로 지정한 버전까지는 에러가 발생하지 않도록 해야 한다.
예를 들어 minSdkVersion을 9로 설정했다고 하자. targetSdkVersion을 24버전이라고 하고 라이브러리를 사용하면 24버전의 라이브러리를 사용한다는 것이고 이 라이브러리를 사용할 때 API 9까지는 오류없이 앱을 구성해야한다. 만약 API 11부터 지원하는 ActionBar를 사용하게 되면 API 11이하는 지원하지 않으므로 문제가 발생한다. 이 부분을 신경 써주어야한다.

#### 하위 호환성에 걸리는 문제 해결법
- 구글 Support 라이브러리 사용
- 오픈소스 라이브러리 사용
- 개발자 코드에서 버전을 직접 선별 사용

##### Support 라이브러리 사용
Support 라이브러리는 구글의 라이브러리지만 표준 라이브러리는 아니다. 하위 호환성을 지원을 하고자 하는 것이 이 라이브러리의 목적 중 하나이다. 앞에서의 문제점을 Support 라이브러리를 사용하여 해결하여보자
- 표준 라이브러리 이외의 라이브러리를 사용 시 그레이들 파일에 dependencies를 연결해야만 사용할 수 있다.

```
dependencies {
    (...)
    implementation 'com.android.support:appcompat-v7:28.0.0'
    implementation 'com.android.support.constraint:constraint-layout:1.1.3'
    (...)
}
```
위의 내용은 `appcompat-v7` 라이브러리를 이용한다는 뜻이다. 이 라이브러리를 사용하여 ActionBar 호환성 문제를 해결할 것이다. 우리가 줄곧 사용했던 AppCompatAcitivity는 이 appcompat 라이브러리에서 제공하는 클래스다. 이 support 라이브러리를 사용하므로써 API 하위 호환 문제를 해결할 수 있다.
- 이때 반드시 appcompat에서 제공하는 테마를 상속받아 정의를 해야한다.

```xml
<style name="AppTheme" parent="Theme.AppCompat.Light.DarkActionBar">
    <!-- Customize your theme here. -->
</style>
```
- 또한 ActionBar를 획득할 때 getActionBar()함수가 아닌 getSupportActionBar() 함수를 이용한다.

>현재 최신 안드로이드 스터디는 자동으로 SupportActionBar를 사용한다. API 지원여부를 떠나 버전에 따라 너무 많은 부분이 변해왔기 때문에 API 11이상이더라도 AppCompatAcitivity를 상속하여 구현하는 것을 권장한다.

#### 개발자 코드로 버전 확인
Support 라이브러리가 매우 편하지만 모든 하위 호환성을 제공한다고 볼 수 없다. 따라서  개발자 코드로 직접 API level을 테스트해 볼 필요가 있다.
```java
if(Build.VERSION.SDK_INT >= Bulid.VERSION_CODES.LOLLIPOP){

}
else{

}
```
- **Build.VERSION.SDK_INT** 를 통해 현재 앱이 구동되는 스마트폰의 API level을 확인 할 수 있으며 이를 조건문으로 이상 버전과 이하 버전이 실행되는 구문을 나눌 수 있다.

---
### 메뉴
메뉴는 액티비티의 구성요소로 선택적으로 추가가 가능한 요소이다. ActionBar영역에 추가되어 표시
![image](https://user-images.githubusercontent.com/11483057/48343134-ee38c600-e6b4-11e8-88ef-cc7a9ff8fead.png)

### 메뉴 작성 방법
메뉴를 추가하는 방법은 java 코드 작성 혹은 xml 파일 이용 두 가지 방법이 있다.
#### java 코드 작성
메뉴 구성 함수를 재정의하여 작성
- onCreateOptionsMeun(Meun meun) : 메뉴가 만들어질 때 최초 한 번 반복
- onPrepareOptionsMeun(Meun menu) : 메뉴가 화면에 보일 때마다 반복 호출

```java
@Override
public boolean onCreateOptionsMeun(Meun meun) {

}

@Override
public boolean onPrepareOptionsMeun(Meun meun) {

}
```
이때 두 함수 모두 매개변수로 Meun 객체가 넘어오게 되고 이 객체에 add()함수를 이용하여 메뉴를 넣으면 된다.
- **add(CharSequence title)**
- **add(int groupId, int itemId, int order, int titleRes)**
- **add(int groupId, int itemId, int order, CharSequence title)**

위 add()의 매개변수 중 itemId는 메뉴의 식별자로 어느 메뉴가 눌렸는지를 확인할 수 있게 해준다. title 매개변수는 메뉴에 표시할 문자열이다.
add()함수는 메뉴 하나를 의미하는 MeunItem 객체를 리턴한다.

```java
@Override
public boolean onCreateOptionsMeun(Meun meun) {
  MeunItem item1 = meun.add(0,0,0,"슬라이드 쇼");
  MeunItem item2 = meun.add(0,1,0,"앨범에 추가");
  return true;
}

@Override
public boolean onPrepareOptionsMeun(Meun meun) {

}
```
이 MeunItem 객체를 구성하는 함수들은 아래와 같다.
- **setIcon(int iconRes)** : 아이콘 이미지 구성
- **setTitle(CharSequence title)** : 문자열 구성
- **setVisible(boolean visible)** : 화면 표시 유무 구성
- **setEnabled(boolean enabled)** : 활성 상태 구성

이제 사용자 이벤트 처리를 해보자. 이벤트 처리 함수는 onOptionsItemSelected()이다. 이 함수는 메뉴가 선택된 순간 호출되며 매개변수로는 선택된 MeunItem 객체가 전달된다. 이때 MenuItem.getItemId()으로 id를 가져와 객체의 id를 구분하여 이벤트를 처리할 수 있다.
```java
@Override
public boolean onOptionsItemSelected(MenuItem item) {
    if(item.getItemId()==android.R.id.home){
        Toast t=Toast.makeText(this, "HOME AS UP Click", Toast.LENGTH_SHORT);
        t.show();
        return true;
    }
    return super.onOptionsItemSelected(item);
}
```

---
### XML로 만들기
#### MeunInflater 활용
onCreateOptionsMeun() 혹은 onPrepareOptionsMeun()를 사용하여 다양한 메뉴를 구성하는 방법에 대해 살펴보았다. 하지만 실행할 때마다 같은 메뉴라면 XML로 만들어 구현하는 방법도 있다.
```xml
<menu xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto">
    <item
        android:id="@+id/menu1"
        android:icon="@drawable/ic_menu_1"
        android:title="선택..."
        />
    <item
        android:id="@+id/menu2"
        android:icon="@drawable/ic_menu_2"
        android:title="레이아웃"
        />
    <item android:id="@+id/file"
        android:title="SubMenu">
        <menu>
            <item android:id="@+id/sub1" android:title="Sub1"/>
            <item android:id="@+id/sub2" android:title="Sub2"/>
        </menu>
</menu>
```
이와 같이 xml로 만들고 **res/meun** 에 위치시킨다. 그리고 이 xml을 자바 코드로 부르기 위해서는 MeunInflater 객체를 사용한다.
```java
@Override
public boolean onCreateOptionsMenu(Menu menu) {
    MenuInflater inflater=getMenuInflater();
    inflater.inflate(R.menu.menu_lab2, menu);
    return true;
}
```
이때도 마찬가지로 <item>태그의 id값을 구별하여 이벤트를 처리하면 된다.


---
### XML로 메뉴 구성
위에서 java 코드로 메뉴구성을 해본 것처럼 xml에서 메뉴를 구성한다.
#### 아이콘 출력
- **android:icon** 속성을 이용하여 아이콘을 등록한다.

```xml
<menu xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto">
    <item
        android:id="@+id/menu1"
        android:icon="@drawable/ic_menu_1"
        android:title="선택..."
        />
</meun>
```

- java 코드에서 MeunBuilder 객체를 획득하여 아이콘 표시 여부를 선택한다.
  - **setOptionalIconsVisible(true)** 를 호출

```java
@Override
public boolean onCreateOptionsMenu(Menu menu) {
    MenuInflater inflater=getMenuInflater();
    inflater.inflate(R.menu.menu_lab2, menu);
    if(menu instanceof MenuBuilder){
        MenuBuilder m=(MenuBuilder)menu;
        m.setOptionalIconsVisible(true);
    }
    return true;
}
```

#### 서브 메뉴
메뉴를 구성하보면 메뉴 안의 메뉴를 구성할 필요가 있다. 이때 <meun>태그 안에 <meun>태그를 중복하여 구성할 수 있다.
```xml
<menu xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto">
    <item
        android:id="@+id/menu1"
        android:icon="@drawable/ic_menu_1"
        android:title="선택..."
        />
    <item
        android:id="@+id/menu2"
        android:icon="@drawable/ic_menu_2"
        android:title="레이아웃"
        />
    <item android:id="@+id/file"
        android:title="SubMenu">
        <menu>
            <item android:id="@+id/sub1" android:title="Sub1"/>
            <item android:id="@+id/sub2" android:title="Sub2"/>
        </menu>
</menu>
```

#### 액션 버튼
지금까지는 메뉴에서 오버플로 아이콘을 클릭해야 화면에 나타났지만 미리 아이콘으로 꺼내서 ActionBar에 올려서 사용할 수 있도록 하게 할 수 있다.

##### 구성 방법
- <item> 태그 안에 **app:showAsAction="always"** 를 추가
  - never : 기본값, 오버플로 메뉴로 구성
  - always : 항상 액션 버튼으로 구성
  - ifRoom : ActionBar에 공간이 있다면 액션버튼, 없다면 오버플로 메뉴로 나타낸다.
  - withText: 아이콘과 문자열이 같이 출력, 공간이 없다면 아이콘만 출력

```xml
<item
    android:id="@+id/menu_main_search"
    android:icon="@android:drawable/ic_menu_search"
    android:title="Search"
    app:showAsAction="always"
    app:actionViewClass="android.support.v7.widget.SearchView"/>
```
> android namespace가 아닌 app namespace인 이유?
> 하위 호환성을 위해 appcompat 라이브러리에서 처리하기 때문이다. appcompat 라이브러리는 표준 라이브러리가 아니므로 네임스페이스를 따로 지정해주어야한다. 이것이 app이다.

---
#### ActionView
메뉴를 구성하는데 있어 유용하게 사용할 수 있는 것이 AcitonView이다. 이는 ActionBar에 제공이 되는 뷰이며 ActionBar가 제공하는 뷰를 그대로 이용할 수 있어서 편리하다. 대표적이 뷰가 SearchView이며 검색을 사용할 때 유용하다.
![image](https://user-images.githubusercontent.com/11483057/48345800-6656ba00-e6bc-11e8-85cb-6ffc462af4c8.png)
위 그림과 같이 돋보기 아이콘이 나와서 일반적인 액션 버튼처럼 사용할 수 있다. 이 버튼을 누르면 자동으로 글을 입력하기 위한 뷰가 나타난다. 구현하는 방법은 기본 액션 버튼과 같지만 **app:actionViewClass="android.support.v7.widget.SearchView"** 만 추가해서 들어간다.

```xml
<item
  android:id="@+id/menu_main_search"
  android:icon="@android:drawable/ic_menu_search"
  android:title="Search"
  app:showAsAction="always"
  app:actionViewClass="android.support.v7.widget.SearchView"
  />
```
또한 이 SearchView 객체를 자바 코드로 가져와 사용한다. SearchView 객체도 MeunItem 객체로 가져온다.
```java
public boolean onCreateOptionsMenu(Menu menu) {
    MenuInflater inflater=getMenuInflater();
    inflater.inflate(R.menu.menu_lab2, menu);

    MenuItem menuItem=menu.findItem(R.id.menu_main_search);
    searchView = (SearchView) menuItem.getActionView();
    searchView.setQueryHint(getResources().getString(R.string.query_hint));
    searchView.setOnQueryTextListener(queryTextListener);

    return true;
}
```
이제 이벤트 처리를 해보자 검색 입력 이벤트 처리는 **OnQueryTextListener**를 구현하면 된다.

```java
SearchView.OnQueryTextListener queryTextListener=new SearchView.OnQueryTextListener() {
    @Override
    public boolean onQueryTextSubmit(String query) {
        searchView.setQuery("", false);
        searchView.setIconified(true);
        showToast(query);
        return false;
    }

    @Override
    public boolean onQueryTextChange(String newText) {
      
        return false;
    }
};
```

- **onQueryTextSubmit(String query)** : 키보드에서 검색 버튼이 눌린 순간 호출
- **onQueryTextChange(String newText)** : 검색 글이 한 글자 한 글자를 입력할 때마다 호출

---
#### actionLayout
위에서 살펴본 SearchView처럼 개발자가 임의의 뷰 ActionView로 설정할 수 있다. 이때 사용되는 속성이 **actionLayout** 이다. **app:actionLayout="@layout/actionview_check"** 로 설정하여 해당 뷰가 AcitonView로 나타난다. 뷰가 공간을 많이 차지하므로 아이콘을 눌러야 나오도록 **app:showAsAction="ifRoom|collapseActionView"** 를 설정하여 아이콘만 나오게 하였다.
```xml
<item
    android:id="@+id/menu3"
    app:showAsAction="ifRoom|collapseActionView"
    android:title="Check"
    android:icon="@android:drawable/ic_menu_day"
    app:actionLayout="@layout/actionview_check"
    />
```

---
#### ContextView
메뉴 중에서 ContextView라는 메뉴가 있다. 이는 AcitonBar에 나타나는 것이 아니라 특정 뷰를 오래 누르면 뷰와 연결되어 보이는 메뉴이다.
##### 구현 방법
액티비티 내에 onCreateContextMeun() 함수를 이용한다.
```java
@Override
public void onCreateContextMenu(ContextMenu menu, View v, ContextMenu.ContextMenuInfo menuInfo) {
    super.onCreateContextMenu(menu, v, menuInfo);
    menu.add(0,0,0,"서버전송");
    menu.add(0,1,0,"보관함에 보관");
    menu.add(0,2,0,"삭제");
}
```
##### 이벤트 처리
이벤트 처리는 onContextItemSelected() 함수를 이용한다.
```java
@Override
public boolean onContextItemSelected(MenuItem item) {
    switch (item.getItemId()){
        case 0:
            showToast("서버 전송이 선택되었습니다.");
            break;
        case 1:
            showToast("보관함에 보관이 선택되었습니다.");
            break;
        case 2:
            showToast("삭제가 선택되었습니다.");
            break;
    }
    return true;
}
```
이후 뷰와의 연결이 필요하다. 이때는 registerForContextMeun() 함수를 사용한다.
```java
registerForContextMeun(imageView);
```
이를 통해 imageView에 메뉴가 연결되어 오래 누르면 메뉴가 표시된다.

---
### 참고도서
깡샘의 안드로이드 프로그래밍(루비페이퍼,2017)

---
