# 730H. Delete Them

{% embed url="https://codeforces.com/problemset/problem/730/H" %}

|  指标  | 评分（10 分） |
| :--: | :------: |
| 算法难度 |     1    |
| 思维难度 |     2    |
| 实现难度 |     1    |
| 推荐指数 |     2    |



```cpp
#include <bits/stdc++.h>

using namespace std;
typedef long long var;

const int N = 1000;

int read() {
	int t;
	scanf("%d", &t);
	return t;
}

char file[N][N];
int need[N];
bool mark[N];
char patten[N];

int main() {
	int n = read(), m = read();
	for (int i = 1; i <= n; ++i) scanf("%s", file[i]);
	for (int i = 1; i <= m; ++i) need[i] = read();
	int len = strlen(file[need[1]]);
	for (int i = 0; i < len; ++i) patten[i] = file[need[1]][i];
	for (int i = 1; i <= m; ++i) {
		mark[need[i]] = true;
		if (strlen(file[need[i]]) != len) {
			puts("No");
			return 0;
		}
		for (int j = 0; j < len; ++j) {
			if (patten[j] == '?' || patten[j] == file[need[i]][j]) continue;
			patten[j] = '?';
		}
	}
	for (int i = 1; i <= n; ++i) {
		if (mark[i]) continue;
		if (strlen(file[i]) != len) continue;
		bool ok = true;
		for (int j = 0; j < len; ++j) {
			if (patten[j] == '?' || patten[j] == file[i][j]) continue;
			ok = false;
		}
		if (ok) {
			puts("No");
			return 0;
		}
	}
	puts("Yes");
	puts(patten);
	return 0;
}

```
