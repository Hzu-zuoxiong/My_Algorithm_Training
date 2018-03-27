## 最长回文子序列

要求：给定字符串，求它的最长回文子序列长度。回文子序列反转字符顺序后仍然与原序列相同。例如字符串abcdfcba中，最长回文子序列长度为7，abcdcba或abcfcba。

思路：对于任意字符串，有如下两种情况

1. 首尾字符相同，那么最长回文子序列等于不包含首尾字符的字符串的最长子序列加上首尾；
2. 首尾字符不同，那么最长回文子序列等于只包含首字符（或只包含尾字符）的字符串的最长回文子序列的较大者。

其动态规划的状态转移方程为：

状态初始条件：dp\[ i \]\[ i \] = 1

状态转移方程：

当str\[ i \] == str\[ j \]时 dp\[ i \]\[ j \] = dp\[ i + 1 \]\[ j - 1 \] + 2

当str\[ i \] != str\[ j \]时 dp\[ i \]\[ j \] = max\(dp\[ i + 1\]\[ j \], dp\[ i \]\[ j - 1\]\)

举例： 字符串"google"

由动态规划画出其dp表：

![](https://hzu-zuoxiong.gitbooks.io/algorithm_training/content/assets/%E6%9C%80%E9%95%BF%E5%9B%9E%E6%96%87%E5%AD%90%E5%BA%8F%E5%88%971.png)

## 代码： {#代码：}

计算dp\[ i \]\[ j \]时需要知道dp\[ i + 1 \]\[ \* \]或dp\[ \* \]\[ j - 1 \]，因此 i 应该从大到小递减， j 应该从小到大递增。

```cpp
#include <cstdio>
#include <cstring>
#include <cmath>
#include<algorithm>
#include <queue>
#include <vector>
#include <iterator>
#include<iostream>

using namespace std;

int LPS(string s) {

    int len = s.length();
    vector<vector<int> > dp(len, vector<int>(len));

    for(int i = len - 1; i >= 0; --i) {
        dp[i][i] = 1;

        for(int j = i + 1; j < len; ++j) {
            if(s[i] == s[j]) {
                dp[i][j] = dp[i + 1][j - 1] + 2;
            }else {
                dp[i][j] = max(dp[i + 1][j], dp[i][j - 1]);
            }
        }          
    }
    return dp[0][len - 1];    
}

int main() {

    ios::sync_with_stdio(false);

    string s;
    int len;

    while(cin >> s) {
        len = LPS(s);
        cout << len << endl;
    }

    return 0; 
}
```



