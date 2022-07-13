# 730J. Bottles

{% embed url="https://codeforces.com/problemset/problem/730/J" %}

|  指标  | 评分（10 分） |
| :--: | :------: |
| 算法难度 |     2    |
| 思维难度 |     4    |
| 实现难度 |     3    |
| 推荐指数 |     5    |



```cpp
#include <bits/stdc++.h>

using namespace std;
typedef long long var;

const int N = 101;

int read() {
	int s = 0, a = 0, c = getchar();
	while (!isdigit(c)) s |= c == '-', c = getchar();
	while (isdigit(c)) a = a * 10 + c - '0', c = getchar();
	return s ? -a : a;
}

int n;
int a[N], b[N];
int dp[N][N * N];
bool able[N][N * N];

int main() {
	int n = read();
	for (int i = 1; i <= n; ++i) a[i] = read();
	for (int i = 1; i <= n; ++i) b[i] = read();

	int suma = 0, sumb = 0;
	for (int i = 1; i <= n; ++i) 
		suma += a[i], sumb += b[i];

	able[0][0] = true;
	for (int i = 1; i <= n; ++i) {
		for (int t = n; t >= 1; --t) {
			for (int j = b[i]; j <= sumb; ++j) {
				if (!able[t - 1][j - b[i]]) continue;
				dp[t][j] = max(dp[t][j], dp[t - 1][j - b[i]] + a[i]);
				able[t][j] = true;
			}
		}
	}

	int k = 0, t = 0x3f3f3f3f;
	for (int i = 1; i <= n; ++i) {
		for (int j = suma; j <= sumb; ++j) {
			if (able[i][j]) {
				k = i;
				t = min(t, suma - dp[k][j]);
			}
		}
		if (k) break;
	}
	printf("%d %d\n", k, t);
	return 0;
}

```
