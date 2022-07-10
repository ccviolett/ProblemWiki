# 847A - Union of oubly Linked Lists

{% embed url="https://codeforces.com/problemset/problem/847/A" %}

{% code title="main.cpp" %}
```cpp
#include <bits/stdc++.h>

using namespace std;

const int N = 1000;

int n;
int l[N], r[N];

int fa[N];
int find(int t) {
	if (fa[t] != t) fa[t] = find(fa[t]);
	return fa[t];
}

bool merge(int x, int y) {
	x = find(x), y = find(y);
	if (x == y) return false;
	fa[x] = y;
	return true;
}

int main() {
	cin >> n;
	for (int i = 1; i <= n; ++i) fa[i] = i;
	for (int i = 1; i <= n; ++i) {
		cin >> l[i] >> r[i];
		if (l[i]) merge(i, l[i]);
		if (r[i]) merge(i, r[i]);
	}
	for (int t = 1; t <= n; ++t) {
		for (int i = 1; i <= n; ++i) {
			if (l[i]) continue;
			for (int j = 1; j <= n; ++j) {
				if (r[j]) continue;
				if (!merge(i, j)) continue;
				l[i] = j, r[j] = i;
				break;
			}
		}
	}
	for (int i = 1; i <= n; ++i) {
		cout << l[i] << " " << r[i] << endl;
	}
	return 0;
}
```
{% endcode %}

