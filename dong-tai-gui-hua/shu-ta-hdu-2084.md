## [数塔](https://vjudge.net/problem/HDU-2084)[HDU - 2084](https://vjudge.net/problem/23620/origin) {#problem-title}

在讲述DP算法的时候，一个经典的例子就是数塔问题，它是这样描述的：

有如下所示的数塔，要求从顶层走到底层，若每一步只能走到相邻的结点，则经过的结点的数字之和最大是多少？

![](https://odzkskevi.qnssl.com/79b65092734d6a263a9280f5b332c5b9?v=1517370965)

已经告诉你了，这是个DP的题目，你能AC吗?

Input

输入数据首先包括一个整数C,表示测试实例的个数，每个测试实例的第一行是一个整数N\(1 &lt;= N &lt;= 100\)，表示数塔的高度，接下来用N行数字表示数塔，其中第i行有个i个整数，且所有的整数均在区间\[0,99\]内。

Output

对于每个测试实例，输出可能得到的最大和，每个实例的输出占一行。

Sample Input

```
1
5
7
3 8
8 1 0 
2 7 4 4
4 5 2 6 5

```

Sample Output

```
30

```

---

## 解题思路： {#解题思路：}

![](https://hzu-zuoxiong.gitbooks.io/algorithm_training/content/assets/%E6%95%B0%E5%A1%941.png)

将输入用map数组保存，用数组f进行动态规划，即f\[i\]\[j\]表示从顶点（1，1）到顶点（i，j）的最大值。

此题有自顶向下和自底向上两种方法解决问题：

自底向上：状态转移方程：f\[i\]\[j\] = max\(f\[i + 1\]\[j\], f\[i + 1\]\[j + 1\]\) + map\[i\]\[j\]; f\[1\]\[1\]为最大值。

自顶向下：状态转移方程：f\[i\]\[j\] = max\(f\[i - 1\]\[j - 1\], f\[i - 1\]\[j\]\) + map\[i\]\[j\]; 需要在最后一列中找出最大值。

---

## 自底向上，代码： {#自底向上，代码：}

```cpp
#include<iostream>
#include<string>
#include<queue>
#include<cstring>
#include<stack>
#include<cmath>
#include<algorithm>

using namespace std;

int f[105][105];
int map[105][105]; 
int c;
int n;

int main(){  
    ios::sync_with_stdio(false);

    cin >> c;
    while(c--) {
        memset(f, 0, sizeof(int));
        memset(map, 0, sizeof(int));

        cin >> n;
        for(int i = 1; i <= n; ++i) {
            for(int j = 1; j <= i; ++j ) {
                cin >> map[i][j];
            }
        }

        for(int i = 1; i <= n; ++i) {
            f[n][i] = map[n][i];
        }

        for(int i = n; i >= 1; --i) {
            for(int j = 1; j <= i; ++j) {
                f[i][j] = max(f[i + 1][j], f[i + 1][j + 1]) + map[i][j];
            }
        }

//        cout << "----------" << endl;    
//        for(int i = 0;  i <= n; ++i) {
//            for(int j = 0; j <= i; ++j) {
//                cout << f[i][j] << " ";
//            }
//            cout << endl;
//        }

        cout << f[1][1] << endl;

    }
}
```

## 自顶向下，代码： {#自顶向下，代码：}

```cpp
#include<iostream>
#include<string>
#include<queue>
#include<cstring>
#include<stack>
#include<cmath>
#include<algorithm>

using namespace std;

int f[105][105];
int map[105][105]; 
int c;
int n;

int main(){  
    ios::sync_with_stdio(false);

    cin >> c;
    while(c--) {
        memset(f, 0, sizeof(int));
        memset(map, 0, sizeof(int));

        cin >> n;
        for(int i = 1; i <= n; ++i) {
            for(int j = 1; j <= i; ++j ) {
                cin >> map[i][j];
            }
        }

        f[1][1] = map[1][1];
        for(int i = 2; i <= n; ++i) {
            for(int j = 1; j <= i; ++j) {
                f[i][j] = max(f[i - 1][j - 1], f[i - 1][j]) + map[i][j];
            }
        }

//        cout << "----------" << endl;    
//        for(int i = 0;  i <= n; ++i) {
//            for(int j = 0; j <= i; ++j) {
//                cout << f[i][j] << " ";
//            }
//            cout << endl;
//        }

        int imax = 0;
        for(int i = 1; i <= n; ++i) {
            imax = max(imax, f[n][i]);
        }

        cout << imax << endl;
    }
}
```



