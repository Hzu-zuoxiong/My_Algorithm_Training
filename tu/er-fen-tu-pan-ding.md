## 二分图判定

《挑战程序设计竞赛》P97

对图进行染色所需要的最小颜色称为最小着色数。最小着色数是2的图称作二分图。

要求：给定一个具有n个顶点的图，要给图上每个顶点染色，并且要使相邻的顶点颜色不同。问是否能最多用2种颜色进行染色？题目保证没有重边和自环。

限制条件:\(1&lt;=n&lt;=1e3\)

输入：

\(n=\)3,\(e=\)3

0 1

0 2

1 2

输出：

NO  


输入：

\(n=\)4,\(e=\)4

0 1

0 3

1 2

2 3

输出：

Yes

---

## 解题思路：

如果只用2种颜色，那么确定一个顶点的颜色之后，和它相邻的顶点的颜色也就确定了。因此，选择任意一个顶点出发，依次确定相邻顶点的颜色，就可以判断是否可以被2种颜色染色了。这个问题如果用深度优先搜索的话，能够简单地实现。

---

代码：

```cpp
#include<cstdio>
#include<algorithm>
#include<cstring>
#include<iostream>
#include<vector>

using namespace std;

const int maxv = 1e3+5;
int v, e; 
vector<int>G[maxv];
int color[maxv];

bool dfs(int v, int c) {
	//把顶点染成c 
	color[v] = c;
	for(int i = 0; i < G[v].size(); i++) {
		//若相邻的顶点同色，则返回false
		if(color[G[v][i]] == c)
			return false;
		//若相邻的顶点还未染色，则染成-c
		if(color[G[v][i]] == 0 && !dfs(G[v][i], -c))
			return false;
	} 
	return true;
}

void solve() {
	for(int i = 0; i < v; i++) {
		if(color[i] == 0) {
			//若顶点i还未染色，则染成1 
			if(!dfs(i , 1)) {
				cout << "No" << endl;
				return;
			}
		}
	}
	cout << "Yes" << endl;
}

int main()
{
	cin >> v >> e;
	for(int i = 0; i < e; i++) {
		int s, t;
		cin >> s >> t;
		G[s].push_back(t);
		G[t].push_back(s); 
	}
	
	solve();
    return 0;
}
```



