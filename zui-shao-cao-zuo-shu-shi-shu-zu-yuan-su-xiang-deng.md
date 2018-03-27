## 最少操作数使数组元素相等 {#最少操作数使数组元素相等}

题目描述：给定一个长度为n的非空整数数组，找出使数组所有元素均相等的最少操作数，其中每一次操作将其中n-1个数加上1。

样例：

输入：\[1, 2, 3\]

输出：3

说明：最少3次操作达到要求：\[1, 2, 3\] =&gt; \[2, 3, 3\] =&gt; \[3, 4, 3\] =&gt; \[4, 4, 4\]

---

## 解题思路： {#解题思路：}

将n - 1个数加 1，相当于将所有数都加 1，再将其中一个数减去1。将所有数加1的操作并不会改变数之间两两差值。

要使次数最小，且每次只能将元素减 1，故应当把所有数减到与最小值相等。

若sum = a0 + a1 + a2 + ... + an-1，则减少的次数为sum - min \* n（min为数组中的最小值）

---

## AC代码： {#ac代码：}

```cpp
#include<iostream>
#include<string>
#include<algorithm>
#include<queue>
#include<set>
#include<stack>
#include<vector>

using namespace std;

int t;
int n;
int sum;
int Min = 10005;
int times;

int main() {

    ios::sync_with_stdio(false);

    cin >> t;

    while(t--) {
        sum = 0;
        Min = 10005;
        cin >> n;
        int temp;
        for(int i = 0; i < n; ++i) {
            cin >> temp;
            sum += temp;
            Min = min(Min, temp);          
        }

        times = sum - Min * n;
        cout << times << endl;
    }
}
```



