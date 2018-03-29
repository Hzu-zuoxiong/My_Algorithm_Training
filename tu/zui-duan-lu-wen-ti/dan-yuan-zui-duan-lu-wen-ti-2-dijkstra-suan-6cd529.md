## 单源最短路问题2\(Dijkstra算法\)

在Bellman-Ford算法中，即使d\[ i \]没有变化，每一个循环也要从检查一遍从 i 出发的所有边。这显然是很浪费时间的，因此可以对算法做如下修改：

1. 找到最短距离已经确定的顶点，从它出发更新相邻顶点的最短距离
2. 此后不再关心1中的“最短距离已经确定的顶点”。

### 代码：

\(此段代码还尚未完全理解。\)

```cpp
int cost[MAX_V][MAX_V];
int d[MAX_V];
bool used[MAX_V];
int V;

void dijkstra(int s) {
	fill(d, d + V, INF);
	fill(used, used + V, false);
	d[s] = 0;
	
	while(true) {
		int v = -1;
		
		for(int u = 0; u < V; ++u) {
			if(!used[u] && (v == -1 || d[u] < d[v]))
				v = u;
		}
		
		if(v == -1)
			break;
		used[v] = true;
		
		for(int u = 0; u < V; u++)
			d[u] = min(d[u], d[v] + cost[v][u]);
	}
} 
```



使用STL的priority\_queue的实现。在每次更新时往堆里插入当前最短距离和顶点的值对。插入的次数是O\(\|E\|\)次，因此元素也是O\(\|E\|\)个。当取出的最小值不是最短距离的话，就丢弃这个值。这样整个算法也可以在同样的复杂度内完成。

### 代码：

```cpp
struct edge{
	int to;
	int cost;
}; 

typedef pair<int, int> P;
int V;
int d[MAX_V];
vector<edge> G[MAX_V];

void dijkstra(int s) {
	//通过指定greater<P>参数，堆按照first从小到大的顺序取出值
	priority_queue<P, vector<P>, greater<P> > que;
	fill(d, d + V, INF);
	d[s] = 0;
	que.push(P(0, s));
	
	while(!que.empty()) {
		P p = que.top();
		que.pop();
		int v = p.second;
		if(d[v] < p.first)
			continue;
		for(int i = 0; i < G[v].size(); i++) {
			edge e = G[v][i];
			if(d[e.to] > d[v] + e.cost) {
				d[e.to] = d[v] + e.cost;
				que.push(P(d[e.to], e.to));
			}
		}
	}
} 
```

但是，在图中存在负边的情况下，Dijkstra算法就无法正确求解问题，还是需要使用Bellman-Ford算法。

