---
layout: post
title: "Dagger2 라이브러리"
categories:
  - Android
tags:
  - android
  - dagger2
  - dependency_injection
last_modified_at: 2019-12-10T
---
### Dagger2 라이브러리

의존성 주입으로 많이 사용되는 Dagger는 Square에서 개발되고 현재 Dagger2가 구글에 의해 지원 개발 되었다.

> 참조 사이트
> https://google.github.io/dagger/
> https://github.com/google/dagger

#### 그레들 의존성 라이브러리

안드로이드에 이 라이브러리를 적용하기 위해 build.gradle에 다음을 추가한다.

```
apply plugin: 'kotlin-kapt'
...
dependencies {
    implementation 'com.google.dagger:dagger:2.x'
    kapt 'com.google.dagger:dagger-compiler:2.x'
    compileOnly 'org.glassfish:javax.annotation:10.0-b28'
...
```

#### 의존성 주입이란?

Dagger는 의존성 주입 혹은 DI(Depdency Injection)이라는 프레임워크 라이브러리이다.

의존성 주입이란 구성요소간의 의존 관계가 소스코드 내부가 아닌 외부의 설정파일 등을 통해 정의되게 하는 디자인 패턴 중의 하나이다.

아래 그림을 통해 확인해보자.

> 기존 방식과 의존성 주입 방식
> <img src="/images/dependency_injected.png" width="100%" height="100%"></img>

전통적인 방법에서는 Main이 여러 코드에 의존되어 있어 하나가 변경되면 차례로 변경을 해야한다.

의존성 주입은 Main에서의 의존은 최대한 줄이되 필요할 때마다 의존성 주입을 통해 동적으로 구조를 적용하는데 있다.

##### 이게 왜 필요할까?

먼저 모듈간의 의존성이 낮아져 프로그램이 대형화되면 유지 보수나 재사용성이 늘어나는데 있다.

하지만 규모가 작은 프로그램에서는 오히려 코드량이 맣아져 읽기 어려워질 수 있다.

안드로이드는 특히 context의 영향을 많이 받게 되는데 만일 Activitiy나 Fragment의 인스턴스를 만들고 그 생명주기에 진입하면 당연히 Activity나 Fragment의 context에 영향을 받을 수 밖에 없다.

하지만 역으로 생각해 인스턴스를 Activity나 Fragment 밖에서 만들고 받아서 사용하면 범용적으로 재사용이 가능하게 된다.

이것을 '제어의 반전'이라는 용어로 Inversion of Control 이라는 디자인 개념으로 설명하고 있다.

소프트웨어 공학을 위한 용어로 꽤 어려운 개념으로 정의되어 있는데 간단히 말하면,

'다른 누군가가 대신 해주는'

개념으로 생각하면 좋을 것 같다.

자바 EE 기반의 개발을 위한 애플리케이션 프레임워크인 Spring 같은 것은 이것을 철저하게 따르고 있다.

Spring 프레임워크와 코틀린의 사용이 궁금한 경우 다음 내용을 참조해 볼 수 있다.

> [hyper-cube.io](http://hyper-cube.io/2017/11/27/spring5-with-kotlin/)
> [spring.io](https://spring.io/guides/tutorials/spring-boot-kotlin/)
> [kotlinlang.org](https://kotlinlang.org/docs/tutorials/spring-boot-restful.html)

#### 의존성 주입의 방법

> Activity에 인스턴스를 주입하는 컴포넌트
> <img src="/images/di_activity.png" width="100%" height="100%"></img>

##### 의존성을 주입하기 위해서는 일단 3가지 방식의 주입을 이해해야 한다.

- 생성자 주입 : 필요한 의존성을 포함하는 클래스의 생성자를 만들고 생성자를 통해 의존성 주입

- 세터를 통한 주입 : 의존성을 입력받는 세터 메서드를 만들고 이것을 통해 의존성 주입

- 인터페이스를 통한 주입 : 의존성을 주입하는 메서드를 포함한 인터페이스를 작성하고 이 인터페이스를 구현하도록 해 실행 시에 이를 통해 의존성 주입

##### Dagger2는 어노테이션 표기법을 이용해 다음과 같이 표현된다.

> Dagger2의 어노테이션 표기법
> <img src="/images/dagger2_model.png" width="100%" height="100%"></img>

먼저 `@Module`, `@Provides`의 공급자와 이것을 `@Inject` 주입해 소비하는 소비자 클래스,

연결을 담당하는 `@Component` 인터페이스로 이루어져 있다.

`@Provides` 어노테이션은 특정 의존성을 제공하는 메서드에 사용된다.

아래의 코드에서처럼 `@Provides`가 붙은 `provideContext()`는 Application의 의존성 객체인 컨텍스트를 제공하게 된다.

```kotlin
@Module
class AppModule(private val app: Application) {
  @Provides
  @Singleton
  fun provideContext(): Context = app
}
```

가장 상위 개념인 앱의 Application을 공급자로 설정한다.

앱 전반의 의존성을 제공할 수 있게된다.

주 생성자에 private으로 선언된 프로퍼티인 app 객체와 이 객체를 반환하는 `provideContext()`를 통해 설정될 수 있다.

Application 클래스는 보통 context 객체를 통해 안드로이드의 여러 요소 간 사용할 공통의 내용을 접근할 수 있다.

Application 클래스의 이름은 AndroidManifest.xml에 `<application>` 태그에 정의되어있다.

따라서 `@Provides` 어노테이션은 의존성의 특정 자료형, 여기서는 Context 객체를 제공할 수 있다는 것을 나타낸다.

`@Singleton`은 Dagger API는 아니고 javax.annotation 패키지에 포함된 어노테이션으로 인스턴스가 오로지 하나여야 한다는 것을 나타낸다.

이것을 다시 `@Module` 어노테이션을 통해 의존성을 주입할 수 있는 클래스로 `@Component`에 제공할 수 있는 Dagger 모듈이 만들어졌다.

#### 의존성 주입의 연결과 빌드

이제 이것을 사용하기 위해서는 `@Component` 어노테이션을 사용하는 연결 매개체가 필요하다.

```kotlin
@Singleton@Component(modules = [AppModule::class])
interface AppComponent
```

`@Component`는 다수의 모듈을 가질 수 있다.

`[AppModule::class]` 표현법은 배열 표현법이 된다.

이 컴포넌트는 의존된 두 객체간의 연결을 담당한다.

보통 `inject()` 메서드를 사용해 주입하고자 하는 대상을 지정한다.

Application의 하위 클래스에서 이것을 할 수 있다.

예를들어 myApplication이 있다면 그 안의 프로퍼티와 초기 메서드를 아래와 같이 작성할 수 있다.

```kotlin
...
lateinit var myComponent: AppComponent
...
private fun initDagger(app: myApplication): AppComponent =
      DaggerAppComponent.builder()
          .appModule(AppModule(app))
          .build()
...
```

빌드 전까지는 `DaggerAppComponent` 에서 에러를 발생하는데 빌드 후 `DaggerAppComponent.builder()`에 의해 DaggerAppComponent.java가 생성되면서 에러는 없어진다.

모든 의존성이 제대로 만족하는지 컴파일 타임에 검사하게 되는 것이다.

이것은 초기 Dagger1이나 기존의 DI 프레임워크는 컴파일 타임에 검사하지 못하고 런타임에 의존성 적합 여부를 알기 때문에 잘못된 의존성이 있을 경우 런타임에서 에러가 날 수 있었다.

Dagger2는 이것을 방지한다.

##### 초기화와 주입

이제 myApplication의 `onCreate()`에서 아래와 같이 초기화 함수를 호출시킨다.

```kotlin
override fun onCreate() {
    super.onCreate()
    wikiComponent = initDagger(this)
  }
```

이제 주입을 위해 AppComponent 인터페이스에 다음을 선언한다.

```kt
fun inject(target: HomepageActivity)
```

이제 HomepageActivity는 AppComponent로 부터 주입이 필요한 클래스가 된다.

공급자 모듈을 하나 더 만들어보자

```kotlin
@Module
class PresenterModule {
  @Provides
  @Singleton
  fun provideHomepagePresenter(): HomepagePresenter = HomepagePresenterImpl()
}
```

이 모듈은 메서드를 통해 `HomepagePresenterImpl()`을 반환하게 된다.

그러면 다음과 같이 `@Component`에 모듈을 더 추가할 수 있게 된다.

```kotlin
@Component(modules = [AppModule::class, PresenterModule::class])
```

이제 HomepageActivity에는 다음과 같은 프로퍼티를 선언한다.

```kotlin
...
@Inject lateinit var presenter: HomepagePresenter // 주입 되어야 함을 나타냄
...
```

여기에 있는 `@Inject`도 사실 Dagger의 어노테이션이 아닌 javax의 어노테이션으로 주입되어야 함을 나타낸다.

실제로는 `onCreate()`에서 `inject()`를 호출하며 주입한다.

```kotlin
override fun onCreate(savedInstanceState: Bundle?) {
    super.onCreate(savedInstanceState)
    setContentView(R.layout.activity_homepage)

    (application as myApplication).myComponent.inject(this)
    ...
  }
```

이제 Dagger는 HomepagePresenter 객체를 HomepageActivity에 주입할 것이다.

##### 커피 제조기 예제

또 다른 예제로, 좀 더 이해해 보려면 다음 사이트를 참조하면 된다.

> Java 예제: https://github.com/google/dagger/tree/master/examples/simple/src/main/java/coffee
> Kotlin 예제: https://github.com/JetBrains/kotlin-examples/tree/master/maven/dagger-maven-example/src/main/kotlin

> CoffeMaker의 연관 관계
> <img src="/images/coffee_maker_dagger.png" width="100%" height="100%"></img>

`@Module`, `@Provides`에서 제공자가 있고, 이것을 통해 연결 역할을 하는 Coffee 인터페이스가 있다.

이 인터페이스는 어노테이션 컴파일러 kapt에 의해 Dagger가 붙은 클래스를 생성하며 여기에 Builder 클래스와 build() 메서드를 통해 의존성에 맞는 인스턴스를 생성해 `@Inject`가 있는 생성자에 주입한다.




  <br>

  ---

<font size="2em"> https://acaroom.net/ko/blog/youngdeok/%EC%97%B0%EC%9E%AC-%EC%BD%94%ED%8B%80%EB%A6%B0-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8-01-%EC%98%A4%ED%94%88%EC%86%8C%EC%8A%A4-%EB%9D%BC%EC%9D%B4%EB%B8%8C%EB%9F%AC%EB%A6%AC%EC%9D%98-%EC%9D%B4%ED%95%B4</font>
