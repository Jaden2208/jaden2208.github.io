---
layout: post
title: "디자인 패턴이란?"
categories:
  - Design Pattern
tags:
  - design
  - pattern
  - solid
last_modified_at: 2019-10-13T
---
*<center> "Don't reinvent the whell." </center>*
<br>
> 소프트웨어를 설게할 때 득정 맥락에서 자주 발생하는 고질적인 문제들이 또 발생했을 때 재사용할 수 있는 훌륭한 해결책

<br>
#### 패턴이란
 * 각기 다른 소프트웨어 모듈이나 기능을 가진 다양한 응용 소프트웨어 시스템들을 개발할 때도 서로 간의 공통되는 설계 문제가 존재하며 이를 처리하는 해결책 사이에도 공통점이 있다. 이러한 유사점을 **패턴** 이라 한다.
 * **패턴** 은 공통의 언어를 만들어주며 팀원 사이의 의사 소통을 원활하게 해주는 아주 중요한 역할을 한다.

---

#### 디자인 패턴 구조
 * Context
   - 문제가 발생하는 여러 상황을 기술한다. 즉, 패턴이 적용될 수 있는 상황을 나타낸다.
   - 경우에 따라서는 패턴이 유용하지 못한 상황을 나타내기도 한다.
 * Problem
   - 패턴이 적용되어 해결될 필요가 있는 여러 디자인 이슈들을 기술한다.
   - 이 때 여러 제약사항과 영향력도 문제해결을 위해 고려해야 한다.
 * Solution
   - 문제를 해결하도록 설계를 구성하는 요소들과 그 요소들 사이의 관계, 책임, 협력 관계를 기술한다.
<br>

---

#### SOLID 원칙
 > 객체 지향 설계에서 지켜줘야 할 5개의 원칙

 S(SRP) 단일 책임 원칙 (Single Responsibility Principle)
 : 한 클래스는 하나의 책임만 가져야 한다.

 O(OCP) 개방-폐쇄 원칙 ( Open/Closed Principle)
 : 소프트웨어 요소는 확장에는 열려 있으나 변경에는 닫혀 있어야 한다.

 L(LSP) 리스코프 치환 원칙 (Liskov Substitution Principle)
 : 프로그램의 객체는 프로그램의 정확성을 깨뜨리지 않으면서 하위 타입의 인스턴스로 바꿀 수 있어야 한다.

 I(ISP) 인터페이스 분리 원칙 (Interface Segregation Principle)
 : 특정 클라이언트를 위한 인터페이스 여러 개가 범용 인터페이스 하나보다 낫다.

 D(DIP) 의존관계 역전 원칙 (Depenedency Inversion Principle)
 : 프로그래머는 추상화에 의존해야지, 구체화에 의존하면 안된다.


  <br>

  ---
  
  ###### 참고 사이트
  https://gmlwjd9405.github.io/2018/07/06/design-pattern.html
  https://brunch.co.kr/@oemilk/12
