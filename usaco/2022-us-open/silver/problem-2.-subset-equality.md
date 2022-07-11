# Problem 2. Subset Equality

{% embed url="http://www.usaco.org/index.php?cpid=1231&page=viewproblem2" %}

|  指标  | 评分（10 分） |
| :--: | :------: |
| 算法难度 |     1    |
| 思维难度 |     7    |
| 实现难度 |     2    |
| 推荐指数 |     7    |



```cpp
#include <bits/stdc++.h>

using namespace std;

const int N = 1e5 + 100;
const int V = 26;

char s[N], t[N];
int snum[V], tnum[V], dnum[V][V];
char c[N];

int main() {
	scanf("%s%s", s, t);
	int n = strlen(s), m = strlen(t);
	for (int i = 0; i < n; ++i) s[i] -= 'a', snum[s[i]]++;
	for (int i = 0; i < m; ++i) t[i] -= 'a', tnum[t[i]]++;
	// for (int i = 0; i < V; ++i) printf("%c %d %d\n", i + 'a', snum[i], tnum[i]);
	for (int i = 0; i < V; ++i) dnum[i][i] = snum[i] && (snum[i] == tnum[i]);

	for (int i = 0; i < V; ++i) {
		if (!snum[i] || !tnum[i]) continue;
		for (int j = i + 1; j < V; ++j) {
			if (!snum[j] && !tnum[j]) continue;
			int x = 0, y = 0;
			bool ok = true;
			while (x < n && y < m) {
				while (x < n && s[x] != i && s[x] != j)
					x++;
				while (y < m && t[y] != i && t[y] != j)
					y++;
				if (s[x] != t[y]) {
					ok = false;
					break;
				}
				x++, y++;
			}
			if (ok) dnum[i][j] = dnum[j][i] = true;
		}
	}
	/*
	for (int i = 0; i < V; ++i) {
		for (int j = i; j < V; ++j) {
			if (dnum[i][j]) printf("%c-%c\n", i + 'a', j + 'a');
		}
	}
	*/
	int Q;
	scanf("%d", &Q);
	for (int i = 1; i <= Q; ++i) {
		scanf("%s", c);
		int len = strlen(c);
		bool ok = true;
		for (int x = 0; x < len; ++x) {
			for (int y = x; y < len; ++y) {
				// printf("%c %c %d\n", c[x], c[y], dnum[x][y]);
				if (!dnum[c[x] - 'a'][c[y] - 'a']) {
					ok = false;
					break;
				}
			}
			if (!ok) break;
		}
		putchar(ok ? 'Y' : 'N');
	}
	puts("");
	return 0;
}

```
