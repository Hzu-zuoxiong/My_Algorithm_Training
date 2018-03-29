## Roadblocks

**Description**

Bessie has moved to a small farm and sometimes enjoys returning to visit one of her best friends. She does not want to get to her old home too quickly, because she likes the scenery along the way. She has decided to take the second-shortest rather than the shortest path. She knows there must be some second-shortest path.

The countryside consists ofR\(1 ≤R≤ 100,000\) bidirectional roads, each linking two of the N \(1 ≤N≤ 5000\) intersections, conveniently numbered 1..N. Bessie starts at intersection 1, and her friend \(the destination\) is at intersectionN.

The second-shortest path may share roads with any of the shortest paths, and it may backtrack i.e., use the same road or intersection more than once. The second-shortest path is the shortest path whose length is longer than the shortest path\(s\) \(i.e., if two or more shortest paths exist, the second-shortest path is the one whose length is longer than those but no longer than any other path\).

**Input**

Line 1: Two space-separated integers:N and R

Lines 2: R+1: Each line contains three space-separated integers:A, B, and D that describe a road that connects intersections A and B and has length D\(1 ≤D≤ 5000\)

**Output**

Line 1: The length of the second shortest path between node 1 and node N

**Sample Input**

```
4 4
1 2 100
2 4 200
2 3 250
3 4 100
```

**Sample Output**

```
450
```

---

## 解题思路：

题意：某街区有R条道路，N个路口，道路可以双向通过，问1路口到N路口的次短距离同一条路可以走多次

我们把路口看作顶点，把道路看作边的无向图。Dijkstra算法的思路是依次确定尚未确定的顶点中距离最小的顶点。为此进行少许修改，就可以简单地求出次短路了。

到某个顶点v的次短路要么是到其他某个顶点u的最短路再加上u-&gt;v的边，要么是到u的次短路再加上u-&gt;v的边，因此所需要求的就是到所有顶点的最短路和次短路。因此，对于每个顶点，我们记录的不仅仅是最短距离，还有次短的距离。

---

## AC代码：

```cpp
#include<cstdio>
#include<queue>
#include<algorithm>
#include<cstring>
#include<iostream>
#include<vector>

using namespace std;

const int max_n = 5010;
const int INF = 0x7fffffff;

struct edge{
	int to;
	int cost;
};
typedef pair<int, int> P;
vector<edge> G[max_n];
int dist[max_n];
int dist2[max_n];
int n, r;

void solve() {
	priority_queue<P, vector<P>, greater<P> > que;
	fill(dist, dist + n, INF);
	fill(dist2, dist2 + n, INF);
	dist[0] = 0;
	que.push(P(0, 0));
	
	while(!que.empty()) {
		P p = que.top();
		que.pop();
		int v = p.second;
		int d = p.first;
		if(dist2[v] < d)
			continue;
			
		for(int i = 0; i < G[v].size(); ++i) {
			edge e = G[v][i];
			int d2 = d + e.cost;
			if(dist[e.to] > d2) {
				swap(dist[e.to], d2);
				que.push(P(dist[e.to], e.to));
			}
			
			if(dist2[e.to] > d2 && dist[e.to] < d2) {
				dist2[e.to] = d2;
				que.push(P(dist2[e.to], e.to));
			}
		}
	}
	cout << dist2[n - 1] << endl;
}

int main()
{
	
	while(cin >> n >> r) {
		edge e;
		for(int i = 0; i < r; ++i) {
			int from;
			cin >> from >> e.to >> e.cost;
			from--;
			e.to--;
			G[from].push_back(e);
			swap(e.to, from);
			G[from].push_back(e);
		}
		solve();
	}	
}
```



