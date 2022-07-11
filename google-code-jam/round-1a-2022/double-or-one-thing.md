# Double or One Thing



|  指标  | 评分（10 分） |
| :--: | :------: |
| 算法难度 |     0    |
| 思维难度 |     2    |
| 实现难度 |     1    |
| 推荐指数 |     2    |



```cpp
#include <bits/stdc++.h>

using namespace std;

const int maxlen = 101;

char s[maxlen];

int main() {
	int T;
	scanf("%d", &T);
	for (int t = 1; t <= T; ++t) {
		printf("Case #%d: ", t);
		scanf("%s", s);
		int n = strlen(s);
		for (int i = 0; i < n; ++i) {
			int r = i + 1;
			while (r < n && s[r] == s[i]) r++;
			if (r < n && s[r] > s[i]) {
				for (int j = i; j < r; ++j) 
					putchar(s[j]), putchar(s[j]);
			} else {
				for (int j = i; j < r; ++j) 
					putchar(s[j]);
			}
			i = r - 1;
		}
		puts("");
	}
	return 0;
}

```
