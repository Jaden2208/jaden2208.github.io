---
layout: post
title: "[탐색] 너비 우선 탐색 : BFS"
categories:
  - Algorithm
tags:
  - bfs
  - algorithm
  - c++
last_modified_at: 2019-10-17T
---
<br>
### BFS (Breadth First Search)
* 탐색을 할 때 너비를 우선으로 하여 탐색하는 탐색 알고리즘이다.
* 즉, 어떤 시작점이 있을 때 그 시작점과 가까운 것 위주로 먼저 탐색하겠다는 것이다.
* 특히, '맹목적인 탐색'을 하고자 할 때 사용할 수 있다.
* BFS는 '최단 경로'를 찾아준다는 점에서 최단 길이를 보장해야 할 때 많이 사용한다.

<br>

---
#### 과정 설명
1. 큐에서 하나의 노드를 꺼낸다.
2. 해당 노드에 연결된 노드 중 방문하지 않은 노드를 모두 찾아 각각 큐에 넣어준다.
3. 1, 2의 과정을 반복한다.

<br>

---
#### c++ 코드

```c++
#include <iostream>
#include <queue>
#include <vector>

using namespace std;

int number = 7;
int c[7]; // 탐색 여부에 따라서 탐색했다면 true로 저장하기 위한 배열.
vector<int> a[8];

void bfs(int start){
	queue<int> q;

	// 0. 먼저, 첫번째 값을 꺼내서 큐에 넣어준다.
	q.push(start);
	c[start] = true;

	while(!q.empty()){
		// 1. 큐에서 하나의 노드를 꺼낸다.
		int x = q.front();
		q.pop();
		cout << x << ' ';

		//2. 해당 노드에 연결된 노드 중 방문하지 않은 노드를 모두 찾아 각각 큐에 넣어준다.
		for(int i=0; i<a[x].size(); i++){
			int y = a[x][i];
			if(!c[y]){
				q.push(y);
				c[y] = true;
			}
		}
	}
}

int main(){
	// 각 노드들을 연결.
	a[1].push_back(2);
	a[2].push_back(1);

	a[1].push_back(3);
	a[3].push_back(1);

	a[2].push_back(3);
	a[3].push_back(2);

	a[2].push_back(4);
	a[4].push_back(2);

	a[2].push_back(5);
	a[5].push_back(2);

	a[3].push_back(6);
	a[6].push_back(3);

	a[3].push_back(7);
	a[7].push_back(3);

	a[4].push_back(5);
	a[5].push_back(4);

	a[6].push_back(7);
	a[7].push_back(6);

	bfs(1);

	return 0;
}

```

<br>

---
<center><font size="2em"> 나동빈 님의 알고리즘 강의를 참고해 작성했습니다.</font></center>
