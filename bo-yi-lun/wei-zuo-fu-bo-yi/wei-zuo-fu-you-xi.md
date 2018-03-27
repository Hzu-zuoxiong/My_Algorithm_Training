## [威佐夫游戏](https://vjudge.net/problem/51Nod-1072) {#problem-title}

有2堆石子。A B两个人轮流拿，A先拿。每次可以从一堆中取任意个或从2堆中取相同数量的石子，但不可不取。拿到最后1颗石子的人获胜。假设A B都非常聪明，拿石子的过程中不会出现失误。给出2堆石子的数量，问最后谁能赢得比赛。  
例如：2堆石子分别为3颗和5颗。那么不论A怎样拿，B都有对应的方法拿到最后1颗。  
Input  
第1行：一个数T，表示后面用作输入测试的数的数量。（1 &lt;= T &lt;= 10000\)  
第2 - T + 1行：每行2个数分别是2堆石子的数量，中间用空格分隔。\(1 &lt;= N &lt;= 2000000\)  
Output  
共T行，如果A获胜输出A，如果B获胜输出B。  
Sample Input  
3  
3 5  
3 4  
1 9  
Sample Output  
B  
A  
A+

---

## AC代码： {#ac代码}

```cpp
#include<iostream>
#include<cstring>
#include<cmath>
#include<algorithm>
using namespace std;
int T,N,M;

int main()
{
    /*cin慢是有原因的，其实默认的时候，cin与stdin总是保持同步的，也就是说这两种方法可以混用，
    而不必担心文件指针混乱，同时cout和stdout也一样，两者混用不会输出顺序错乱。正因为这个兼容性的特性，
    导致cin有许多额外的开销，如何禁用这个特性呢？只需一个语句std::ios::sync_with_stdio(false);
    这样就可以取消cin于stdin的同步了。*/
    ios::sync_with_stdio(false);
    cin>>T;
    while(T--)
    {
        cin>>N>>M;
        if (N>M) swap(N,M);
        //k=bk-ak;
        if (N==(int)((1.0+sqrt(5.0))/2.0*(M-N)))
            cout<<"B\n";
        else
            cout<<"A\n";
    }
    return 0;
}
```



