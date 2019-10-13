---
layout: post
title: "[정렬] 삽입정렬 (Insertion Sort)"
categories:
  - Algorithm
tags:
  - insertion
  - sort
  - algorithm
  - c++
last_modified_at: 2019-10-11T
---
<br>
### 삽입 정렬
> *각 숫자를 적절한 위치에 값을 넣어주기.*

<br>
#### 다음의 숫자들을 오름차순으로 정렬하는 프로그램을 작성해보자
> 1 10 5 8 7 6 4 3 2 9
---
* 맨 앞에 위치한 1은 스킵

<br>
##### 10은 1의 앞 또는 뒤로 들어갈 수 있는데, 1보다 크므로 뒤에 위치시킨다.
> <span style="color:red">1 10</span> 5 8 7 6 4 3 2 9

<br>
##### 5는 _ 1 _ 10 _ 다음의 자리에 위치할 수 있다. 먼저 10과 비교하여 5가 더 작다면 다음 1과 비교한다.

<br>
##### 1과 비교하여 5가 더 클 때 10과 5의 위치를 바꾼다.
> <span style="color:red">1 5 10</span> 8 7 6 4 3 2 9

<br>
##### 이 같은 과정을 반복한다.
---
#### c++ 코드
```c++
#include <iostream>
using namespace std;
int main(){
	int temp;
	int array[10] = {1, 10, 5, 8, 7, 6, 4, 3, 2, 9};

	for(int i=0; i<9; i++){
		for(int j=i; array[j] > array[j+1]; j--){
			temp = array[j];
			array[j] = array[j+1];
			array[j+1] = temp;
		}
	}

	for(int i=0; i<10; i++){
		cout << array[i];
	}

	return 0;
}
```
---
#### 시간 복잡도 O(n<sup>2</sup>)
선택정렬, 버블정렬과 동일한 O(n<sup>2</sup>) 이지만
원소 간의 이동이 **필요한 만큼만** 이루어지므로 [선택](https://jaden2208.github.io/algorithm/2019/10/10/algorithm-insertion-sort.html), [버블](https://jaden2208.github.io/algorithm/2019/10/11/algorithm-bubble-sort.html), [삽입](#삽입-정렬)정렬 중에서는 **가장 효율적** 인 알고리즘이다.

<br>

---

<center><font size="2em"> 나동빈 님의 알고리즘 강의를 참고해 작성했습니다.</font></center>
