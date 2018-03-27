## 畅通工程之最低成本建设问题 {#畅通工程之最低成本建设问题}

某地区经过对城镇交通状况的调查，得到现有城镇间快速道路的统计数据，并提出“畅通工程”的目标：使整个地区任何两个城镇间都可以实现快速交通（但不一定有直接的快速道路相连，只要互相间接通过快速路可达即可）。现得到城镇道路统计表，表中列出了有可能建设成快速路的若干条道路的成本，求畅通工程需要的最低成本。

### 输入格式: {#-}

输入的第一行给出城镇数目N\(1&lt;N≤1000\)和候选道路数目M≤3N；随后的M行，每行给出3个正整数，分别是该条道路直接连通的两个城镇的编号（从1编号到N）以及该道路改建的预算成本。

### 输出格式: {#-}

输出畅通工程需要的最低成本。如果输入数据不足以保证畅通，则输出“Impossible”。

### 输入样例1: {#-1-}

```
6 15
1 2 5
1 3 3
1 4 7
1 5 4
1 6 2
2 3 4
2 4 6
2 5 2
2 6 6
3 4 6
3 5 1
3 6 1
4 5 10
4 6 8
5 6 3

```

### 输出样例1: {#-1-}

```
12

```

### 输入样例2: {#-2-}

```
5 4
1 2 1
2 3 2
3 1 3
4 5 4

```

### 输出样例2: {#-2-}

```
Impossible

```

---

## 解题思路： {#解题思路：}



---

## AC代码： {#ac代码：}

```cpp
#include<iostream>
#include<cstdio>
#include<set>
#include<algorithm>
#include<string>
#include<stack>
#include<vector>

using namespace std;

const int N = 100005;
int par[N];

struct Node{
    int pre;
    int next;
    int w;
}node[3005];

int ans;
int cnt;

int comp(const Node a, const Node b) {
    return a.w < b.w;
}

void init(int n) {
    for(int i = 0; i < n; ++i) {
        par[i] = i;
    }
}

int find(int x) {
    return par[x] == x ? x : par[x] = find(par[x]);
}

int main() {

    int n;
    int m;
    cin >> n >> m;

    init(n + 5);
    for(int i = 0; i < m; ++i) {

        int a, b, c;
        cin >> a >> b >> c;
        node[i].pre = a;
        node[i].next = b;
        node[i].w = c;        
    }

    sort(node, node + m, comp);

    for(int i = 0; i < m; i++) {

        int x = find(node[i].pre);
        int y = find(node[i].next);
        if(x != y) {
            par[x] = y;
            ans += node[i].w;
        }

    }

    for(int i = 1; i <= n; ++i) {
        if(par[i] != i) {
            cnt++;
        }
    }
    
    if(cnt != n - 1) {
        cout << "Impossible" << endl;
    } else {
        cout << ans << endl;
    }
    return 0;
}
```



