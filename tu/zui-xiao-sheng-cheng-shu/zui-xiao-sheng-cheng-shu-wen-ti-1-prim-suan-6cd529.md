## Prim算法

Prim算法和Dijkstra算法十分相似，都是从某个顶点出发，不断添加边的算法。

### 代码：

```cpp
int cost[MAX_V][MAX_V];
int mincost[MAX_V];
bool used[MAX_V];
int V;

int prim(int s) {
	
	for(int i = 0; i < V; i++) {
		mincost[i] = INF;
		used[i] = false;
	}
	mincost[0] = 0;
	int res = 0;
	
	while(true) {
		int v = -1;
		
		for(int u = 0; u < V; ++u) {
			if(!used[u] && (v == -1 || mincost[u] < mincost[v]))
				v = u;
		}
		
		if(v == -1)
			break;
		used[v] = true;
		res += mincost[v];
		
		for(int u = 0; u < V; u++)
			mincost[u] = min(mincost[u], mincost[v] + cost[v][u]);
	}
	return res;
}
```



