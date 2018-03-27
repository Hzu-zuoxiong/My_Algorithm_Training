[不容易系列之\(3\)—— LELE的RPG难题](https://vjudge.net/problem/HDU-2045)

人称“AC女之杀手”的超级偶像LELE最近忽然玩起了深沉，这可急坏了众多“Cole”（LELE的粉丝,即"可乐"）,经过多方打探，某资深Cole终于知道了原因，原来，LELE最近研究起了著名的RPG难题:

有排成一行的ｎ个方格，用红\(Red\)、粉\(Pink\)、绿\(Green\)三色涂每个格子，每格涂一色，要求任何相邻的方格不能同色，且首尾两格也不同色．求全部的满足要求的涂法.

以上就是著名的RPG难题.

如果你是Cole,我想你一定会想尽办法帮助LELE解决这个问题的;如果不是,看在众多漂亮的痛不欲生的Cole女的面子上,你也不会袖手旁观吧?

Input

输入数据包含多个测试实例,每个测试实例占一行,由一个整数N组成，\(0&lt;n&lt;=50\)。

Output

对于每个测试实例，请输出全部的满足要求的涂法，每个实例的输出占一行。

Sample Input

```
1
2

```

Sample Output

```
3
6

```

---

## 解题思路： {#解题思路：}

1. 由题意可知：F\(1\) = 3, F\(2\) = 6, F\(3\) = 6
2. 对第n个格子填色，根据n - 1个格子，分为2种情况：
   1. 已知F\(n - 1\)，当对第n个格子填色时，因第n - 1个格子与第一个格子颜色不一样，又因首尾不能同色，则第n个格子只有一种选择，则共有F\(n-1\)种可能。
   2. 已知F\(n - 2\)，此时n - 1个格子与第一个格子不受首尾不能同色的规则限制，则假设第n-1个格子与第一个格子同色，则第n个格子有两种选择，则共有2\*F\(n - 2\)种可能。

---

## AC代码： {#ac代码：}

```cpp
#include<iostream>
#include<string>
#include<queue>
#include<cstring>
#include<stack>
#include<cmath>

using namespace std;

long long sum[55];

int main() {

    ios::sync_with_stdio(false);

    sum[1] = 3;
    sum[2] = 6;
    sum[3] = 6;

    for(int i = 4; i <= 50; ++i) {
        sum[i] = sum [i - 1] + 2 * sum[i - 2];
    }

    int n;
    while(cin >> n) {
        cout << sum[n] << endl;
    }
}
```



