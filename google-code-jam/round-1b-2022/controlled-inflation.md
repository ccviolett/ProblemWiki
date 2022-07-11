# Controlled Inflation

{% embed url="https://codingcompetitions.withgoogle.com/codejam/round/000000000087711b/0000000000accfdb" %}

|  指标  | 评分（10 分） |
| :--: | :------: |
| 算法难度 |     2    |
| 思维难度 |     3    |
| 实现难度 |     2    |
| 推荐指数 |     3    |



```cpp
#include <bits/stdc++.h>

using namespace std;

const int N = 1e3 + 1;

int read() {
	int a = 0, s = 0, c = getchar();
	while (!isdigit(c)) s |= c == '-', c = getchar();
	while (isdigit(c)) a = a * 10 + c - '0', c = getchar();
	return s ? -a : a;
}

long long dp[N][2];

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
	memset(dp, 0, sizeof(dp));
	int n = read(), p = read();
	int tl = 0, tr = 0, pl = 0, pr = 0;
	for (int i = 1; i <= n; ++i) {
		tl = tr = read();
		for (int j = 2; j <= p; ++j) {
			int v = read();
			tl = min(tl, v), tr = max(tr, v);
		}
		dp[i][0] = min(dp[i - 1][0] + abs(pl - tr), dp[i - 1][1] + abs(pr - tr)) + (tr - tl);
		dp[i][1] = min(dp[i - 1][0] + abs(pl - tl), dp[i - 1][1] + abs(pr - tl)) + (tr - tl);

		pl = tl, pr = tr;
	}

	printf("%lld\n", min(dp[n][0], dp[n][1]));

}

```
