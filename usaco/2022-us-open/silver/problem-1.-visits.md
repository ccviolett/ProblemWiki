# Problem 1. Visits

{% embed url="http://www.usaco.org/index.php?cpid=1230&page=viewproblem2" %}

|  指标  | 评分（10 分） |
| :--: | :------: |
| 算法难度 |     1    |
| 思维难度 |     2    |
| 实现难度 |     2    |
| 推荐指数 |     2    |



```cpp
#include <bits/stdc++.h>

using namespace std;

const int N = 1e5 + 100;

int from[N], to[N], mark[N];
int v[N];

long long dfs(int t, int i) {
	if (mark[t]) {
		if (mark[t] == i) {
			int x = from[t], minv = v[t];
			while (x != t) {
				minv = min(minv, v[x]);
				x = from[x];
			}
			return -minv;
		}
		return 0;
	}

	mark[t] = i;
	from[to[t]] = t;
	return dfs(to[t], i) + v[t];
}

int main() {
	int n;
	scanf("%d", &n);
	for (int i = 1; i <= n; ++i) scanf("%d %d", &to[i], &v[i]);
	long long res = 0;
	for (int i = 1; i <= n; ++i) {
		if (!mark[i]) res += dfs(i, i);
	}
	printf("%lld\n", res);
	return 0;
}

```
