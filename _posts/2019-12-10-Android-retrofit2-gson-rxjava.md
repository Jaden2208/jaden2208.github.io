---
layout: post
title: "Retrofit2, Gson, Rxjava 사용법"
categories:
  - Android
tags:
  - android
  - kotlin
  - java
  - retrofit2
  - rest_api
  - gson
  - rxjava
last_modified_at: 2019-12-10T
---
### Retrofit2

HTTP를 처리하기 위해서는 만들어야 할 루틴들이 너무 많다.

커넥션, 캐싱, 요청, 스레딩, 파싱, 에러 핸들링 등...

Retrofit은 HTTP의 REST API 구현을 위한 매우 인기 있는 라이브러리로 Square의 오픈소스 라이브러리 중 하나이다. 앞서 언급한 여러가지 루틴을 제공해 개발자가 해야할 일을 많이 줄여준다.

> https://square.github.io/retrofit/

Square 사는 otto, dagger, Picasso, OkHTTP와 같은 라이브러리도 배포하고 있다, REST는 Representational State Transfer의 약자로 네트워크 상 클라이언트의 통신방식을 말하며, HTTP의 GET, POST, PUT, DELETE와 같은 요청을 처리하는 방법을 제공한다. 클라이언트의 응답에 대한 처리로 xml, json, text, rss등을 지원한다.

### 사용법

##### 1. Gradle 파일에 dependencies 추가

`implementation 'com.squareup.retrofit2:retrofit:2.7.0'`

##### 2. 인터페이스 만들기

```java
public interface GitHubService {
  @GET("users/{user}/repos")
  Call<List<Repo>> listRepos(@Path("user") String user);
}
```

`@GET` 어노테이션을 통해 GitHub API 중에서 user와 관련된 부분을 읽어올 준비가 된다. `@Path`는 경로상의 {...}를 대체할 수 있다.

##### 3. URL 초기화하기

```java
// url 초기화
Retrofit retrofit = new Retrofit.Builder()
    .baseUrl("https://api.github.com/")
    .build();
// 인터페이스 서비스 요청
GitHubService service = retrofit.create(GitHubService.class);
```

Retrofit의 빌더 메서드인 baseUrl()을 통해 URL을 초기화 한다. 이때 생성된 객체인 retrofit을 통해 앞서 지정된 GitHubService 인터페이스를 이용한 하나의 서비스 요청이 생성된다.

이 요청을 받은 서버는 XML, JSON등 다양한 형태로 응답할 수 있다. 이 응답에 대응하려면 다양한 컨버터들이 있어야 한다.

Retrofit은 다음과 같은 컨버터를 제공한다.

Retrofit이 제공하는 컨버터
> Gson: com.squareup.retrofit2:converter-gson
Jackson: com.squareup.retrofit2:converter-jackson
Moshi: com.squareup.retrofit2:converter-moshi
Protobuf: com.squareup.retrofit2:converter-protobuf
Wire: com.squareup.retrofit2:converter-wire
Simple XML: com.squareup.retrofit2:converter-simplexml
Scalars (primitives, boxed, and String): com.squareup.retrofit2:converter-scalars

Gson은 자바 객체와 JSON을 서로 변환할 수 있는 구글에서 제공하는 라이브러리이다.

Jackson은 JSON 뿐만 아니라 다양한 자료형을 제공한다.

그 밖에도 기타 사용하는 라이브러리나 목적에 따라 컨버터를 선택할 수 있다.

그 중 **Gson** 을 사용한 예를 한번 보자

### Gson

##### 1. Gradle 파일에 dependencies 추가

`implementation 'com.squareup.retrofit2:converter-gson:2.7.0'`

그리고 [retrofit 초기화 코드](#3.-URL-초기화하기)에 `addConverterFactory()`를 다음과 같이 추가한다.

##### 2. URL 초기화

```java
// url 초기화
Retrofit retrofit = new Retrofit.Builder()
    .baseUrl("https://api.github.com/")
    .addConverterFactory(GsonConverterFactory.create())
    .build();
```

### RxJava

보통 웹서비스는 비동기적으로 응답을 처리해야한다. 따라서 이에 필요한 추가 어댑터인 RxJava를 사용하는 경우에 gradle에 다음과 같이 추가한다.

(RxJava에 대한 자세한 설명은 [여기](링크))


##### 1. Gradle 파일에 dependencies 추가

`implementation 'com.squareup.retrofit2:adapter-rxjava2:2.7.0`

그 다음 인터페이스에는 다음과 같이 `Observable<Repo>`를 정의한다. 코틀린으로 정의하면 다음과 같다.

##### 2. 인터페이스 만들기

```kotlin
@GET("/search/users?")
fun searchUser(
        @Query(value = "q", encoded = true) userKeyword: String,
        @Query("page") page: Int,
        @Query("per_page") perPage: Int): Observable<GitHubUserSearchResponse>
```

따라서 초기화 시에는 추가 어댑터 설정을 다음과 같이 넣어준다.

##### 3. URL 초기화

```kotlin
Retrofit retrofit = new Retrofit.Builder()
    .baseUrl("https://api.github.com")
    .addCallAdapterFactory(RxJavaCallAdapterFactory.create()) // 혹은 RxJava2CallAdapterFactory
    .addConverterFactory(GsonConverterFactory.create())
    .build();
```

이후에는 RxJava나 RxAndroid를 다음과 같이 gradle에 추가하고 나머지 루틴을 개발한다.

```
implementation 'io.reactivex:rxandroid:<버전명>'
implementation 'io.reactivex:rxjava:<버전명>'
```

다음 사이트에서 추가 정보를 확인할 수 있다.

```
https://github.com/square/retrofit/tree/master/retrofit-adapters/rxjava2
```

### Coroutines

만약 코틀린의 코루틴으로 비동기 루틴을 만들때는 Retrofit2를 같이 사용하기 위해 gradle에 다음을 추가하고 어댑터를 변경할 수 있다.

`implementation 'com.jakewharton.retrofit:retrofit2-kotlin-coroutines-adapter:0.9.2'`

인터페이스 설계 시에는 기존 Call 대신에 Deffered 인스턴스를 반환해 사용할 수 있다.

```Kotlin
interface MyService {
  @GET("/user")
  fun getUser(): Deferred<User>

  // 또는

  @GET("/user")
  fun getUser(): Deferred<Response<User>>
}
```

추가 정보는 다음 사이트에서 확인할 수 있다.

```
https://github.com/JakeWharton/retrofit2-kotlin-coroutines-adapter
```
  <br>

  ---

<font size="2em"> https://acaroom.net/ko/blog/youngdeok/%EC%97%B0%EC%9E%AC-%EC%BD%94%ED%8B%80%EB%A6%B0-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8-01-%EC%98%A4%ED%94%88%EC%86%8C%EC%8A%A4-%EB%9D%BC%EC%9D%B4%EB%B8%8C%EB%9F%AC%EB%A6%AC%EC%9D%98-%EC%9D%B4%ED%95%B4</font>
