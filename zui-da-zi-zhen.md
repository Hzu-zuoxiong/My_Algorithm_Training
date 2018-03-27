## 最大子阵 {#历届试题-最大子阵}

问题描述

　　给定一个n\*m的矩阵A，求A中的一个非空子矩阵，使这个子矩阵中的元素和最大。

　　其中，A的子矩阵指在A中行和列均连续的一块。

输入格式

　　输入的第一行包含两个整数n, m，分别表示矩阵A的行数和列数。

　　接下来n行，每行m个整数，表示矩阵A。

输出格式

　　输出一行，包含一个整数，表示A中最大的子矩阵中的元素和。

样例输入

3 3

-1 -4 3

3 4 -1

-5 -2 8

样例输出

10

样例说明

　　取最后一列，和为10。

数据规模和约定

　　对于50%的数据，1&lt;=n, m&lt;=50；

　　对于100%的数据，1&lt;=n, m&lt;=500，A中每个元素的绝对值不超过5000。

---

## 解题思路： {#解题思路：}

此道题是求最大子序列和的变形。先从求最大子序列和讲起：输入一个整数序列，求出其中连续子序列和的最大值。

---

## AC代码： {#ac代码：}

```cpp
#include <algorithm>
#include <string.h>
#include <iostream>
#include <cstdio>
#include <string>
#include <vector>
#include <queue>
#include <map>
#include <set>

using namespace std;

int n, m;
int imax = INT_MIN;
int h[1005];
int rect[1005][1005];
int cur;

int main() {

    ios::sync_with_stdio(false);

    cin >> n >> m;
    for(int i = 0; i < n; ++i) {
        for(int j = 0; j < m; ++j) {
            cin >> rect[i][j];
        }
    }


    for(int i = 0; i < n;  ++i) {
        memset(h, 0, m*sizeof(int));
        for(int j = i; j < n; ++j) {
            cur = 0;
            for(int k = 0; k < m; ++k) {
                h[k] += rect[j][k];
                cur += h[k];
                imax = max(imax, cur);
                cur = cur < 0 ? 0 : cur;
            }
        } 
    }

    cout << imax << endl;

    return 0;
}
```



