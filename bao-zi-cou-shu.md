## 包子凑数 {#历届试题-包子凑数}

问题描述

小明几乎每天早晨都会在一家包子铺吃早餐。他发现这家包子铺有N种蒸笼，其中第i种蒸笼恰好能放Ai个包子。每种蒸笼都有非常多笼，可以认为是无限笼。

每当有顾客想买X个包子，卖包子的大叔就会迅速选出若干笼包子来，使得这若干笼中恰好一共有X个包子。比如一共有3种蒸笼，分别能放3、4和5个包子。当顾客想买11个包子时，大叔就会选2笼3个的再加1笼5个的（也可能选出1笼3个的再加2笼4个的）。

当然有时包子大叔无论如何也凑不出顾客想买的数量。比如一共有3种蒸笼，分别能放4、5和6个包子。而顾客想买7个包子时，大叔就凑不出来了。

小明想知道一共有多少种数目是包子大叔凑不出来的。

输入格式

第一行包含一个整数N。\(1 &lt;= N &lt;= 100\)

以下N行每行包含一个整数Ai。\(1 &lt;= Ai &lt;= 100\)

输出格式

一个整数代表答案。如果凑不出的数目有无限多个，输出INF。

样例输入

2

4

5

样例输出

6

样例输入

2

4

6

样例输出

INF

---

## 解题思路： {#解题思路：}

满足所有数的最大公约数不为1则有无穷多个，否则都是有限个。

有限个的情况利用完全背包就可以进行统计。

---

## AC代码: {#ac代码}

```cpp
#include <algorithm>
#include <string.h>
#include <iostream>
#include <stdio.h>
#include <string>
#include <vector>
#include <queue>
#include <map>
#include <set>

using namespace std;

int n;
const int N = 10010;
bool dp[N];
int arr[110];

int gcd(int a, int b) {
    if(b == 0) 
        return a;
    return gcd(b, a % b);
}

int main() {

    ios::sync_with_stdio(false);

    cin >> n;
    for(int i = 0; i < n; ++i) {
        cin >> arr[i];
    }

    int g = arr[0];
    for(int i = 1; i < n; ++i) {
        g = gcd(g, arr[i]);
    }

    if(g != 1) {
        cout << "INF" << endl;
    } else {
        dp[0] = true;
        for(int i = 0; i < n; ++i) {
            for(int j = 0; j + arr[i]< N; ++j) {
                if(dp[j]) {
                    dp[j + arr[i]] = true;
                }
            }
        }

        int count = 0;
        for(int i = 0; i < N; ++i) {
            if(!dp[i]) {
                count++;
            }
        }
        cout << count << endl;
    }
    return 0;
}
```



