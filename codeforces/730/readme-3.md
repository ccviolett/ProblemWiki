# 730I. Olympiad in Programming and Sports



|  指标  | 评分（10 分） |
| :--: | :------: |
| 算法难度 |     5    |
| 思维难度 |     1    |
| 实现难度 |     5    |
| 推荐指数 |     4    |



```cpp
#include <bits/stdc++.h>

using namespace std;
typedef long long var;

const int N = 1e5 + 1;
const int M = 1e5 + 1;

int read() {
	int s = 0, a = 0, c = getchar();
	while (!isdigit(c)) s |= c == '-', c = getchar();
	while (isdigit(c)) a = a * 10 + c - '0', c = getchar();
	return s ? -a : a;
}

class Graph {
	public:
		int top, fi[N], ne[M << 1], to[M << 1], fl[M << 1], co[M << 1];

		int S, T;
		var dist[N];
		int head, tail, q[N];
		bool inq[N];
		int fromNode[N], fromLine[N];

		Graph() {
			top = 1;
		}

		void Add(int u, int v, int f, int w) {
			ne[++top] = fi[u], fi[u] = top, to[top] = v, fl[top] = f, co[top] = w;
			ne[++top] = fi[v], fi[v] = top, to[top] = u, fl[top] = 0, co[top] = -w;
		}

		bool SPFA() {
			memset(dist, 0x3f, sizeof(dist));
			dist[S] = 0;
			q[head = tail = 1] = S;
			while (head <= tail) {
				int t = q[head++];
				inq[t] = false;
				for (int i = fi[t]; i; i = ne[i]) {
					if (!fl[i] || dist[to[i]] <= dist[t] + co[i]) continue;
					dist[to[i]] = dist[t] + co[i];

					fromNode[to[i]] = t, fromLine[to[i]] = i;

					if (inq[to[i]]) continue;
					q[++tail] = to[i];
					inq[to[i]] = true;
				}
			}
			return dist[T] != 0x3f3f3f3f3f3f3f3f;
		}

		void MCMF(var &sum_flow, var &cost) {
			while (SPFA()) {
				int flow = 0x3f3f3f3f;
				for (int i = T; i != S; i = fromNode[i])
					flow = min(flow, fl[fromLine[i]]);
				for (int i = T; i != S; i = fromNode[i]) 
					fl[fromLine[i]] -= flow, fl[fromLine[i] ^ 1] += flow;
				sum_flow += flow;
				cost += dist[T] * flow;
			}
		}
} g;

int n, a[N], b[N];
int t1[N], t2[N];

int main() {
	int n = read(), p = read(), s = read();
	for (int i = 1; i <= n; ++i) a[i] = read();
	for (int i = 1; i <= n; ++i) b[i] = read();

	int c1 = n * 3 + 2, c2 = n * 3 + 3;
	g.S = n * 3 + 1, g.T = n * 3 + 4;
	g.Add(c1, g.T, p, 0);
	g.Add(c2, g.T, s, 0);

	for (int i = 1; i <= n; ++i) {
		g.Add(i, n + i * 2 - 1, 1, -a[i]);
		t1[i] = g.top;
		g.Add(i, n + i * 2, 1, -b[i]);
		t2[i] = g.top;

		g.Add(g.S, i, 1, 0);
		g.Add(n + i * 2 - 1, c1, 1, 0);
		g.Add(n + i * 2, c2, 1, 0);
	}

	var flow = 0, cost = 0;
	g.MCMF(flow, cost);
	printf("%lld\n", -cost);
	for (int i = 1; i <= n; ++i) {
		if (g.fl[t1[i]]) printf("%d ", i);
	}
	puts("");
	for (int i = 1; i <= n; ++i) {
		if (g.fl[t2[i]]) printf("%d ", i);
	}
	puts("");
	return 0;
}

```
