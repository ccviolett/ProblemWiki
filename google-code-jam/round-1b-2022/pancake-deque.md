# Pancake Deque

{% embed url="https://codingcompetitions.withgoogle.com/codejam/round/000000000087711b/0000000000acd59d" %}

|  指标  | 评分（10 分） |
| :--: | :------: |
| 算法难度 |     0    |
| 思维难度 |     1    |
| 实现难度 |     1    |
| 推荐指数 |     1    |



```cpp
#include <bits/stdc++.h>

using namespace std;

int read() {
	int a = 0, s = 0, c = getchar();
	while (!isdigit(c)) s |= c == '-', c = getchar();
	while (isdigit(c)) a = a * 10 + c - '0', c = getchar();
	return s ? -a : a;
}

const int N = 1e5 + 100;

int d[N];

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
	int n = read();
	for (int i = 1; i <= n; ++i) d[i] = read();
	int l = 1, r = n, mxv = 0, res = 0;
	while (l <= r) {
		int tv = 0;
		if (d[l] <= d[r]) tv = d[l++];
		else tv = d[r--];
		res += mxv <= tv;
		mxv = max(mxv, tv);
	}
	printf("%d\n", res);
}
```
