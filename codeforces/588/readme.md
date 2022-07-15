# 588B. Duff in Love

{% embed url="https://codeforces.com/problemset/problem/588/B" %}
'
{% endembed %}

|  指标  | 评分（10 分） |
| :--: | :------: |
| 算法难度 |     1    |
| 思维难度 |     2    |
| 实现难度 |     2    |
| 推荐指数 |     2    |



```cpp
#include <bits/stdc++.h>

using namespace std;
typedef long long var;

int main() {
	var n;
	cin >> n;
	for (var i = 2; i * i <= n; ++i) {
		if (n % i) continue;
		while (!(n % (i * i))) n /= i;
	}
	cout << n << endl;
	return 0;
}

```
