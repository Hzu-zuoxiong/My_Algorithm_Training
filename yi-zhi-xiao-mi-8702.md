## [一只小蜜蜂...](https://vjudge.net/problem/HDU-2044) {#problem-title}

有一只经过训练的蜜蜂只能爬向右侧相邻的蜂房，不能反向爬行。请编程计算蜜蜂从蜂房a爬到蜂房b的可能路线数。

其中，蜂房的结构如下所示。

![](https://odzkskevi.qnssl.com/db4917bb4b1bd4e9ccc285a9597f8e31?v=1514927247)

Input

输入数据的第一行是一个整数N,表示测试实例的个数，然后是N 行数据，每行包含两个整数a和b\(0&lt;a&lt;b&lt;50\)。

Output

对于每个测试实例，请输出蜜蜂从蜂房a爬到蜂房b的可能路线数，每个实例的输出占一行。

Sample Input

```
2
1 2
3 6

```

Sample Output

```
1
3

```

---

## 解题思路： {#解题思路：}

如果a-b的绝对值相同，则他们之间的线路数也相同。如：

1--&gt;2，有1条路；2--&gt;3，有一条路。

1--&gt;3则可以看成是1--&gt;2--&gt;3，即1+1条路。

1--&gt;4则可以看成是1--&gt;2--&gt;3--&gt;4，即1+1+1条路。

......

这样依此类推，则可以找出a--&gt;b之间有多少条路。

PS：数据范围较大，int型满足不足，需设置为long long类型。

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

    sum[0] = 0;
    sum[1] = 1;
    sum[2] = 2;

    for(int i = 3; i < 50; ++i) {
        sum[i] = sum [i - 1] + sum[i - 2];
    }

    int n;
    cin >> n;
    while(n--) {
        int a, b;
        cin >> a >> b;
        int temp = abs(a - b);
        cout << sum[temp] << endl;
    }
}
```



