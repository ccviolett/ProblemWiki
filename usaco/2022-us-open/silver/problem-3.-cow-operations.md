# Problem 3. COW Operations

{% embed url="http://www.usaco.org/index.php?cpid=1232&page=viewproblem2" %}

|  指标  | 评分（10 分） |
| :--: | :------: |
| 算法难度 |     1    |
| 思维难度 |     5    |
| 实现难度 |     1    |
| 推荐指数 |     4    |



```cpp
#include <bits/stdc++.h>

using namespace std;

const int N = 2e5 + 100;

char s[N];
int num[26][N];

int main() {
	scanf("%s", s + 1);
	int n = strlen(s + 1);
	for (int i = 1; i <= n; ++i) {
		for (int j = 0; j < 26; ++j) 
			num[j][i] = num[j][i - 1];
		num[s[i] - 'A'][i]++;
	}
	int Q;
	scanf("%d", &Q);
	while (Q--) {
		int l, r;
		scanf("%d%d", &l, &r);
		int C = num['C' - 'A'][r] - num['C' - 'A'][l - 1],
			O = num['O' - 'A'][r] - num['O' - 'A'][l - 1],
			W = num['W' - 'A'][r] - num['W' - 'A'][l - 1];
		// printf("%d %d %d\n", C, O, W);
		if ((C + O) % 2 == 1 && (O + W) % 2 != 1)
			putchar('Y');
		else 
			putchar('N');
		putchar(((C + O) & 1) && !((O + W) & 1) ? 'Y' : 'N');
	}
	puts("");
	return 0;
}

```
