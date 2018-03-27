## [Nim游戏](https://vjudge.net/problem/51Nod-1069) {#problem-title}

有N堆石子。A B两个人轮流拿，A先拿。每次只能从一堆中取若干个，可将一堆全取走，但不可不取，拿到最后1颗石子的人获胜。假设A B都非常聪明，拿石子的过程中不会出现失误。给出N及每堆石子的数量，问最后谁能赢得比赛。

例如：3堆石子，每堆1颗。A拿1颗，B拿1颗，此时还剩1堆，所以A可以拿到最后1颗石子。

Input

第1行：一个数N，表示有N堆石子。（1 &lt;= N &lt;= 1000\)

第2 - N + 1行：N堆石子的数量。\(1 &lt;= Ai&lt;= 10^9\)

Output

如果A获胜输出A，如果B获胜输出B。

Sample Input

```
3
1
1
1

```

Sample Output

```
A

```

---

## 解题思路： {#解题思路：}

先手必胜态：当且仅当这两堆石子的数目相等。

只有两堆石子的话，第一个取石头使得两堆石头数相等（A胜），如果一开始石头就相等（B胜）。

当这些数都做异或运算，结果为1，先手胜后手输；结果为2，先手输后手胜。

---

## AC代码：

```cpp
#include<iostream>
#include<string>
#include<queue>
#include<cstring>
#include<stack>
#include<cmath>

using namespace std;

int main(){  
    ios::sync_with_stdio(false);

    int t;
    cin >> t;
    int ans;

    for(int i = 0; i < t; ++i) {
        int t;
        cin >> t;
        if(!i) {
            ans = t;
        } else {
            ans ^= t;
        }
    }
    if(ans) {
        cout << "A\n";
    } else {
        cout << "B\n";
    }
}
```



