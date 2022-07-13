# 732C. Sanatorium

{% embed url="https://codeforces.com/problemset/problem/732/C" %}

|  指标  | 评分（10 分） |
| :--: | :------: |
| 算法难度 |     1    |
| 思维难度 |     2    |
| 实现难度 |     3    |
| 推荐指数 |     1    |



```cpp
#include <bits/stdc++.h>

using namespace std;
typedef long long var;

int main() {
	var a, b, c;
	cin >> a >> b >> c;
	if (a == b && b == c) {
		cout << 0 << endl;
		return 0;
	}
	var v = min(min(a, b), c);
	a -= v, b -= v, c -= v;
	if (!a) a = b, b = c, c = 0;
	if (!b) b = a, a = c, c = 0;
	if (!c) {
		if (a > b) {
			a--;
		} else if (a == b) {
			a--, b--;
		} if (b > a) {
			b--;
		}
		var res = abs(a - b) + max(a, b);
		cout << res << endl;
	}

	return 0;
}

```
