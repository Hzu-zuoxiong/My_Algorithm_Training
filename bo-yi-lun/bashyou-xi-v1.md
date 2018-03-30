## Bash游戏 {#bash游戏}

有一堆石子共有N个。A B两个人轮流拿，A先拿。每次最少拿1颗，最多拿K颗，拿到最后1颗石子的人获胜。假设A B都非常聪明，拿石子的过程中不会出现失误。给出N和K，问最后谁能赢得比赛。

例如N = 3，K = 2。无论A如何拿，B都可以拿到最后1颗石子。

Input

第1行：一个数T，表示后面用作输入测试的数的数量。（1 &lt;= T &lt;= 10000\)

第2 - T + 1行：每行2个数N，K。中间用空格分隔。（1 &lt;= N,K &lt;= 10^9\)

Output

共T行，如果A获胜输出A，如果B获胜输出B。

Sample Input

```
4
3 2
4 2
7 3
8 3
```

Sample Output

```
B
A
A
B
```

---

## 解题思路： {#解题思路：}

只有一堆物品，共有n个，两人轮流从这对物品取，规定每次至少取一个，最多取m个，取最后一个胜。

1、当n&lt;=m时，先取者可一次去完，所以先取者胜；

2、当n=m+1时，无论先取者如何取，后取者都可一次性取完，所以后取者胜。

如果是\(k+1\)的整数倍，先手取任何一个1~k内的数x，后手都可以取\(k+1-x\)个石子，则先手一直面对（k+1）的整数倍的状态，于是（k+1）的整数倍是先手的必败态，同理，不是k+1的整数倍时，先手可以取n%\(k+1\)个石子，从而使后手必败。

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

    while(t--) {

        int n, k;
        cin >> n >> k;

        if(n % (k + 1)) {
            cout << "A\n";
        } else {
            cout << "B\n";
        }
    }
}
```



