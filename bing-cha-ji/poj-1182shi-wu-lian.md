## 食物链 {#食物链}

Description

动物王国中有三类动物A,B,C，这三类动物的食物链构成了有趣的环形。A吃B， B吃C，C吃A。

现有N个动物，以1－N编号。每个动物都是A,B,C中的一种，但是我们并不知道它到底是哪一种。

有人用两种说法对这N个动物所构成的食物链关系进行描述：

第一种说法是"1 X Y"，表示X和Y是同类。

第二种说法是"2 X Y"，表示X吃Y。

此人对N个动物，用上述两种说法，一句接一句地说出K句话，这K句话有的是真的，有的是假的。当一句话满足下列三条之一时，这句话就是假话，否则就是真话。

1） 当前的话与前面的某些真的话冲突，就是假话；

2） 当前的话中X或Y比N大，就是假话；

3） 当前的话表示X吃X，就是假话。

你的任务是根据给定的N（1 &lt;= N &lt;= 50,000）和K句话（0 &lt;= K &lt;= 100,000），输出假话的总数。

Input

第一行是两个整数N和K，以一个空格分隔。

以下K行每行是三个正整数 D，X，Y，两数之间用一个空格隔开，其中D表示说法的种类。

若D=1，则表示X和Y是同类。

若D=2，则表示X吃Y。

Output

只有一个整数，表示假话的数目。

Sample Input

```
100 7
1 101 1 
2 1 2
2 2 3 
2 3 3 
1 1 3 
2 3 1 
1 5 5

```

Sample Output

```
3

```

---

## 解题思路： {#解题思路：}

此题是并查集的一个典型，在此题中创建3倍N大小的数组，0--N表示A动物，N--2N表示B动物，2N--3N表示C动物，并用这个3N数组建立并查集。

应 i--X 表示“ i 属于种类X”

根据题意，本题输入的两种动物有两种关系：

1. X 与 Y 属于同一类 此时，合并X--A和Y--A、X--B和Y--B、X--C和Y--C
2. X 吃 Y 此时，合并X--A和Y--B、X--B和Y--C、X--C和Y--A\(分别代表着A吃B，B吃C，C吃A\)

---

## AC代码： {#ac代码：}

```cpp
#include<iostream>
#include<cstdio>
#include<set>
#include<string>
#include<stack>
#include<vector>

using namespace std;

const int N = 150010;
int par[N];
int n;
int k;

int find(int x) {
    return par[x] == x ? x : par[x] = find(par[x]);
}

void unite(int x, int y) {
    x = find(x);
    y = find(y);
    if(x != y) {
        par[x] = y;
    }
}

bool same(int x, int y) {
    return find(x) == find(y);
}

int main() {

    scanf("%d %d", &n, &k);
    for(int i = 0; i < 3 *n; i++) {
        par[i] = i;
    }

    int ans = 0;
    while(k--) {

        int a, x, y;
        //用C++的输入输出一直超时，
        //加ios::sync_with_stdio(false);也是超时
        //没办法只能用scanf和printf了 
        scanf("%d %d %d", &a, &x, &y);
        x = x - 1;
        y = y - 1;

        if(x < 0 || x >= n || y < 0 || y >= n) {
            ans++;
            continue;
        }            

        if(a == 1) {

            if(same(x, y + n) || same(x, y + 2 * n)) {
                ans++;
            }else {
                unite(x, y);
                unite(x + n, y + n);
                unite(x + 2 * n, y + 2 * n);
            }        

        } else {

            if(same(x, y) || same(x, y + 2 * n)) {
                ans++;
            } else {
                unite(x, y + n);
                unite(x + n, y + 2 * n);
                unite(x + 2 * n, y);
            }
        }
    }

    printf("%d\n", ans);
    return 0;
}
```



