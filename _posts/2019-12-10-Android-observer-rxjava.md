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
### Observer 패턴

>
> *Observer : 관찰자*
>

**Observer** 패턴은 객체의 상태 변화를 관찰하는 관찰자들인 **Observer** 들의 목록을 객체에 등록하여 상태 변화가 있을 때 마다 메서드 등을 통해 객체가 직접 목록의 각 **Observer** 들에게 통지하도록 하는 디자인 패턴이다.

이벤트 처리 시스템이나 GUI를 설계할 때 사용되는 패턴이기도 하다.

> observer 패턴의 클래스 다이어그램
>
> <img src="/images/observerpattern_uml_class.png" width="80%" height="80%"></img>

위 그림에서 Subject는 이벤트를 발생시키는 주체이다. RxJava 에서는 Observable 또는 Subject 라는 이름으로 표현된다.

Subject에서 발생되는 이벤트들은 그 Subject에 관심있다고 등록한 Observer 들에게 전달된다.

여기서 Observer는 RxJava에서는 Subsrciber라는 이름으로 표현된다.

> observer 패턴의 시퀀스 다이어그램
>
> <img src="/images/observerpattern_uml_sequence.png" width="80%" height="80%"></img>

기본적으로 관찰자(Observer) 또는 구독자(Subsrciber)인 o1, o2는 관심주제(Subject) s1에 붙임(attach) 또는 등록(register) 또는 구독(subscribe)이라는 과정을 한다.

이 후에 관심주제 s1에 이벤트가 발생하면 통보(notify)하게 되고 관찰자들은 갱신(update) 할 수 있게 된다.

RxJava에서 사용하는 용어 기준으로 다시 한번 정리하면 다음과 같다.
 * **이벤트(Event)**: 구독자들에게 전달되는 데이터 (주로 클릭, 상태, API 응답 등)
 * **구독(Subscribe)**: 구독자가 이벤트를 전달받기 위해 하는 행위(등록)
 * **관찰(Observe)**: RxJava에서는 Observable 컴포넌트들을 서로 연결(map())할 수 있으며 Observable은 다른 Observable을 관찰. Subsriber는 구독(subscribe())을 통해서 Observable을 관찰.

#### 이벤트의 처리

* `onNext()` : 이벤트 발생 시
* `onCompleted()` : 이벤트 종료 시
* `onError()` : 에러 발생 시

```java
// Observable 생성
Observable<String> o1 = Observable.just("One"); // (1)
// 구독
o1.subscribe(new Subscriber<String>() {
    @Override public void onNext(String text) {
        System.out.println("onNext : " + text);
    }

    @Override public void onCompleted() {
        System.out.println("onCompleted");
    }

    @Override public void onError(Throwable e) {
        System.out.println("onError : " + e.getMessage());
    }
});
```

(1)번 부분인 `Observable.just()` 는 누군가가 구독(subscribe)을 하게 되면 "One"이라는 이벤트를 한번 발생시킨다.

이후 `onNext()`로 "One"이 전달되고 그 다음 `onCompleted()`가 호출된다.

만일 (1)번 부분을 아래과 같이 변경하면 Iterable 요소의 순서대로 이벤트를 발생한다.

```java
Observable<String> observable = Observable.from(new String[] { "One", "Two", "Three" });
```

지속적으로 `onNext()`를 발생하다가 `onCompleted()`를 마지막으로 호출하고 종료된다.

```
onNext : One
onNext : Two
onNext : Three
onCompleted
```

`Observable.defer()`를 사용하면 특정 함수를 실행시킬 수 있다.

```java
Observable<String> observable = Observable.defer(new Func0<Observable<String>>() {
            @Override public Observable<String> call() {
                System.out.println("defer function call");
                return Observable.just("HelloWorld");
            }
        });
```

#### 비동기 처리

비동기 처리를 위한 새로운 스레드를 생성해 처리하고자 하는 경우에는 `subscribeOn()`과 `observeOn()`을 이용한다.

```java
...
System.out.println(Thread.currentThread().getName() + ", create observable");
Observable<String> observable = Observable.defer(new Func0<Observable<String>>() {
    @Override public Observable<String> call() {
        System.out.println(Thread.currentThread().getName() + ", defer function call");
        return Observable.just("HelloWorld");
    }
});
...
System.out.println(Thread.currentThread().getName() + ", do subscribe");
observable
    .subscribeOn(Schedulers.computation()) // 연산을 위한 스레드에서 defer 함수가 실행된다
    .observeOn(Schedulers.newThread()) // 새로운 스레드에서 Subscriber로 이벤트가 전달된다
    .subscribe(new Subscriber<String>() {
        @Override public void onNext(String text) {
            System.out.println(Thread.currentThread().getName() + ", onNext : " + text);
        }

        @Override public void onCompleted() {
            System.out.println(Thread.currentThread().getName() + ", onCompleted");
        }

        @Override public void onError(Throwable e) {
            System.out.println(Thread.currentThread().getName() + ", onError : " + e.getMessage());
        }
    });

System.out.println(Thread.currentThread().getName() + ", after subscribe");
}
```

`subscribeOn()`은 구독이 이루어지는 스레드로 옵션인 `computation()`이 정의되었고

`observeOn()`에는 관찰자에게 전달될 때 사용하는 스레드가 지정되어 실행된다.

결과는 아래와 같다.

```
main, create observable
main, do subscribe
main, after subscribe
RxComputationThreadPool-3, defer function call
RxNewThreadScheduler-1, onNext : HelloWorld
RxNewThreadScheduler-1, onCompleted
```

### 안드로이드 UI에서의 처리

안드로이드의 UI스레드인 메인스레드를 관찰하기 위해서는 RxAndroid를 통해 다음과 같이 사용할 수 있다.

```java
Observable.just("one", "two", "three", "four", "five")
        .subscribeOn(Schedulers.newThread())
        .observeOn(AndroidSchedulers.mainThread())
        .subscribe(/* an Observer */);
```

안드로이드에는 메시지 전달 역할을 하는 루퍼(Looper)라는 개념이 있는데, 메시지큐에서 메시지를 스레드에 전달해 처리하는 역할을 한다.

그런 루퍼를 관찰하기 위해서는 다음과 같이 지정할 수 있다.

```java
Looper backgroundLooper = // ...
Observable.just("one", "two", "three", "four", "five")
        .observeOn(AndroidSchedulers.from(backgroundLooper))
        .subscribe(/* an Observer */)
```

### RxKotlin 확장의 사용

RxKotlin 확장을 사용하면 코틀린 문법으로 자바의 보일러플레이트한(=재사용 가능한) 코드를 확 줄일 수 있다.

> 참고 링크
> https://github.com/ReactiveX/RxKotlin


이 사이트에서 소개된 컬렉션에 사용된 예제를 확인해 보자

```kotlin
import io.reactivex.rxkotlin.subscribeBy
import io.reactivex.rxkotlin.toObservable

fun main(args: Array<String>) {

    val list = listOf("Alpha", "Beta", "Gamma", "Delta", "Epsilon")

    list.toObservable() // 컬렉션의 함수 확장
            .filter { it.length >= 5 }
            .subscribeBy(  // named arguments for lambda Subscribers
                    onNext = { println(it) },
                    onError =  { it.printStackTrace() },
                    onComplete = { println("Done!") }
            )

}
```

추가 정보는 아래 사이트에서 확인할 수 있다.
> https://github.com/ReactiveX/RxAndroid

  <br>

  ---

<font size="2em"> https://acaroom.net/ko/blog/youngdeok/%EC%97%B0%EC%9E%AC-%EC%BD%94%ED%8B%80%EB%A6%B0-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8-01-%EC%98%A4%ED%94%88%EC%86%8C%EC%8A%A4-%EB%9D%BC%EC%9D%B4%EB%B8%8C%EB%9F%AC%EB%A6%AC%EC%9D%98-%EC%9D%B4%ED%95%B4</font>
