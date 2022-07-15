# 687A. NP-Hard Problem

{% embed url="https://codeforces.com/problemset/problem/687/A" %}

|  指标  | 评分（10 分） |
| :--: | :------: |
| 算法难度 |     2    |
| 思维难度 |     2    |
| 实现难度 |     2    |
| 推荐指数 |     2    |

因为需要分为两个点覆盖集，所以一条边的两个端点一定分别在两个不同的集合中。

转换为一个黑白染色问题。

```cpp
#include <bits/stdc++.h>

using namespace std;
typedef long long var;

const int N = 2e5 + 1;

int read() {
	int s = 0, a = 0, c = getchar();
	while (!isdigit(c)) s |= c == '-', c = getchar();
	while (isdigit(c)) a = a * 10 + c - '0', c = getchar();
	return s ? -a : a;
}

int n, m;
int top, fi[N], ne[N], to[N];
bool mark[N];
int color[N];
bool conflic;

void add(int u, int v) {
	ne[++top] = fi[u], fi[u] = top, to[top] = v;
	ne[++top] = fi[v], fi[v] = top, to[top] = u;
}

void DFS(int t, int c) {
	if (color[t] && color[t] != c) {
		conflic = true;
		return ;
	}
	color[t] = c;
	if (mark[t]) return ;
	mark[t] = true;
	for (int i = fi[t]; i; i = ne[i])
		DFS(to[i], -c);
}

int main() {
	n = read(), m = read();
	for (int i = 1; i <= m; ++i) add(read(), read());
	for (int i = 1; i <= n; ++i) {
		if (!mark[i]) DFS(i, 1);
	}

	/* 
	for (int i = 1; i <= n; ++i) cout << color[i] << ' ';
	cout << endl;
	*/

	if (conflic) {
		puts("-1");
		return 0;
	}
	int n1 = 0;
	for (int i = 1; i <= n; ++i) n1 += color[i] == 1;
	printf("%d\n", n1);
	for (int i = 1; i <= n; ++i) {
		if (color[i] == 1) printf("%d%c", i, --n1 ? ' ' : '\n');
	}

	for (int i = 1; i <= n; ++i) n1 += color[i] == -1;
	printf("%d\n", n1);
	for (int i = 1; i <= n; ++i) {
		if (color[i] == -1) printf("%d%c", i, --n1 ? ' ' : '\n');
	}
	return 0;
}


```
