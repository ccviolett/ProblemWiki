# Problem 2. Robot Instructions

{% embed url="http://www.usaco.org/index.php?cpid=1207&page=viewproblem2" %}

|  指标  | 评分（10 分） |
| :--: | :------: |
| 算法难度 |     4    |
| 思维难度 |     3    |
| 实现难度 |     6    |
| 推荐指数 |     5    |

`meet-in-the-middle`是能够很简单地想到的，但是如何去做却需要思考。

按照一般的做法，一半搜好放进 map 里，另一半搜的时候查，这样的方法理论上可行，但是 map 的大常数让我们望而却步，尝试一下结果是全部 TLE。

考虑使用双端指针，因为当枚举一半中的一个元素时，需要在另一半中找到坐标正好互补的元素。如果我们枚举的元素是单调增大的（按照我们指定的坐标比较规则），则这个另一半中找互补元素的过程也是单调的。

所以可以将两边都搜出来存下来，然后单调指针搞一下就行，省去一个 map 的巨大复杂度极其常数

```cpp
#include <bits/stdc++.h>

using namespace std;
typedef long long var;

const int N = 50;

int read() {
	int s = 0, a = 0, c = getchar();
	while (!isdigit(c)) s |= c == '-', c = getchar();
	while (isdigit(c)) a = a * 10 + c - '0', c = getchar();
	return s ? -a : a;
}

struct Node {
	var x, y;
	int v;
};

Node operator - (const Node a, const Node b) {
	return (Node) {a.x - b.x, a.y - b.y, a.v - b.v};
}

bool operator == (const Node a, const Node b) {
	return a.x == b.x && a.y == b.y;
}

bool operator != (const Node a, const Node b) { return !(a == b); }

bool operator < (const Node a, const Node b) {
	if (a.x != b.x) return a.x < b.x;
	return a.y < b.y;
}

Node goal, node[N];
vector<Node> a, b;
var have[N], res[N];

void DFS(int t, int n, Node p, vector<Node> &v);

int main() {
	int n = read();
	goal = (Node) { read(), read(), 0 };
	for (int i = 1; i <= n; ++i) node[i] = (Node) { read(), read(), 0 };
	DFS(1, n / 2, (Node) {0, 0, 0}, a);
	DFS(n / 2 + 1, n, (Node) {0, 0}, b);
	sort(a.begin(), a.end());
	sort(b.begin(), b.end());

	Node last_need = (Node) {(var) 1e18, (var) 1e18, 0};
	for (int cnta = 0, cntb = b.size() - 1; 
			cnta < a.size() && cntb >= 0; cnta++) {
		Node need = goal - a.at(cnta);
		if (need != last_need) {
			last_need = need;
			memset(have, 0, sizeof(have));
			while (cntb >= 0 && need < b.at(cntb)) cntb--;
			while (cntb >= 0 && need == b.at(cntb)) {
				have[b.at(cntb).v]++;
				cntb--;
			}
		}

		for (int i = 0; i <= n; ++i) 
			res[a.at(cnta).v + i] += have[i];
	}
	for (int i = 1; i <= n; ++i) printf("%lld\n", res[i]);
	return 0;
}

void DFS(int t, int n, Node p, vector<Node> &v) {
	if (t > n) {
		v.push_back(p);
		return ;
	}
	DFS(t + 1, n, p, v);
	p.x += node[t].x, p.y += node[t].y, p.v++;
	DFS(t + 1, n, p, v);
}

```
