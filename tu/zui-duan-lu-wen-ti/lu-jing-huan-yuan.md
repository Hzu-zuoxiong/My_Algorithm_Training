## 路径还原

虽然许多问题只需输出最短距离就可以了，但是也有的问题需要求解最短路的路径。

在求解最短距离时，满足d\[ j \] = d\[ k \] + cost\[ k \]\[ j \]的顶点k，就是最短路上顶点 j 的前趋节点， 因此通过不断寻找前趋节点就可以恢复出最短路。时间复杂度是O\(\|E\|\)。

此外，如果用prev\[ j \]来记录最短路上顶点 j 的前趋，那么就可以在O\(\|V\|\)的时间内完成最短路的恢复。在d\[ j \] = d\[ k \] + cost\[ k \]\[ j \]更新时，修改prev\[ j \] = k，这样可以求得prev数组。

Bellman-Ford算法和Floyd-Warshall算法都可以用类似的方法进行最短路的还原。

### 代码：

```cpp
int cost[MAX_V][MAX_V];
int d[MAX_V];
int prev[MAX_V];
bool used[MAX_V];
int V;

void dijkstra(int s) {
	fill(d, d + V, INF);
	fill(used, used + V, false);
	fill(prev, prev + V, -1);
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
	
		for(int u = 0; u < V; u++) {
			d[u] = min(d[u], d[v] + cost[v][u]);
			prev[u] = v;
		}
	}
}

//到顶点t的最短路
vector<int> get_path(int t) {
	vector<int> path;
	//不断沿着prev[t]走直到t = s；
	for(; t != -1; t = pre[t])
		path.push_back(t);
	//得到的是按照t到s的顺序，所以要翻转。
	reverse(path.begin(), path.end());
	return path;
}
```



