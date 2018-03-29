## Kruskal算法

Kruskal算法按照边的权值的顺序从小到大查看一遍，如果不产生圈（重边等也算在内），就把当前这条边加入到生成树中。

如何判断是否产生圈：

假设要把顶点 u 和顶点 v 的边e加入生成树中。如果加入之前 u 和 v 不在同一个连通分量里，那么加入 e 也不会产生圈。反之，如果 u 和 v 在同一个连通分量里，那么一定会产生圈。可以使用并查集高效地判断是否属于同一个连通分量。

Kruskal算法在边的排序上最费时，算法的复杂度是O\(\|E\|log\|V\|\)。



### 代码：

```cpp
struct edge {
	int u;
	int v;
	int cost;
};

bool comp(const edge& e1, const edge& e2) {
	return e1.cost < e2.cost;
}

edge es[MAX_E];
int V, E;

int Kruskal() {
	//按照edge.cost的顺序从小到大排序 
	sort(es, es + E, comp);
	//并查集的初始化 
	init_union_find(V);
	int res = 0;
	for(int i = 0; i < E; ++i) {
		edge e = es[i];
		if(!same(e.u, e.v)) {
			unite(e.u, e.v);
			res += e.cost;
		}
	}
	return res;
}
```



