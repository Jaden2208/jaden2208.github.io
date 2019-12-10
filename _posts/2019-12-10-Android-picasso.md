---
layout: post
title: "Picasso 라이브러리"
categories:
  - Android
tags:
  - android
  - picasso
last_modified_at: 2019-12-10T
---
### Picasso 라이브러리

네트워크 상의 이미지를 위한 관련 라이브러리 중 유용한 라이브러리로 Square의 Picasso와 구글의 Glide가 있다.

두 라이브러리의 사용법은 거의 동일하다.

다만 Glide는 빠르게 가져오기 위한 설정이 기본적으로 적용되어 있어 품질은 약간 낮으나 적은 자원과 느린 네트워크에서 좀 더 원활하게 이미지를 가져올 수 있다.

두 개의 라이브러리 중 여기서는 Picasso에 대해 살펴보겠다.

> 참조 사이트
> http://square.github.io/picasso/

#### Picasso의 기본 사용

`implementation 'com.squareup.picasso:picasso:<버전명>'`

사용법이 간단하며 이미지에 대한 각종 전처리, 후처리, 캐싱, 메모리 관리 등이 제공된다.

특히 외부 링크로 저장된 이미지를 디스플레이하는 데 효과적이다.

이 라이브러리는 이미지 로딩 처리 과정의 각 단계인 초기 HTTP 요청부터 이미지를 캐싱하는 데까지의 범위를 다룰 수 있다.

이러한 것을 모두 직접 구현하는 것은 꽤 장황한 코드가 될 수 있는데 이 라이브러리를 사용하면 간단히 구현할 수 있다.

```java
Picasso.get()
        .load("http://i.imgur.com/DvpvklR.png")
        .placeholder(R.drawable.img_default) // 실패 시 기본 이미지
        .resize(50,50) // 리사이즈
        .centerCrop() // 중앙 크롭 하기
        .into(picassoImageView);
```

웹사이트에서 로딩한 png파일을 이미지뷰인 imageView에 나타낸다.

하지만 대부분 이미지를 그냥 나타내는 경우 원본 이미지를 그대로 가져오려고 하기 때문에 imageView 사이즈가 고려되지 않는다.

이때는 `resize()`나 `fit()`함수를 사용해 명시적인 크기로 정하는 것이 좋다.

이미지 처리 함수를 통해 크롭하거나 placeholder()를 사용해 로드 실패 시 기본적으로 지정할 그림을 정해주면 좋다.

만일, 비율에 따른 사이즈가 필요하다면 `transformation()`을 사용할 수 있다.


  <br>

  ---

<font size="2em"> https://acaroom.net/ko/blog/youngdeok/%EC%97%B0%EC%9E%AC-%EC%BD%94%ED%8B%80%EB%A6%B0-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8-01-%EC%98%A4%ED%94%88%EC%86%8C%EC%8A%A4-%EB%9D%BC%EC%9D%B4%EB%B8%8C%EB%9F%AC%EB%A6%AC%EC%9D%98-%EC%9D%B4%ED%95%B4</font>
