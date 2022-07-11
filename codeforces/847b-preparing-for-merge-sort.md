# 847B - Preparing for Merge Sort

{% embed url="https://codeforces.com/problemset/problem/847/B" %}

| 算法难度 | 思维难度 | 实现难度 | 推荐指数 |
| :--: | :--: | :--: | :--: |
|   3  |   4  |   3  |   3  |



```cpp
#include <bits/stdc++.h>

using namespace std;

const int N = 1e6 + 1;

int n, fa[N];

struct Tree {
#define mid ((l + r) >> 1)
#define lson t << 1, l, mid
#define rson t << 1 | 1, mid + 1, r
	int val[N << 4];
	Tree() {
		memset(val, 0, sizeof(val));
	}
	int cmp(int l, int r) {
		if (!fa[l]) return r;
		if (!fa[r]) return l;
		if (fa[l] < fa[r]) return l;
		return r;
	}
	void Pushup(int t) {
		val[t] = cmp(val[t << 1], val[t << 1 | 1]);
	}
	void Modify(int p, int v, int t = 1, int l = 1, int r = n) {
		if (l == r) {
			val[t] = v;
			return ;
		}
		if (p <= mid) Modify(p, v, lson);
		else Modify(p, v, rson);
		Pushup(t);
	}
	int Query(int x, int y, int t = 1, int l = 1, int r = n) {
		if (x > r || y < l) return 0;
		if (x <= l && r <= y) return val[t];
		return cmp(Query(x, y, lson), Query(x, y, rson));
	}
} tree;

vector<int> res[N];
struct Val {
	int id, val;
} b[N];
int a[N], v[N];
int rtp[N];

int main() {
	scanf("%d", &n);
	for (int i = 1; i <= n; ++i) scanf("%d", &a[i]);

	for (int i = 1; i <= n; ++i) b[i] = (Val) {i, a[i]};
	sort(b + 1, b + n + 1, [=] (Val x, Val y) {
			return x.val < y.val;
			});
	for (int i = 1; i <= n; ++i) b[i].val = i;
	sort(b + 1, b + n + 1, [=] (Val x, Val y) {
			return x.id < y.id;
			});
	for (int i = 1; i <= n; ++i) v[i] = b[i].val;
	for (int i = 1; i <= n; ++i) rtp[v[i]] = i;

	int cnt = 0;
	for (int i = 1; i <= n; ++i) {
		int p = tree.Query(1, v[i] - 1);
		if (!p) fa[v[i]] = ++cnt;
		else {
			fa[v[i]] = fa[p];
			tree.Modify(p, 0);
		}
		tree.Modify(v[i], v[i]);
	}
	
	for (int i = 1; i <= n; ++i) res[fa[i]].push_back(a[rtp[i]]);

	for (int i = 1; i <= cnt; ++i) {
		for (int j = 0; j < (int)res[i].size(); ++j)
			printf("%d%c", res[i][j], j == (int) res[i].size() - 1 ? '\n' : ' ');
	}
	return 0;
}

```
