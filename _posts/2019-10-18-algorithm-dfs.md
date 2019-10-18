---
layout: post
title: "[탐색] 깊이 우선 탐색 : DFS"
categories:
  - Algorithm
tags:
  - dfs
  - algorithm
  - c++
last_modified_at: 2019-10-18T
---
<br>
### BFS (Breadth First Search)
* 탐색을 할 때 깊이를 우선으로 하여 탐색하는 탐색 알고리즘이다.
* [BFS](https://jaden2208.github.io/algorithm/2019/10/17/algorithm-bfs.html)와 마찬가지로 '맹목적인 탐색'을 하고자 할 때 사용할 수 있다.

<br>

---
#### 과정 설명
0. 먼저, 첫번째 값을 꺼내서 스택에 넣어준다.
1. 스택의 최상단 노드(가장 마지막에 들어온 노드)를 확인한다.
2. 최상단 노드에게 방문하지 않은 인접 노드를 모두 찾아 차례로 스택에 넣어준다.
3. 1, 2의 과정을 반복한다.

<br>

<center>
<img src="/images/dfs.png" width="50%" height="50%"></center>

<br>

---
#### c++ 코드

```c++
#include <iostream>
#include <vector>

using namespace std;

int number = 7;
bool visited[7]; // 탐색 여부에 따라서 탐색했다면 true로 저장하기 위한 배열.
vector<int> a[8];

void dfs(int x){
	if(visited[x]) return;
	visited[x] = true;
	cout << x << ' ';
	for(int i=0; i<a[x].size(); i++){
		int y = a[x][i];
		dfs(y);
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

	dfs(1);

	return 0;
}
```

<br>

---
<center><font size="2em"> 나동빈 님의 알고리즘 강의를 참고해 작성했습니다.</font></center>
