# Weightlifting

{% embed url="https://codingcompetitions.withgoogle.com/codejam/round/0000000000877ba5/0000000000aa9280" %}

|  指标  | 评分（10 分） |
| :--: | :------: |
| 算法难度 |     3    |
| 思维难度 |     4    |
| 实现难度 |     3    |
| 推荐指数 |     5    |



```cpp
#include <bits/stdc++.h>

using namespace std;

const int N = 101;

int x[N][N];
int same[N][N], dp[N][N];

int read() {
	int a = 0, s = 0, c = getchar();
	while (!isdigit(c)) s |= c == '-', c = getchar();
	while (isdigit(c)) a = a * 10 + c - '0', c = getchar();
	return s ? -a : a;
}

void solve();

int main() {
	int T = read();
	for (int i = 1; i <= T; ++i) {
		printf("Case #%d: ", i);
		solve();
	}
	return 0;
}

void solve() {
	int n = read(), m = read();
	for (int i = 1; i <= n; ++i) {
		for (int j = 1; j <= m; ++j) x[i][j] = read();
	}

	memset(same, 0, sizeof(same));
	for (int i = 1; i <= m; ++i) {
		for (int l = 1; l <= n; ++l) {
			int have = x[l][i];
			for (int r = l; r <= n; ++r) {
				have = min(have, x[r][i]);
				same[l][r] += have;
			}
		}
	}
	memset(dp, 0x3f, sizeof(dp));
	for (int i = 1; i <= n; ++i) dp[i][i] = 0;
	for (int i = 2; i <= n; ++i) {
		for (int l = 1; l <= n; ++l) {
			int r = l + i - 1;
			if (r > n) break;
			for (int k = l; k < r; ++k) {
				dp[l][r] = min(dp[l][r], dp[l][k] + dp[k + 1][r] + 2 * (same[l][k] + same[k + 1][r] - 2 * same[l][r]));
			}
		}
	}
	printf("%d\n", dp[1][n] + 2 * same[1][n]);
}

```
