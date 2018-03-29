## 单源最短路问题1（Bellman-Ford算法）

单源最短路问题是固定一个起点，求它到其他所有点的最短路问题。

记从起点 s 出发到顶点 i 的最短距离为d\[ i \]。则下述等式成立。

```
d[ i ] = min{ d [ j ] + (从 j 到 i 的边的权值) | e = ( j ,i ) ∈ E }
```

如果给定的图是一个DAG（有向无环图），就可以按拓扑序给顶点编号，并利用这条递推关系式计算出d。在这种情况下，记当前到顶点 i 的最短路长度为d\[ i \]，并设初值d\[ s \] = 0, d\[ i \] = INF\(足够大的常数\)，再不断使用这条递推关系式更新d的值。只要图中不存在负圈，这样的更新操作就是有限的。结束之后的d就是所求的最短距离。

### 代码：

```cpp
struct edge{
    int from;
    int to;
    int cost;
};

edge es[MAX_E];
int d[MAX_V];
int V, E;

void shortest_path(int s) {
    for(int i = 02; i < V; i++) {
        d[i] = INF;
    }
    d[s] = 0;
    while(true) {
        bool update = false;
        for(int i = 0; i < E; i++) {
            edge e = es[i];
            if(d[e.from] != INF && d[e.to] > d[e.from] + e.cost) {
                d[e.to] = d[e.from] + e.cost;
                update = true;
            }
        }
        if(!update) 
            break;
    }
}
```



