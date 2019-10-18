---
layout: post
title: "[정렬] 힙정렬 (Heap Sort)"
categories:
  - Algorithm
tags:
  - heap
  - sort
  - complete binary tree
  - algorithm
  - c++
last_modified_at: 2019-10-13T
---
<br>
### 힙 정렬
> *최대 힙 트리를 이용하여 정렬하기.*

---

##### 힙
최솟값이나 최댓값을 빠르게 찾아내기 위해 완전 이진트리를 기반으로 하는 트리형 자료구조.
<br>
##### 완전 이진트리
중간에 비어있는 것 없이 꽉 차있는 이진 트리.(왼쪽 부터 채워짐)
<br>
##### 최대 힙
부모 노드가 자식 노드보다 큰 힙.


---

* 힙 정렬을 하기 위해서는 데이터를 힙 구조로 만들어야 한다.

- 새로운 노드를 추가하다보면 최대 힙의 구조를 깨트리는 경우가 생긴다. 노드를 추가했는데 부모 노드가 새로 추가한 자식 노드의 어떤 값 보다 작은 경우다. 이 때는 부모 노드와 그 자식 노드의 값을 바꿔 주면 정상적으로 최대 힙 상태가 된다.

---

<br>

#### 다음의 숫자들을 오름차순으로 정렬하는 프로그램을 작성해보자
> 7 6 5 8 3 4 9 1 2


<center><img src="/images/heap_tree1.png" width="50%" height="50%"></center>

<br>

---
#### 1. 전체 트리 구조를 최대 힙 구조로 바꾼다.

- 루트 노드(7)를 제외하고 위에서 부터 차례로 비교해 더 큰 값이 있는 노드가 부모 노드 자리에 위치하도록 한다.

(1) 먼저, 자식노드 6 과 그 부모노드 7을 비교해보면, 더 큰 값이 부모 노드에 있으므로 pass 한다.

(2) 그 다음, 자식 노드 5와 부모노드 7을 비교해도 마찬가지이므로 pass 한다.

(3) 그리고, 자식노드 8과 부모노드 6과 비교하면, 이번에는 자식노드 값이 부모노드 값 보다 크므로 서로 바꿔준다.

<center><img src="/images/heap_tree2.png" width="50%" height="50%"></center>

<br>

---

(4) 위치가 바뀐 자식노드 8의 부모노드가 바뀌었다. 다시 한번 바뀐 부모노드 7과 비교한다. "자식노드 8 > 부모노드 7" 이므로 서로 위치를 바꿔준다.

<center><img src="/images/heap_tree3.png" width="50%" height="50%"></center>

<br>

---

(5) (1)~(4)의 과정을 반복한다.

```c++
for(int i=1; i<number; i++){

  int c = i; // 자식 노드의 인덱스

  while(c != 0){
    int root = (c - 1) / 2;  // 부모 노드의 인덱스

    if(heap[root] < heap[c]){

      int temp = heap[root];
      heap[root] = heap[c];
      heap[c] = temp;
    }
    c = root;
  }
}
```
<br>

[최대힙](#최대-힙) 구조로 정렬된 모습
<center><img src="/images/heap_tree4.png" width="50%" height="50%">
</center>

> 9 7 8 6 3 4 5 1 2

위의 과정을 거치면 루트 노드에는 가장 큰 값이 위치하게 된다.

<br>

---

#### 2. 크기를 줄여가며 반복적으로 힙을 구성한다.

(1) 루트 노드 9와 마지막 리프 노드 2의 위치를 서로 바꿔준다.

<center><img src="/images/heap_tree5.png" width="50%" height="50%">
</center>

<br>

---

(2) 그리고 루트 노드 2의 자식 노드들 중 큰 값 8을 찾아 그 자식 노드 8과 루트노드 2의 값을 비교해 자식이 더 크면 서로 교환한다.

<center><img src="/images/heap_tree6.png" width="50%" height="50%">
</center>

<br>

---

(3) 부모노드 2의 자식노드를 비교하여 (2)와 같은 방법으로 위치를 바꿔준다.

<center><img src="/images/heap_tree7.png" width="50%" height="50%">
</center>

- 배열의 맨 마지막 원소 9를 제외하고 나머지 노드들에 대해서 최대 힙 구조를 가지게 된다.

<br>

---

(4) 그리고 다시 2의 처음 과정부터 반복해서 진행한다.

<br>

```c++
for(int i=number-1; i>=0; i--){

  int temp = heap[0];
  heap[0] = heap[i];
  heap[i] = temp;

  int root = 0; // 루트 노드의 인덱스
  int c = 1;

  while(c < i){
    c = 2 * root + 1; // 자식 노드의 인덱스

    // 자식 중에 더 큰 값 찾기
    if(heap[c] < heap[c+1] && c < i - 1){
      c++;
    }

    // 루트보다 자식이 더 크다면 교환
    if(heap[root] < heap[c] && c < i){
      int temp = heap[root];
      heap[root] = heap[c];
      heap[c] = temp;
    }

    root = c;
  }
}
```

---
#### 전체 c++ 코드

```c++
#include <iostream>
using namespace std;
int main(){

	int heap[9] = {7, 6, 5, 8, 3, 4, 9, 1, 2};
	int number = 9;

	// 전체 트리 구조를 힙 구조로 바꾼다.
	for(int i=1; i<number; i++){

		int c = i; // 자식 노드의 인덱스

		while(c != 0){
			int root = (c - 1) / 2;  // 부모 노드의 인덱스

			if(heap[root] < heap[c]){

				int temp = heap[root];
				heap[root] = heap[c];
				heap[c] = temp;
			}
			c = root;
		}
	}

	// 크기를 줄여가며 반복적으로 힙을 구성
	for(int i=number-1; i>=0; i--){

		int temp = heap[0];
		heap[0] = heap[i];
		heap[i] = temp;

		int root = 0; // 루트 노드의 인덱스
		int c = 1;

		while(c < i){
			c = 2 * root + 1; // 자식 노드의 인덱스

			// 자식 중에 더 큰 값 찾기
			if(heap[c] < heap[c+1] && c < i - 1){
				c++;
			}

			// 루트보다 자식이 더 크다면 교환
			if(heap[root] < heap[c] && c < i){
				int temp = heap[root];
				heap[root] = heap[c];
				heap[c] = temp;
			}

			root = c;
		}
	}

	for(int i=0; i<number; i++){
		cout << heap[i] << ' ';
	}

	return 0;
}
```
---

#### 시간 복잡도 O(n log n)
한번 힙 구조를 만드는데에(heapify) 드는 시간은 트리 구조로 인해 log n 이다.
그리고 n개의 수 만큼 반복해야 하기 때문에 n * log n 의 시간 비용이 든다.

<br>

---
#### 기타 설명

* [병합정렬](https://jaden2208.github.io/algorithm/2019/10/13/algorithm-merge-sort.html)과 다르게 별도로 추가적인 배열이 필요하지 않기 때문에 메모리 측면에서 효율적이다.

* 또한 시간복잡도가 항상 O(n log n)이지만 이론적으로는 [퀵정렬](https://jaden2208.github.io/algorithm/2019/10/13/algorithm-quick-sort.html), [병합정렬](https://jaden2208.github.io/algorithm/2019/10/13/algorithm-merge-sort.html) 보다 더 우위에 있다고 할 수 있다.

* 하지만 단순히 속도만 가지고 비교하면 [퀵정렬](https://jaden2208.github.io/algorithm/2019/10/13/algorithm-quick-sort.html)이 평균적으로 더 빠르기 때문에 힙정렬이 일반적으로 많이 사용되지는 않는다.

<br>

---

<center><font size="2em"> 나동빈 님의 알고리즘 강의를 참고해 작성했습니다.</font></center>
