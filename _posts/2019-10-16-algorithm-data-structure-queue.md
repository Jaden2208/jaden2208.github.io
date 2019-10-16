---
layout: post
title: "[자료구조] 큐 (Queue)"
categories:
  - Algorithm
tags:
  - queue
  - data structure
  - algorithm
  - c++
last_modified_at: 2019-10-16T
---
<br>
### 큐(Queue) : 선입선출
먼저 들어온 값이 먼저 나간다.

(반대 : [스택(Stack)](https://jaden2208.github.io/algorithm/2019/10/16/algorithm-data-structure-stack.html) 는 후입선출)

<br>

---

#### c++ 코드

```c++
#include <iostream>
#include <queue>

using namespace std;

int main(){
	queue<int> q;

	q.push(7);	// 7
	q.push(5);	// 7, 5
	q.push(4);	// 7, 5, 4
	q.pop();	// out<--(7)  5, 4
	q.push(6);	// 5, 4, 6
	q.pop();	// out<--(5)  4, 6

	while(!q.empty()){
		cout << q.front() << ' ';
		q.pop();
	}

	return 0;
}
```

<br>

---
<center><font size="2em"> 나동빈 님의 알고리즘 강의를 참고해 작성했습니다.</font></center>
