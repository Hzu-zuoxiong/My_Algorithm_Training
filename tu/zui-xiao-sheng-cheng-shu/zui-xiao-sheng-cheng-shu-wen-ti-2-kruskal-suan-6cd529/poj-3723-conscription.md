## Conscription

**Description**

Windy has a country, and he wants to build an army to protect his country. He has picked upNgirls andMboys and wants to collect them to be his soldiers. To collect a soldier without any privilege, he must pay 10000 RMB. There are some relationships between girls and boys and Windy can use these relationships to reduce his cost. If girl**x**and boy**y**have a relationshipdand one of them has been collected, Windy can collect the other one with 10000-dRMB. Now given all the relationships between girls and boys, your assignment is to find the least amount of money Windy has to pay. Notice that only one relationship can be used when collecting one soldier.

**Input**

The first line of input is the number of test case.  
The first line of each test case contains three integers,N,MandR.  
ThenRlines followed, each contains three integersxi,yianddi.  
There is a blank line before each test case.

1 ≤N,M≤ 10000  
0 ≤R≤ 50,000  
0 ≤xi&lt;N  
0 ≤yi&lt;M  
0 &lt;di&lt; 10000

**Output**

For each test case output the answer in a single line.

**Sample Input**

```
2

5 5 8
4 3 6831
1 3 4583
0 0 6592
0 1 3063
3 3 4975
1 3 2049
4 2 2104
2 2 781

5 5 10
2 4 9820
3 2 6236
3 1 8864
2 4 8326
2 0 5156
2 0 1463
4 1 2439
0 4 4373
3 4 8889
2 4 3133

```

**Sample Output**

```
71071
54223
```

---

## 解题思路：

题目大意：要招募n个女兵和m个男兵，而每招募一个人都要花费10000，可以用男女之间的关系减少费用，因为当招募一个士兵时，如果已招的人里与其有t点关系，则只需10000-n的费用。

分析：把n个女兵和m个男兵看成V=\(n + m\)个顶点，将他们之间的关系 r 转成负数，则可以看成是最小生成树的问题，最终费用为（n + m） \* 10000 + 最小生成树的值，则为最终答案。

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

struct edge{
	int from;
	int to;
	int cost;
};

edge es[50010];
int par[50010];
int rank[50010];
int n, m, r;

void init(int n) {
	for(int i = 0; i < n; i++) {
		par[i] = i;
		rank[i] = 0;
	}
}

int find(int x) {
	if(par[x] == x)
		return x;
	return par[x] = find(par[x]);
}

void unite(int x, int y) {
	x = find(x);
	y = find(y);
	
	if(x == y) {
		return;
	}
	
	if(rank[x] < rank[y]) {
		par[x] = y;
	} else {
		par[y] = x;
		if(rank[x] == rank[y])
			rank[x]++;
	}
}

bool same(int x, int y) {
	return find(x) == find(y);
}

bool comp(const edge& e1, const edge& e2) {
	return e1.cost < e2.cost;
}

int kruskal() {
	int res = 0;
	init(n + m);
	sort(es, es + r, comp);
	for(int i = 0; i < r; i++) {
		edge e = es[i];
		if(!same(e.from, e.to)) {
			unite(e.from, e.to);
			res += e.cost;
		}	
	}
	return res; 
}

int main()
{

	//用C++的输入输出会超时，还是不清楚什么原因
        //ios::sync_with_stdio(false);
	
	int t;
	scanf("%d", &t);
	while(t--) {
		
		scanf("%d %d %d", &n, &m, &r);
		
		for(int i = 0; i < r; i++) {
			int x, y, w;
			scanf("%d %d %d", &x, &y, &w);
			es[i].from = x;
			es[i].to = n + y;
			es[i].cost = -w;
		}
		
		printf("%d\n", 10000 * (n + m) + kruskal());
		
	}
}
```





