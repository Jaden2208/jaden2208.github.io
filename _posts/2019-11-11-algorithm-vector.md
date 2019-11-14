---
layout: post
title: "[STL] 벡터 (vector)"
categories:
  - Algorithm
tags:
  - stl
  - vector
  - algorithm
  - c++
last_modified_at: 2019-11-11T
---
<br>
### 벡터(vector)
일반적인 배열처럼 개체들을 연속적인 메모리 공간에 저장.

<br>

---

#### 생성자
|생성자|설명|
|:-:|:-:|
|`vector v`|v는 빈 컨테이너 이다.|
|`vector v(n,x)`|v는 x 값으로 초기화된 n개의 원소를 갖는다.|
|`vector v(v2)`|v는 v2 컨테이너의 복사본이다.(복사 생성자 호출)|
|`vector v(b,e)`|v는 반복자 구간 [b,e)로 초기화된 원소를 갖는다.|


#### 멤버 함수
|멤버 함수|설명|
|:-:|:-:|
|` v.assign(n,x)`|v에 x 값으로 n개의 원소를 할당한다|
|`v.assign(b,e)`|v를 반복자 구간 [b,e)로 할당한다.|
|`v.at(i)`|v의 i번째 원소를 참조한다.|
|`v.back()`|v의 마지막 원소를 참조한다.|
|`p=v.begin()`|p는 v의 첫 원소를 가리키는 반복자|
|`x=v.capacity()`|x는 v에 할당된 공간의 크기|
|`v.clear()`|v의 모든 원소를 제거한다.|
|`v.empty()`|v가 비었는지 조사한다.|
|`p=v.end()`|p는 v의 끝을 표식하는 반복자|
|`p=v.erase(p)`|p가 가리키는 원소를 제거한다. q는 다음 원소를 가리킨다.|
|`q=v.erase(b,e)`|반복자 구간 [b,e)의 모든 원소를 제거한다. q는 다음 원소|
|`v.front()`|v의 첫 번째 원소를 참조한다.|
|`q=v.insert(p,x)`|p가 가리키는 위치에 x 값을 삽입한다. q는 삽입한 원소를 가리키는 반복자다.|
|`v.insert(p,n,x)`|p가 가리키는 위치에 n개의 x 값을 삽입한다.|
|`v.insert(p,b,e)`|p가 가리키는 위치에 반복자 구간 [b,e)의 원소를 삽입한다.|
|`x=v.max_size()`|x는 v가 담을 수 있는 최대 원소의 개수(메모리의 크기)|
|`v.pop_back()`|v의 마지막 원소를 제거한다.|
|`v.push_back()`|v의 끝에 x를 추가한다.|
|`p=v.rbegin()`|p는 v의 역 순차열의 첫 원소를 가리키는 반복자다.|
|`p=v.rend()`|p는 v의 역 순차열의 끝을 표식하는 반복자|
|`v.reserve(n)`|n개의 원소를 저장할 공간을 예약한다.|
|`v.resize(n)`|v의 크기를 n으로 변경하고 확장되는 공간의 값을 기본값으로 초기화 한다.|
|`v.size()`|v의 원소 갯수|
|`v.swap(v2)`|v와 v2를 swap한다.|


<br>

---
###### 참고 사이트
https://hyeonstorage.tistory.com/324
