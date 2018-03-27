## 八皇后问题 {#八皇后问题}

POJ 2698

经典的八皇后问题：在8×8格的国际象棋上摆放八个皇后，使其不能互相攻击，即任意两个皇后都不能处于同一行、同一列或同一斜线上，问有多少种摆法。

---

## 代码: {#代码}

```cpp
#include<iostream>
#include<string>
#include<queue>
#include<cstring>
#include<stack>
#include<cmath>
#include<algorithm>

using namespace std;

int ans;
int vis[10];

bool check(int r, int l) {
    for(int i = 1; i < r; ++i) {
        if(vis[i] == l) {
            return false;
        }
        if(vis[i] - l ==  r - i || vis[i] - l == i - r) {
            return false;
        }
    }
    return true;
}

void dfs(int r) {
    if(r > 8) {
        ans++;
        return;
    }
    for(int i = 1; i <= 8; ++i) {
        if(check(r, i)) {
            vis[r] = i;
            dfs(r + 1);
            vis[r] = 0;
        }
    }    
}


int main() {
    ios::sync_with_stdio(false);

    dfs(1);
    cout << ans << endl;    
}
```



