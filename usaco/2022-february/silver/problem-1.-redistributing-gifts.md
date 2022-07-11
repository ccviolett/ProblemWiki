# Problem 1. Redistributing Gifts

{% embed url="http://www.usaco.org/index.php?cpid=1206&page=viewproblem2" %}

|  指标  | 评分（10 分） |
| :--: | :------: |
| 算法难度 |     1    |
| 思维难度 |     2    |
| 实现难度 |     1    |
| 推荐指数 |     2    |



```cpp
#include <bits/stdc++.h>

using namespace std;

const int N = 501;

int n;
int favor[N][N];
bool edge[N][N];
bool arrive[N][N];

void DFS(int t, int v) {
	arrive[v][t] = true;
	for (int i = 1; i <= n; ++i) {
		if (edge[t][i] && !arrive[v][i]) 
			DFS(i, v);
	}
}

int main() {
	scanf("%d", &n);
	for (int i = 1; i <= n; ++i) {
		for (int j = 1; j <= n; ++j)
			scanf("%d", &favor[i][j]);
	}
	
	for (int i = 1; i <= n; ++i) {
		for (int j = 1; j <= n; ++j) {
			edge[i][favor[i][j]] = true;
			if (favor[i][j] == i) break;
		}
	}
	for (int i = 1; i <= n; ++i) DFS(i, i);
	for (int i = 1; i <= n; ++i) {
		for (int j = 1; j <= n; ++j) {
			int t = favor[i][j];
			if (arrive[i][t] && arrive[t][i]) {
				printf("%d\n", t);
				break;
			}
		}
	}
	return 0;
}

```
