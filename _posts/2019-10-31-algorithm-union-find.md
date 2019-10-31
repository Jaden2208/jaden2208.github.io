---
layout: post
title: "합집합 찾기 : Union-Find"
categories:
  - Algorithm
tags:
  - union find
  - algorithm
  - c++
last_modified_at: 2019-10-31T
---
<br>
### Union-Find
 > = 서로소 집합(Disjoint-Set) 알고리즘

여러 개의 노드가 존재할 때 두 개의 노드를 선택해서, 현재 이 두 노드가 서로 같은 그래프에 속하는지 판별하는 프로그램을 작성하려고 한다.

<br>

---

>그림1 ![union_find1](/images/union_find1.png)

그림1에 대해서 다음과 같이 리스트 형식으로 노드를 저장한다.

|노드|1|2|3|4|5|6|7|8|
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
|부모노드|1|2|3|4|5|6|7|8|

---

그리고 위의 그림1에서 1과 2를 연결하면 아래와 같은 그래프가 된다.

>그림2 ![union_find2](/images/union_find2.png)

---

이때 리스트 값을 아래와 같이 변경해준다.

|노드|1|2|3|4|5|6|7|8|
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
|부모노드|1|1|3|4|5|6|7|8|

1과 2가 연결된 것을 i=2의 값(j)을 1로 바꿔줌으로써 연결된 노드임을 표현한 것이다.

<br>

이때 1을 2로 바꾸는 것이 아니라 더 작은 값쪽으로, 즉 2를 1로 바꿔야한다.

---

여기에 아래 그림3과 같이 2와 3을 연결하면

>그림3 ![union_find3](/images/union_find3.png)

리스트는 아래와 같이 변경된다.

|노드|1|2|3|4|5|6|7|8|
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
|부모노드|1|1|2|4|5|6|7|8|

---

하지만 (i=)1과 3은 값(j)이 각각 1과 2로 다르기 때문에 연결된 상태임에도 불구하고 연결된 상태임을 파악할 수 없다.

<br>

<u> 이러한 문제를 해결하는 방법이 **Union-Find** 의 핵심이다. </u>

이때 필요한 것이 재귀 함수이다.

3의 부모를 찾기 위해서는 먼저 3이 가리키고 있는 2를 찾고 2의 부모가 1을 가리키므로, 아래와 같이 리스트를 수정해준다.

|노드|1|2|3|4|5|6|7|8|
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
|부모노드|1|1|1|4|5|6|7|8|

노드 1, 2, 3의 부모가 모두 1이기 때문에 세 가지 노드는 모두 같은 그래프에 속한다고 할 수 있다. 이것이 **Union-Find** 의 전부이다.

---

#### 예제 코드

```c++
#include <iostream>

using namespace std;

// 부모 노드를 찾는 함수  
int getParent(int parent[], int x){
	if(parent[x] == x) return x;
	return parent[x] = getParent(parent, parent[x]);
}

// 두 부모 노드를 합치는 함수
int unionParent(int parent[], int a, int b){
	a = getParent(parent, a);
	b = getParent(parent, b);
	if(a < b) parent[b] = a;
	else parent[a] = b;
}

// 같은 부모를 가지는지 확인
bool isSameParent(int parent[], int a, int b){
	a = getParent(parent, a);
	b = getParent(parent, b);
	if(a == b) return 1;
	return 0;
}
int main(){
	int parent[11];
	for(int i=1; i<10; i++){
		parent[i] = i;
	}

	unionParent(parent, 1, 2);
	unionParent(parent, 2, 3);
	unionParent(parent, 3, 4);
	unionParent(parent, 5, 6);
	unionParent(parent, 6, 7);
	unionParent(parent, 7, 8);

	cout << "1과 5는 연결되어 있나요? ";
	cout << isSameParent(parent, 1, 5);
	cout << "\n";

	unionParent(parent, 1, 7);

	cout << "1과 5는 연결되어 있나요? ";
	cout << isSameParent(parent, 1, 5);

	return 0;

}
```

---
<center><font size="2em"> 나동빈 님의 알고리즘 강의를 참고해 작성했습니다.</font></center>
