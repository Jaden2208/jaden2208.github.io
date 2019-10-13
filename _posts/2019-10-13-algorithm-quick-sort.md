---
layout: post
title: "[정렬] 퀵정렬 (Quick Sort)"
categories:
  - Algorithm
tags:
  - quick
  - sort
  - algorithm
  - c++
last_modified_at: 2019-10-13T
---
<br>
### 퀵 정렬
> *특정한 값(pivot)(보통 맨 앞의 값)을 기준으로 왼쪽에서부터 pivot보다 큰 값을, 오른쪽에서부터 pivot보다 작은 값을 찾아 각각 바꿔주기.*

<br>
#### 다음의 숫자들을 오름차순으로 정렬하는 프로그램을 작성해보자
> 3 7 8 1 5 9 6 10 2 4

---
##### 1. 맨 앞 값을 <span style="color:red">pivot</span> 값으로 정해준다. <span style="color:red">pivot</span> = 3
> <span style="color:red">3</span> 7 8 1 5 9 6 10 2 4

<br>
##### 2. <span style="color:red">pivot</span> 값을 제외하고 왼쪽에서부터는 <span style="color:red">pivot</span> 보다 큰 값을, 오른쪽에서부터는 <span style="color:red">pivot</span> 보다 작은 값을 찾아서 서로 바꾼다.
><span style="color:red">3</span> <span style="color:blue">2</span> 8 1 5 9 6 10 <span style="color:blue">7</span> 4

<br>
##### 3. 2 반복
> <span style="color:red">3</span> 2 <span style="color:blue">1 8</span> 5 9 6 10 7 4

<br>
##### 4. 또 다시 2 반복?
이번엔 8과 1인데, 서로 위치가 엇갈려있다. 다시 말해 3보다 큰 값이 3보다 작은 값보다 더 뒤에 있다.

<br>
##### 5. 이렇게 엇갈렸을 때 <span style="color:blue">왼쪽의 값</span>과 <span style="color:red">pivot</span> 값을 서로 바꿔준다.
> <span style="color:blue">1</span> 2 <span style="color:red">3</span> 8 5 9 6 10 7 4

<br>
##### 6. pivot 값을 기준으로 왼쪽에는 더 작은 값들이, 오른쪽에는 더 큰 값들이 위치하게 된다.

<br>
##### 7. 양쪽 모두에서 1~5의 과정을 반복해준다.

<br>

---
#### c++ 코드
```c++
#include <iostream>
using namespace std;

int array[10] = {3, 7, 8, 1, 5, 9, 6, 10, 2, 4};

void show(){
	for(int i=0; i<10; i++){
		cout << array[i] << ' ';
	}
	cout << endl;
}

void QuickSort(int* array, int start, int end){
	if(start >= end) { // 원소가 1개인 경우 그대로 두기
		return;
	}
	int key = start;
	int i = start + 1; // 왼쪽 출발 지점
	int j = end; // 오른쪽 출발 지점
	int temp;

	while(i <= j){ // 엇갈릴 때까지 반복
		while(array[i] <= array[key]){ // 키 값보다 큰 값을 만날 때 까지 오른쪽으로 이동  
			i++;
		}
		while(j > start && array[j] >= array[key]){ // 키 값보다 작은 값을 만날 때 까지 왼쪽으로 이동
			j--;
		}
		if(i > j){ // 현재 엇갈린 상태면 키 값과 교체
			temp = array[j];
			array[j] = array[key];
			array[key] = temp;
		}
		else { // 엇갈리지 않았다면 i와 j를 교체
			temp = array[i];
			array[i] = array[j];
			array[j] = temp;
		}
	}
	QuickSort(array, start, j-1);
	QuickSort(array, j+1, end);

}

int main(){
	QuickSort(array, 0, 9);
	show();

	return 0;
}
```
---
#### 시간 복잡도 O(n log n)
데이터의 개수 : n개
분할정복으로 인한 연산횟수 : log n

=>O(n log n)
: 최악의 경우에는 O(n<sup>2</sup>)이다.

다 정렬 되어있는 경우에는 분할의 이점을 활용하지 못한다.
정렬이 되어있는 경우에는 [삽입정렬](https://jaden2208.github.io/algorithm/2019/10/11/algorithm-insertion-sort.html)을 통해 퀵정렬보다 더 빠르게 풀어낼 수 있다.
<br>
*퀵정렬이 무조건 빠른 것은 아니다!*
<br>

---

<center><font size="2em"> 나동빈 님의 알고리즘 강의를 참고해 작성했습니다.</font></center>
