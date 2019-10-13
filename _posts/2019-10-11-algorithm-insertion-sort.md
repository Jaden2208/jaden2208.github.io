---
layout: post
title: "[정렬] 버블정렬 (Bubble Sort)"
categories:
  - Algorithm
tags:
  - bubble
  - sort
  - algorithm
  - c++
last_modified_at: 2019-10-11T
---
<br>
### 버블 정렬
> *바로 옆에 있는 값과 비교해서 더 작은 값을 앞으로 보내기.*

<br>
#### 다음의 숫자들을 오름차순으로 정렬하는 프로그램을 작성해보자
> 1 10 5 8 7 6 4 3 2 9
---
##### 1. 가장 앞에 있는 원소부터, 즉, 1과 10을 비교해 더 작은 것을 앞으로 오도록 바꾼다.
> <span style="color:red">1</span> 10 5 8 7 6 4 3 2 9

<br>
##### 2. 두번째 원소와 그 다음 원소, 즉, 10과 5를 비교해 <span style="color:red">더 작은 것</span>을 앞으로 오도록 바꾼다.
> 1 <span style="color:red">5</span> 10 8 7 6 4 3 2 9

<br>
##### 3. 이 같은 과정을 끝까지 반복한다.
> 그러면 가장 큰 값인 10이 맨 뒤에 위치하게 된다.

<br>
##### 4. 가장 뒤에 있는 원소(10)를 제외하고 다음 원소부터 위 1~3의 과정을 반복한다.

<br>
##### 5. 4의 과정을 반복한다.
---
#### c++ 코드
```c++
#include <iostream>
using namespace std;
int main(){
	int temp;
	int array[10] = {1, 10, 5, 8, 7, 6, 4, 3, 2, 9};

	for(int i=0; i<10; i++){
		for(int j=0; j<9-i; j++){
			if(array[j] > array[j+1]){
				temp = array[j];
				array[j] = array[j+1];
				array[j+1] = temp;
			}
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
10 + 9 + 8 + ... + 1 번, 즉 10 * (10 + 1) / 2 번의 비교 연산이 이루어진다.
따라서 시간복잡도는 [선택정렬](https://jaden2208.github.io/algorithm/2019/10/10/algorithm-insertion-sort.html)과 동일한 O(n<sup>2</sup>)이다. 하지만 [선택정렬](https://jaden2208.github.io/algorithm/2019/10/10/algorithm-insertion-sort.html)과 다르게 swap이 계속해서 이루어지므로 **더 비효율적** 인 알고리즘이다.

<br>

---

<center><font size="2em"> 나동빈 님의 알고리즘 강의를 참고해 작성했습니다.</font></center>
