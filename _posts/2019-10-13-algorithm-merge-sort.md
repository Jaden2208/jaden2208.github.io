---
layout: post
title: "[정렬] 병합정렬 (Merge Sort)"
categories:
  - Algorithm
tags:
  - merge
  - sort
  - algorithm
  - c++
last_modified_at: 2019-10-13T
---
<br>
### 병합 정렬
> *일단 반으로 쪼개고 나중에 합쳐서 정렬하기.*

<br>

##### 1. 리스트를 반씩 쪼개는 것을 연결된 모든 원소들이 각각 분리된 원소가 될 때 까지 반복한다.(재귀)

##### 2. 분리된 리스트를 두개 씩 반복해서 묶어(병합) 하나의 리스트로 합친다.

<br>

<center>
<img src="/images/merge.png" width="80%" height="80%">

[그림 출처 : [코린이의 얕은 블로그](https://sexycoder.tistory.com/73)]
</center>
<br>

#### 다음의 숫자들을 오름차순으로 정렬하는 프로그램을 작성해보자
> 7 6 5 8 3 4 9 1

<br>

---
#### c++ 코드
```c++
#include <iostream>
using namespace std;

int number = 8;
int sorted[8]; // 정렬 배열은 반드시 전역 변수로 선언

void merge(int a[], int start, int middle, int end){
	int i = start;
	int j = middle + 1;
	int k = start;
	// 작은 순서대로 배열에 삽입
	while(i <= middle && j <=end){
		if(a[i] <= a[j]){
			sorted[k] = a[i];
			i++;
		}else{
			sorted[k] = a[j];
			j++;
		}
		k++;
	}
	// i가 먼저 끝나거나, j가 먼저 끝난 경우, 남은 데이터도 삽입
	if(i > middle){
		for(int t=j; t<=end; t++){
			sorted[k] = a[t];
			k++;
		}
	} else {
		for(int t=i; t<=middle; t++){
			sorted[k] = a[t];
			k++;
		}
	}
	// 정렬된 배열을 삽입
	for(int t=start; t<=end; t++){
		a[t] = sorted[t];
	}
}

void mergeSort(int a[], int start, int end){
	// 크기가 1보다 큰 경우
	if(start < end){
		int middle = (start + end) / 2;
		mergeSort(a, start, middle);
		mergeSort(a, middle + 1, end);
		merge(a, start, middle, end);
	}
}

int main(){
	int array[number] = {7, 6, 5, 8, 3, 4, 9, 1};
	mergeSort(array, 0, number - 1);
	for(int i = 0; i < number; i++){
		cout << array[i] << " ";
	}

	return 0;
}
```
---
#### 시간 복잡도 O(n log n)
데이터의 개수 : n개
분할정복으로 인한 연산횟수 : log n

=>O(n log n)
: 최악의 경우에도 마찬가지다.

[퀵정렬](https://jaden2208.github.io/algorithm/2019/10/13/algorithm-quick-sort.html)의 경우에는 최악의 경우에 O(n<sup>2</sup>)이지만 **병합정렬** 은 [퀵정렬](https://jaden2208.github.io/algorithm/2019/10/13/algorithm-quick-sort.html)과 다르게 정확히 반절씩 나누어 주기 때문이다.
<br>

---

<center><font size="2em"> 나동빈 님의 알고리즘 강의를 참고해 작성했습니다.</font></center>
