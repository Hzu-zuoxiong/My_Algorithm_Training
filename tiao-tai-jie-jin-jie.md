## 跳台阶进阶 {#跳台阶进阶}

题目描述： 一个台阶总共有 n 级，如果一次可以跳 1 级，也可以跳 2 级……也可以跳 n 级，求跳到 n 阶台阶有多少种跳法。

显而易见，当n = 1时，Fib\(1\) = 1；当n = 2时，Fib\(2\) = 2；

当n = 3时，Fib\(3\) = Fib\(1\) + Fib\(2\) + 1 = 4;

当n = 4时，Fib\(4\) = Fib\(1\) + Fib\(2\) + Fib\(3\) + 1 = 8；

当n = 5时，Fib\(5\) = Fib\(1\) + Fib\(2\) + Fib\(3\) + Fib\(4\) + 1 = 16；

当n = 6时，Fib\(6\) = Fib\(1\) + Fib\(2\) + Fib\(3\) + Fib\(4\) + Fib\(5\) + 1 = 32；

......

规律可得：

Fib\(n - 1\) = Fib\(1\) + Fib\(2\) + ....... + Fib\(n - 2\) + 1；

Fib\(n\) = Fib\(1\)+Fib\(2\)+.......+ Fib\(n - 2\) + Fib\(n - 1\) + 1;

则，Fib\(n\) = Fib\(n - 1\) + Fib\(n - 1\) = 2 \* Fib\(n - 1\)；

## AC代码： {#代码：}

```cpp
#include<iostream>
#include<string>
#include<algorithm>
#include<queue>
#include<set>
#include<stack>

using namespace std;

int n;
int t;
long long nums[35];

void init() {
    nums[1] = 1;
    nums[2] = 2;

    for(int i = 3; i <= 35; ++i) {
        nums[i] = 2 * nums[i - 1];
    }
}

int main() {

    cin >> t;
    init();
    while(t--) {
        cin >> n;
        cout << nums[n] << endl;
    }
    return 0;
}
```



