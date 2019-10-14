---
layout: post
title: "[STL] sort()-pair 라이브러리"
categories:
  - Algorithm
tags:
  - sort()
  - pair
  - vector
  - algorithm
  - c++
last_modified_at: 2019-10-13T
---
<br>
### pair 라이브러리

말 그대로 한 쌍(pair)으로 데이터를 묶어서 처리할 수 있게 해주는 라이브러리다.

<br>

#### c++ 코드
```c++
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;
int main(){
	vector<pair<int, string> > v;
	v.push_back(pair<int, string>(98, "이름1"));
	v.push_back(pair<int, string>(96, "이름2"));
	v.push_back(pair<int, string>(94, "이름3"));
	v.push_back(pair<int, string>(92, "이름4"));
	v.push_back(pair<int, string>(90, "이름5"));

	sort(v.begin(), v.end());

	for(int i=0; i<v.size(); i++){
		cout << v[i].second << ' ';
	}
	return 0;
}
```

<br>

---
##### 다음 문제를 풀어보자.
> 학생을 나타낼 수 있는 정보가 이름, 성적, 생년월일일 때 학생을 성적 순서대로 나열하고자 한다. 다만 성적이 동일한 경우 나이가 더 어린 학생이 더 우선순위가 높다.

**[학생 명단]**
이름1 / 92점 / 1996-01-01 <br>
이름2 / 96점 / 1993-02-02 <br>
이름3 / 94점 / 1994-03-03 <br>
이름4 / 92점 / 1992-04-04 <br>
이름5 / 90점 / 1994-05-05 <br>


<br>
#### c++ 코드
```c++
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

bool compare(pair<string, pair<int, int> > a, pair<string, pair<int, int> > b){
	if(a.second.first == b.second.first){ // 성적이 같다면
		return a.second.second > b.second.second; // 생년월일값이 더 큰(더 어린)게 우선으로!
	} else{
		return a.second.first > b.second.first;
	}
}

int main(void){
	vector<pair<string, pair<int, int> > > v;
	v.push_back(pair<string, pair<int, int> > ("이름1", pair<int, int>(92, 19960101)));
	v.push_back(pair<string, pair<int, int> > ("이름2", pair<int, int>(96, 19930202)));
	v.push_back(pair<string, pair<int, int> > ("이름3", pair<int, int>(94, 19940303)));
	v.push_back(pair<string, pair<int, int> > ("이름4", pair<int, int>(92, 19920404)));
	v.push_back(pair<string, pair<int, int> > ("이름5", pair<int, int>(90, 19940505)));

	sort(v.begin(), v.end(), compare);
	for(int i=0; i<v.size(); i++){
		cout << v[i].first << ' ';
	}

}
```

<br>

---

<center><font size="2em"> 나동빈 님의 알고리즘 강의를 참고해 작성했습니다.</font></center>
