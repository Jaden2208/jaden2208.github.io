---
layout: post
title: "액티비티의 생명주기(Life Cycle)"
categories:
  - Android
tags:
  - this
  - java
last_modified_at: 2019-10-11T
---
### Activity의 생명주기(Lifecycle)
* 액티비티에는 특정 시점에 호출되는 여러 메서드가 있다. 예를 들어 `onCreate()`는 생성 시점에 호출된다.
* 이렇게 특정한 타이밍에 호출되는 메서드를 '콜백 메서드'라고 한다.

<img src="/images/activity_lifecycle.png"></img>

#### 액티비티 시작
 1) `onCreate()` : 액티비티가 시작되면 호출  
 2) `onStart()`  
 3) `onResume()`

#### 액티비티 종료
 1) `onPause()` : 액티비티가 화면에서 보이지 않게 되는 순간 호출  
 2) `onStop()` : 완전히 보이지 않게 되면 호출  
 3) `onDestroy()`

#### 액티비티 재개
앱을 완전히 종료하지 않고 홈으로 가거나 전원버튼을 통해 화면을 끄는 경우에는 `onPause()`, `onStop()` 까지만 호출되고 대기하게 된다.
  이때 다시 앱이 전면으로 나오는 경우에는 `onRestart()`, `onStart()`, `onResume()` 순으로 호출된다.

#### 프로세스 강제 종료

  안드로이드의 모든 앱은 백그라운드 실행 중에 메모리 부족 등으로 강제 종료될 수 있다.
  이때 앱을 다시 실행하면 `onCreate()` 메서드부터 호출한다.

  <br>

  ---

  <center><font size="2em"> <<오준석의 안드로이드 생존코딩 - 코틀린 편>> 을 참고해 작성했습니다.</font></center>
