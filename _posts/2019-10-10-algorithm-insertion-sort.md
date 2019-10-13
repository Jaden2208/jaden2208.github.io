---
layout: post
title: "[정렬] 선택정렬 (Insertion Sort)"
categories:
  - Algorithm
tags:
  - selection
  - sort
  - algorithm
  - c++
last_modified_at: 2019-10-10T
---
<br>
### 선택 정렬
> *가장 작은 값을 찾아 맨 앞으로 보내기.*

<br>
#### 다음의 숫자들을 오름차순으로 정렬하는 프로그램을 작성해보자
> 1 10 5 8 7 6 4 3 2 9
---
##### 처음부터 끝까지 확인해 <span style="color:red">가장 작은 값</span>을 찾아서 가장 앞에 있는 원소와 위치를 바꾼다.
> <span style="color:red">1</span> 10 5 8 7 6 4 3 2 9

<br>
##### 맨 앞 원소를 제외하고 그 다음부터 끝까지 확인해 <span style="color:red">가장 작은 값</span>을 찾아서 마찬가지로 <span style="color:blue">가장 앞에 있는 원소</span> ~~(맨 앞 원소(1) 제외)~~ 와 위치를 바꾼다.
> 1 <span style="color:red">2</span> 5 8 7 6 4 3 10 9

<br>
##### 이 과정을 반복한다.
<br>

---
#### c++ 코드
```c++
#include <iostream>
using namespace std;
int main(){
	int min, index, temp;
	int array[10] = {1, 10, 5, 8, 7, 6, 4, 3, 2, 9};

	for(int i=0; i<10; i++){
		min = 9999;
		for(int j=i; j<10; j++){
			if(min > array[j]){
				min = array[j];
				index = j;
			}
		}
		temp = array[i];
		array[i] = array[index];
		array[index] = temp;
	}

	for(int i=0; i<10; i++){
		cout << array[i];
	}

	return 0;
}
```
---
#### 시간 복잡도 O(n<sup>2</sup>)
10 + 9 + 8 + ... + 1 번, 즉 10 * (10 + 1) / 2 번의 비교 연산이 이루어진다.
n개의 원소를 정렬하는데 필요한 연산 횟수는 n * (n + 1) / 2 이므로 O(n<sup>2</sup>) 만큼의 시간 복잡도를 가진다고 할 수 있다.

<br>

---

<center><font size="2em"> 나동빈 님의 알고리즘 강의를 참고해 작성했습니다.</font></center>
