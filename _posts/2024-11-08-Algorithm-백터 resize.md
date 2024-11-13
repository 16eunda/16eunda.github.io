---
layout: post
title: 백준 12100번 풀이
subtilte: 이차원 백터 resize (c++)
date: 2024-11-08
categories: algorithm
tags: 알고리즘
comments: true
typora-root-url: ../
---





> c++로 백준 문제를 풀다가 자주 헷갈리는 문법이 있어서 정리!



dfs로 4방향으로 탐색을 하고 depth가 5가되면 멈추도록 구성



```c++
#include <bits/stdc++.h>
using namespace std;

int n, ret = 0;
vector<vector<int>> a;

vector<vector<int>> move(vector<vector<int>> b, int d) {
	int n = b.size();
	//위쪽 이동
	if (d == 0) {
		for (int j = 0; j < n; j++) {
			int l = 0;
			int idx = 0;

			for (int i = 0; i < n; i++) {
				if (b[i][j] == 0) continue;
				if (l == b[i][j]) {
					b[idx - 1][j] *= 2;
					b[i][j] = 0;
					l = 0;
				}
				else {
					l = b[i][j];
					swap(b[idx][j], b[i][j]);
					idx++;
				}
			}

		}
	}

	else if (d == 1) {
		for (int i = 0; i < n; i++) {
			int l = 0;
			int idx = n-1;

			for (int j = n-1; j >= 0; j--) {
				if (b[i][j] == 0) continue;
				if (l == b[i][j]) {
					b[i][idx + 1] *= 2;
					b[i][j] = 0;
					l = 0;
				}
				else {
					l = b[i][j];
					swap(b[i][idx], b[i][j]);
					idx--;
				}
			}

		}
	}

	else if (d == 2) {
		for (int j = 0; j < n; j++) {
			int l = 0;
			int idx = n-1;

			for (int i = n-1; i >= 0; i--) {
				if (b[i][j] == 0) continue;
				if (l == b[i][j]) {
					b[idx + 1][j] *= 2;
					b[i][j] = 0;
					l = 0;
				}
				else {
					l = b[i][j];
					swap(b[idx][j], b[i][j]);
					idx--;
				}
			}

		}
	}

	else if (d == 3) {
		for (int i = 0; i < n; i++) {
			int l = 0;
			int idx = 0;

			for (int j = 0; j < n; j++) {
				if (b[i][j] == 0) continue;
				if (l == b[i][j]) {
					b[i][idx - 1] *= 2;
					b[i][j] = 0;
					l = 0;
				}
				else {
					l = b[i][j];
					swap(b[i][idx], b[i][j]);
					idx++;
				}
			}

		}
	}

	return b;
}

void dfs(vector<vector<int>> board, int depth) {
	if (depth >= 5) {
		int max_ = 0;
		for (int i = 0; i < n; i++) {
			for (int j = 0; j < n; j++) {
				max_ = max(max_, board[i][j]);
			}
		}

		ret = max(ret, max_);
		return;
	}

	for (int dir = 0; dir < 4; dir++) {
		vector<vector<int>> new_a = move(board, dir);
		dfs(new_a, depth + 1);
	}
}

int main() {
	cin >> n;

	int t;
	a.resize(n, vector<int>(n));
	for (int i = 0; i < n; i++) {
		for (int j = 0; j < n; j++) {
			cin >> a[i][j];
		}
	}

	dfs(a, 0);
	cout << ret;
}		
```



### 몰랐던거 (1)

잘 안써봤던 이차원 백터를 사용했다. 보통 이렇게 2차원을 사용해야 하면 이차원 배열을 사용하는 편이다.

왜냐면.. 이차원 배열은 cin >> a[ i ] [ j ] or a[ i ] 이렇게 입력을 한 번에 받을 수 있다. 그리고 보통 vector를 사용하는 이유가 사이즈를 정하기 귀찮을 때 사용하는데 그러면

```c++
int temp; vector<int> v;
cin >> temp;
v.push_back(temp);
```

위 처럼 저렇게 temp라는 변수로 먼저 받고 push로 집어 넣야한다. 처음에는 배열처럼 cin >> v[i] 이렇게 했는데 오류가 났다. 이유는 vector는 크기가 정해져 있지 않는데 인덱스를 사용해서 입력을 받으려고 해서 오류가 나는 것이었다.. 오류가 안 나고 싶으면 vector의 크기를 지정해야 한다.



그래서 이번에 오랜만에 vector를 resize 했는데.. resize(n*n)으로 했다...  그게 아니라 꼭 아래처럼 하도록 기억..

```c++
a.resize(n, vector<int>(n));
```



### 몰랐던거 (2)

그리고 이렇게 resize를 했는데도 내가 push_back()을 사용해서 입력을 받았더니 코드가 잘 작동하지 않았다. 알고 보니 사이즈를 정해놓고 push_back을 하게되니 내가 정한 크기에 뒤로 붙여서 오류가 나는 것이었다.

즉 크기 n으로 고정된 상태에서 push_back(t)를 하게되면 크기가 n+1로 늘어난다...

resize를 했는데도 push_back을 왜 했는지는 모르겠지만 저런 이유로 오류가 날 수 있는 것은 처음 알았다!

