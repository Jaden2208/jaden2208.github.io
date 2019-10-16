---
layout: post
title: "[정렬] 계수정렬 (Counting Sort)"
categories:
  - Algorithm
tags:
  - counting
  - sort
  - algorithm
  - c++
last_modified_at: 2019-10-16T
---
<br>
### 계수 정렬
> *크기를 기준으로 개수를 세기.*

---

<br>

#### 다음의 숫자들을 오름차순으로 정렬하는 프로그램을 작성해보자
> 1 3 2 4 3 2 5 3 1 2 3 4 4 3 5 1 2 3 5 2 3 1 4 3 5 1 2 1 1 1

---

위의 데이터들은 전부 1에서 5 사이에 속해있다.
이와 같이 **'범위 조건'** 이 있는 경우에 한해서 굉장히 빠른 알고리즘이 있다.
바로 계수 정렬 알고리즘이다.
**그 속도는 무려 O(n)이다.**

---

#### 1. 앞에서 순서대로 1, 2, 3, 4, 5에 대해서 각각의 숫자가 나오면 배열'1, 2, 3, 4, 5'의 값을 하나씩 증가시킨다.
[결과]
|1|2|3|4|5|
|:-:|:-:|:-:|:-:|:-:|
|8|6|8|4|4|

#### 2. 그리고 1을 8번, 2를 6번, 3을 8번, ... 이런식으로 출력한다.

<br>

#### 3. 끝.

<br>

---

#### c++ 코드

```c++
#include <iostream>
using namespace std;
int main(){
	int n = 30;
	int array[n] = {1, 3, 2, 4, 3, 2, 5, 3, 1, 2,
					3, 4, 4, 3, 5, 1, 2, 3, 5, 2,
					 3, 1, 4, 3, 5, 1, 2, 1, 1, 1};
	int count[5] = {0, 0, 0, 0, 0};

	for(int i=0; i<n; i++){
		if(array[i] == 1)
			count[0]++;
		else if(array[i] == 2)
			count[1]++;
		else if(array[i] == 3)
			count[2]++;
		else if(array[i] == 4)
			count[3]++;
		else
			count[4]++;
	}

	for(int i=0; i<5; i++){
		if(count[i] != 0){
			for(int j=0; j<count[i]; j++){
				cout << i+1 << ' ';
			}
		}
	}
}
```

#### 시간 복잡도 O(n)
배열의 값 들을 순서대로 한번씩 확인하는게 전부이기 때문에 O(n) 만큼만 시간비용이 발생한다.

<br>

---

<center><font size="2em"> 나동빈 님의 알고리즘 강의를 참고해 작성했습니다.</font></center>
