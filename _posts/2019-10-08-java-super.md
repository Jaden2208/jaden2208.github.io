---
layout: post
title: super 키워드와 super() 메소드
categories:
  - Java
tags:
  - super
  - java
last_modified_at: 2019-10-08T
---
<br>
### super 키워드
> *부모 클래스로부터 상속받은 필드(클래스 안에서 선언되는 멤버 변수)나 메소드를 자식 클래스에세 참조하는 데 사용하는 참조 변수*

<br>

인스턴스 변수의 이름과 지역 변수의 이름이 같을 경우 인스턴스 변수 앞에 [this 키워드](https://jaden2208.github.io/java/2019/10/08/java-this.html)를 사용하여 구분할 수 있다. 이와 마찬가지로 부모 클래스의 멤버와 자식 클래스의 멤버 이름이 같을 경우 super 키워드를 사용하여 구별할 수 있다.
<br>

#### 예제 코드
```java
class Parent {
	int a = 10;
}

class Child extends Parent{
	int a = 20;

	void display() {
		System.out.println(a); // 20
		System.out.println(this.a); // 20
		System.out.println(super.a); // 10
	}
}

public class Main {

	public static void main(String[] args) {
		Child ch = new Child();
		ch.display();
	}

}
```

<br>
#### 실행 결과
```
20
20
10
```
<br>

---

### super() 메소드
> *[this() 메소드](https://jaden2208.github.io/java/2019/10/08/java-this.html)가 같은 클래스의 다른 생성자를 호출할 때 사용된다면, super() 메소드는 부모 클래스의 생성자를 호출할 때 사용된다.*

<br>
자식 클래스의 인스턴스를 생성하면, 해당 인스턴스에는 자식 클래스의 고유 멤버뿐만 아니라 부모 클래스의 모든 멤버까지도 포함되어 있다.

따라서 부모 클래스의 멤버를 초기화하기 위해서는 자식 클래스의 생성자에서 부모 클래스의 생성자까지 호출해야 한다.

자바 컴파일러는 부모 클래스의 생성자를 명시적으로 호출하지 않는 모든 자식 클래스의 생성자 첫 줄에 자동으로 super(); 명령문을 추가하여, 부모 클래스의 멤버를 초기화할 수 있도록 해준다.

<br>
#### 예제 코드
```java
class Parent{
	int a;
	Parent(){
		a = 10;
		System.out.println("1");
	}
	Parent(int n){
		a = n;
		System.out.println("2");
	}
}

class Child extends Parent{
	int b;
	Child(){
		// 자바 컴파일러는 이 곳에 자동으로 super(); 구문을 삽입한다.
		// 하지만 이 주석 처리를 해제하고 실행하면, 부모 클래스인 Parent 클래스는 두번째 생성자에 의해
		// a는 40으로 초기화 된다.
//		super(40);
		System.out.println("3");

		b = 20;
	}
	void display() {
		System.out.println(a);
		System.out.println(b);
	}
}

public class Main {

	public static void main(String[] args) {
		Child ch = new Child();
		ch.display();

	}

}
```
<br>
#### 실행 결과
```
1
3
10
20
```
---
###### 참고 사이트
 http://tcpschool.com/
