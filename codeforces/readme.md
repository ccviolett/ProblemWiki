# 743C. Vladik and fractions

{% embed url="https://codeforces.com/problemset/problem/743/C" %}

|  指标  | 评分（10 分） |
| :--: | :------: |
| 算法难度 |     1    |
| 思维难度 |     3    |
| 实现难度 |     1    |
| 推荐指数 |     3    |



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

var n;

int main() {
	n = read();
	if (n == 1) cout << "-1" << endl;
	else cout << n << " " << n + 1 << " " << n * (n + 1) << endl;
	return 0;
}

```
