## 威佐夫游戏 V2 {#problem-title}

有2堆石子。A B两个人轮流拿，A先拿。每次可以从一堆中取任意个或从2堆中取相同数量的石子，但不可不取。拿到最后1颗石子的人获胜。假设A B都非常聪明，拿石子的过程中不会出现失误。给出2堆石子的数量，问最后谁能赢得比赛。

例如：2堆石子分别为3颗和5颗。那么不论A怎样拿，B都有对应的方法拿到最后1颗。

Input

第1行：一个数T，表示后面用作输入测试的数的数量。（1 &lt;= T&lt;= 10000\)

第2 - T + 1行：每行2个数分别是2堆石子的数量，中间用空格分隔。\(1 &lt;= N &lt;= 10^18\)

Output

共T行，如果A获胜输出A，如果B获胜输出B。

Sample Input

```
3
3 5
3 4
1 9

```

Sample Output

```
B
A
A

```

---

## 解题思路： {#解题思路：}

因题目数据较大\(1 &lt;= N &lt;= 10^18\)，直接套用公式k\*\(sqrt\(5\)+1\)/2会产生精度问题，所以需要模拟大数乘法。

有公式ak =\[k（1+√5）/2\]，bk= ak + k，其中\(sqrt\(5\)+1\)/2的值为1.618…其-1的值为0.618033988749894848...即黄金分割比例。

所以，判断ak是否符合威佐夫博弈的条件，只需模拟k（1+√5）/2相乘的过程，它等价于k \* 黄金分割比例 + k\(k = bk - ak\)。

模拟乘法过程：

![](https://hzu-zuoxiong.gitbooks.io/algorithm_training/content/assets/%E5%A8%81%E4%BD%90%E5%A4%AB%E5%8D%9A%E5%BC%88V2.png)

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

typedef unsigned long long ULL;
const ULL Gold[3] = {618033988, 749894848, 204586834};
const ULL MOD = 1e9;

int main(){  

    ios::sync_with_stdio(false);

    int t;
    cin >> t;
    ULL a, b;

    while(t--) {
        cin >> a >> b;
        if(a > b)
            swap(a, b);
        //k = bk - ak;
        ULL dist = b - a;
        ULL pre = dist / MOD;
        ULL last = dist % MOD;
        ULL a1 = last * Gold[2];
        ULL a2 = pre * Gold[2] + last * Gold[1] + a1 / MOD;
        ULL a3 = pre * Gold[1] + last * Gold[0] + a2 / MOD;
        ULL a4 = dist + pre * Gold[0] + a3 / MOD;
        if(a4 == a) {
            cout << "B\n";
        } else {
            cout << "A\n";
        }
    }
}

```



