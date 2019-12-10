---
layout: post
title: "RxJava란"
categories:
  - Android
tags:
  - android
  - rxjava
  - observer
last_modified_at: 2019-12-10T
---
### Rxjava

**Reactive 프로그래밍**으로 **RxJava**가 많이 사용되는데 **Reactive 프로그래밍**이란 데이터를 <u>비동기적으로 처리</u>해 효율성을 높여주고자 나온 프로그래밍 기법이다.

다음 사이트에서 추가 정보를 확인할 수 있다.
> https://github.com/ReactiveX/RxJava

통신에서 일반적인 비동기 데이터 처리가 끝날 때까지 스레드를 대기시키거나 콜백을 받아서 처리하면 **불필요한 리소스 사용**이 발생한다.

반면 <u>메시징 기반</u>의 **Reactive 프로그래밍**에서는 필요한 경우에만 스레드를 생성한 후 메시지 형태로 전달하기 때문에 <u>더 효율적</u>으로 컴퓨팅 리소스를 사용할 수 있다.

물론, 코틀린의 **코루틴**을 통해서 비동기 프로그래밍을 손쉽게 적용할 수 있지만, **코루틴**은 이제 막 안정되기 시작한 라이브러리이고 **RxJava**는 비교적 오랜 시간에 걸쳐 안정되고 있는 인기있는 라이브러리이기 때문에 기존의 프로젝트가 **RxJava**를 사용했을 경우 읽고 이해하기 위해 알아둘 필요가 있다.

[여기](링크)로 이동해서 **RxJava**를 어떻게 사용하는지 알아볼 수 있다.

**RxJava**를 사용하기 위해서는 **Observer 패턴**에 대한 이해 또한 필요하다.

**Ovserver 패턴**에 대한 설명은 [여기](https://jaden2208.github.io/android/2019/12/10/Android-observer-rxjava.html)에 있다.


  <br>

  ---

<font size="2em"> https://acaroom.net/ko/blog/youngdeok/%EC%97%B0%EC%9E%AC-%EC%BD%94%ED%8B%80%EB%A6%B0-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8-01-%EC%98%A4%ED%94%88%EC%86%8C%EC%8A%A4-%EB%9D%BC%EC%9D%B4%EB%B8%8C%EB%9F%AC%EB%A6%AC%EC%9D%98-%EC%9D%B4%ED%95%B4</font>
