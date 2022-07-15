# 730A. Toda 2

{% embed url="https://codeforces.com/problemset/problem/730/A" %}

|  指标  | 评分（10 分） |
| :--: | :------: |
| 算法难度 |     3    |
| 思维难度 |     5    |
| 实现难度 |     4    |
| 推荐指数 |     6    |



```cpp
#include <bits/stdc++.h>

using namespace std;
typedef long long var;

const int M = 10001;
const int N = 101;

int read() {
	int s = 0, a = 0, c = getchar();
	while (!isdigit(c)) s |= c == '-', c = getchar();
	while (isdigit(c)) a = a * 10 + c - '0', c = getchar();
	return s ? -a : a;
}

struct R {
	int p, v;
};

bool operator < (const R a, const R b) {
	return a.v < b.v;
}

int n, r[N];
priority_queue<R> q;
int cnt, use[N];
bool choose[M][N];

int main() {
	int n = read();
	for (int i = 1; i <= n; ++i) r[i] = read();

	int minv = r[1];
	for (int i = 1; i <= n; ++i) {
		q.push({i, r[i]});
		minv = min(minv, r[i]);
		use[i] = 1;
	}

	while (true) {
		R a = q.top();
		q.pop();
		R b = q.top();
		q.pop();
		if (b.v == minv) {
			for (int x = a.v - b.v; x && use[a.p] <= cnt; ++use[a.p]) {
				if (!choose[use[a.p]][a.p]) {
					choose[use[a.p]][a.p] = true;
					a.v--, x--;
				}
			}
			if (a.v == b.v) {
				printf("%d\n", minv);
				break;
			}
		}

		cnt++;
		choose[cnt][a.p] = choose[cnt][b.p] = 1;
		if (a.v) a.v--;
		if (b.v) b.v--;
		if (b.v < minv) minv = b.v;
		q.push(a), q.push(b);
	}

	printf("%d\n", cnt);
	for (int i = 1; i <= cnt; ++i) {
		for (int j = 1; j <= n; ++j) putchar(choose[i][j] ? '1' : '0');
		puts("");
	}
	return 0;
}

```
