## 高精度加法

问题描述

输入两个整数a和b，输出这两个整数的和。a和b都不超过100位。

算法描述

由于a和b都比较大，所以不能直接使用语言中的标准数据类型来存储。对于这种问题，一般使用数组来处理。

定义一个数组A，A\[0\]用于存储a的个位，A\[1\]用于存储a的十位，依此类推。同样可以用一个数组B来存储b。

计算c=a+b的时候，首先将A\[0\]与B\[0\]相加，如果有进位产生，则把进位（即和的十位数）存入r，把和的个位数存入C\[0\]，即C\[0\]等于\(A\[0\]+B\[0\]\)%10。然后计算A\[1\]与B\[1\]相加，这时还应将低位进上来的值r也加起来，即C\[1\]应该是A\[1\]、B\[1\]和r三个数的和．如果又有进位产生，则仍可将新的进位存入到r中，和的个位存到C\[1\]中。依此类推，即可求出C的所有位。

最后将C输出即可。

输入格式

输入包括两行，第一行为一个非负整数a，第二行为一个非负整数b。两个整数都不超过100位，两数的最高位都不是0。

输出格式

输出一行，表示a+b的值。

样例输入

20100122201001221234567890

2010012220100122

样例输出

20100122203011233454668012

---

## 解题思路： {#解题思路：}

逐位相加的思想。

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

string sa, sb;
int a[120];
int b[120];
int sum[120];

int main(){  
    ios::sync_with_stdio(false);

    cin >> sa >> sb;
    int len_a = sa.length();
    int len_b = sb.length();
    int index = 0;
    for(int i = len_a - 1; i >= 0; --i) {
        a[index++] = sa[i] - '0';
    }
    index = 0;
    for(int i = len_b - 1; i >= 0; --i) {
        b[index++] = sb[i] - '0';
    }

    int r = 0;
    int len = max(len_a, len_b);
    index = 0;

    for(int i = 0; i <= len; ++i) {
        int isum = a[i] + b[i] + r;
        sum[index++] = isum % 10;
        r = isum / 10;
    }

    if(sum[index - 1] == 0) {
        index--;
    }
    for(int i = index -1; i >= 0; --i) {
        cout << sum[i];
    }
    cout << endl;
}
```



