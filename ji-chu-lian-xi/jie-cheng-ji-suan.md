## 阶乘计算 {#阶乘计算}

问题描述

输入一个正整数n，输出n!的值。

其中n!=1\*2\*3\*…\*n。

算法描述

```
 n!可能很大，而计算机能表示的整数范围有限，需要使用高精度计算的方法。使用一个数组A来表示一个大整数a，A[0]表示a的个位，A[1]表示a的十位，依次类推。

将a乘以一个整数k变为将数组A的每一个元素都乘以k，请注意处理相应的进位。

首先将a设为1，然后乘2，乘3，当乘到n时，即得到了n!的值。

```

输入格式

输入包含一个正整数n，n&lt;=1000。

输出格式

输出n!的准确值。

样例输入

10

样例输出

3628800

---

解题思路：

创建一个数组，利用数组逐位相乘求出最终答案。

---

## AC代码： {#ac代码：}

```cpp
#include<iostream>
#include<string>
#include<queue>
#include<cstring>
#include<stack>
#include<cmath>
#include<algorithm>

using namespace std;

int num[5000]; 
int n;

int main(){  
    ios::sync_with_stdio(false);

    num[0] = 1;
    cin >> n;
    int r = 0;
    for(int i = 2; i <= n; ++i) {
        for(int k = 0; k < 5000; ++k) {
            int temp = num[k] * i + r;
            r = temp / 10;
            num[k] = temp % 10;
        }
    }
    int index = 0;
    for(index = 4999; index >= 0; --index) {
        if(num[index]) {
            break;
        }
    }

    for(int i = index; i >= 0; --i) {
        cout << num[i];
    }
    cout << endl;
}
```



