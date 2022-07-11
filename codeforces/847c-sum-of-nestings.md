# 847C - Sum of Nestings

{% embed url="https://codeforces.com/problemset/problem/847/C" %}

| 算法难度 | 思维难度 | 实现难度 | 推荐指数 |
| :--: | :--: | :--: | :--: |
|   0  |   3  |   2  |   4  |



```cpp
#include <bits/stdc++.h>

using namespace std;

long long n, k;

int main() {
	cin >> n >> k;
	if (n * (n - 1) < k * 2) {
		cout << "Impossible" << endl;
		return 0;
	}
	for (int t = 0; t < n; t++) {
		if (k - t == 0) {
			for (int i = 0; i <= t; ++i) cout << "(";
			for (int i = 0; i <= t; ++i) cout << ")";
			for (int i = t + 1; i < n; ++i) cout << "()";
			cout << endl;
			return 0;
		}
		if (k - t < 0) {
			long long x = t - k;
			for (int i = 0; i < t; ++i) cout << "(";
			for (int i = 0; i < t; ++i) {
				if (i == x) cout << "()";
				cout << ")";
			}
			for (int i = t + 1; i < n; ++i) cout << "()";
			cout << endl;
			return 0;
		}
		k -= t;
	}
	cout << "Impossible" << endl;
	return 0;
}

```