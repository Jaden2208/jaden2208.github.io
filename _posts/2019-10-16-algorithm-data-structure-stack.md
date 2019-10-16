---
layout: post
title: "[자료구조] 스택 (Stack)"
categories:
  - Algorithm
tags:
  - stack
  - data structure
  - algorithm
  - c++
last_modified_at: 2019-10-16T
---
<br>
### 스택(Stack) : 후입선출
나중에 들어온 것이 먼저 나간다.

(반대 : [큐(Queue)](https://jaden2208.github.io/algorithm/2019/10/16/algorithm-data-structure-queue.html) 는 선입선출)

<br>

---

#### c++ 코드

```c++
#include <iostream>
#include <stack>

using namespace std;

int main(){
	stack<int> s;
	s.push(7);  // 7
	s.push(5);	// 7, 5
	s.push(4);	// 7, 5, 4
	s.pop();	// 7, 5    (4)-->out

	while(!s.empty()){
		cout << s.top() << ' ';
		s.pop();
	}

	return 0;
}
```

<br>

---
<center><font size="2em"> 나동빈 님의 알고리즘 강의를 참고해 작성했습니다.</font></center>
