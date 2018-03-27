# L2-020. 功夫传人 {#l2-020-功夫传人}

一门武功能否传承久远并被发扬光大，是要看缘分的。一般来说，师傅传授给徒弟的武功总要打个折扣，于是越往后传，弟子们的功夫就越弱…… 直到某一支的某一代突然出现一个天分特别高的弟子（或者是吃到了灵丹、挖到了特别的秘笈），会将功夫的威力一下子放大N倍 —— 我们称这种弟子为“得道者”。

这里我们来考察某一位祖师爷门下的徒子徒孙家谱：假设家谱中的每个人只有1位师傅（除了祖师爷没有师傅）；每位师傅可以带很多徒弟；并且假设辈分严格有序，即祖师爷这门武功的每个第i代传人只能在第i-1代传人中拜1个师傅。我们假设已知祖师爷的功力值为Z，每向下传承一代，就会减弱r%，除非某一代弟子得道。现给出师门谱系关系，要求你算出所有得道者的功力总值。

**输入格式：**

输入在第一行给出3个正整数，分别是：N（&lt;=105）——整个师门的总人数（于是每个人从0到N-1编号，祖师爷的编号为0）；Z——祖师爷的功力值（不一定是整数，但起码是正数）；r ——每传一代功夫所打的折扣百分比值（不超过100的正数）。接下来有N行，第i行（i=0, ..., N-1）描述编号为i的人所传的徒弟，格式为：

KiID\[1\] ID\[2\] ... ID\[Ki\]

其中Ki是徒弟的个数，后面跟的是各位徒弟的编号，数字间以空格间隔。Ki为零表示这是一位得道者，这时后面跟的一个数字表示其武功被放大的倍数。

**输出格式：**

在一行中输出所有得道者的功力总值，只保留其整数部分。题目保证输入和正确的输出都不超过1010。

**输入样例：**

```
10 18.0 1.00
3 2 3 5
1 9
1 4
1 7
0 7
2 6 1
1 8
0 9
0 4
0 3

```

**输出样例：**

```
404

```

---

## 解题思路： {#解题思路：}

用vector容器存储师徒关系，然后使用dfs搜索每个得道者有多少层师徒关系后进行计算就可以了。

---

## AC代码： {#ac代码：}

```cpp
#include<iostream>
#include<cstdio>
#include<set>
#include<string>
#include<stack>
#include<algorithm>
#include<vector>
#include<cmath>

using namespace std;

vector<int> vec[100050];
double z, r;
int n;
int a[100050];

double dfs(int x, int t) {
    double sum = 0;

    if(!vec[x].size()) {
        sum += a[x] * z * pow(1 - r/100.0, t);
    } else {
        for(int i = 0; i < vec[x].size(); ++i) {
            sum += dfs(vec[x][i], t + 1);
        }
    }
    return sum;
}

int main() {

    cin >> n >> z >> r;

    for(int i = 0; i < n; ++i) {
        int k;
        cin >> k;
        if(!k) {
            cin >> a[i];
        }else {
            for(int j = 0; j < k; ++j) {
                int num;
                cin >> num;
                vec[i].push_back(num);
            }
        }
    }

    cout << (long long)dfs(0, 0) << endl;

}
```


