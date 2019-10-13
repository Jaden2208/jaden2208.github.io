---
layout: post
title: "[STL] sort()"
categories:
  - Algorithm
tags:
  - sort()
  - algorithm
  - c++
last_modified_at: 2019-10-13T
---
<br>
### sort()
* c++ <algorithm> 헤더파일에 속한 함수이다.
* [퀵정렬](https://jaden2208.github.io/algorithm/2019/10/13/algorithm-quick-sort.html)을 기반으로 구현되어 있어 평균 시간복잡도는 O(n log n)이다.
* `sort(start, end)`를 이용해 [start, end) 범위에 있는 인자를 <span style="color:blue">오름차순</span> 으로 정렬해준다.
* 이때 <span style="color:blue">오름차순</span> 은 default 이고 별도의 함수를 추가해 <span style="color:green">내림차순</span> 으로 정렬할 수도 있다.

<br>

---

#### c++ 코드

```c++
#include <iostream>
#include <algorithm>

using namespace std;

bool compare(int a, int b){
	return a < b; // 현재 내림차순. 오름차순은 return a > b;
}
int main(){
	int a[10] = {9, 3, 5, 4, 1, 10, 8, 6, 7, 2};
	sort(a, a + 10, compare); // 기본 : sort(a, a+10)

	for(int i=0; i<10; i++){
		cout << a[i] << ' ';
	}
}
```

<br>

---

### 데이터를 묶어서 정렬하는 방법 (class)
위와 같은 단순 데이터 정렬 기법은 실무에서 사용하기에 적합하지 않다.
실무에서 프로그래밍 할 때는 모든 데이터들이 객체로 정리되어 내부적으로 여러 개의 변수를 포함하고 있기 때문이다.
이 경우 가장 중요한 정렬 방식은 **<span style="color:blue">특정한 변수를 기준으로</span>** 정렬하는 것이다.
```c++
#include <iostream>
#include <algorithm>
using namespace std;

class Student {
	public:
		string name;
		int score;
		Student(string name, int score){
			this->name = name;
			this->score = score;
		}
		// 정렬 기준은 '점수가 작은 순서'
		bool operator <(Student &student) {
			return this->score < student.score;
		}
};
int main(){
	Student students[] = {
		Student("이름1", 99),
		Student("이름2", 97),
		Student("이름3", 95),
		Student("이름4", 93),
		Student("이름5", 91)
	};
	sort(students, students + 5);
	for(int i=0; i<5; i++){
		cout << students[i].name << ' ';
	}
	return 0;
}
```

하지만 이와 같이 class를 이용해 구현하는 것은 <span style="color:green">프로그래밍 대회</span> 및 <span style="color:green">코딩 테스트</span> 등 에서는 적합하지 않다.

이 때 필요한 것이 **pair 라이브러리** 다.

**pair 라이브러리** 에 대한 예제 및 설명은 [여기(클릭)](https://jaden2208.github.io/algorithm/2019/10/13/algorithm-stl-sort-pair.html)에서 다루도록 하겠다.

<br>

---
<center><font size="2em"> 나동빈 님의 알고리즘 강의를 참고해 작성했습니다.</font></center>
