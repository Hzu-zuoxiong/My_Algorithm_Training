## L1-048. 矩阵A乘以B {#l1-048-矩阵a乘以b}

[L1-048. 矩阵A乘以B](https://www.patest.cn/contests/gplt/L1-048)

给定两个矩阵A和B，要求你计算它们的乘积矩阵AB。需要注意的是，只有规模匹配的矩阵才可以相乘。即若A有Ra行、Ca列，B有Rb行、Cb列，则只有Ca与Rb相等时，两个矩阵才能相乘。

输入格式：  
输入先后给出两个矩阵A和B。对于每个矩阵，首先在一行中给出其行数R和列数C，随后R行，每行给出C个整数，以1个空格分隔，且行首尾没有多余的空格。输入保证两个矩阵的R和C都是正数，并且所有整数的绝对值不超过100。

输出格式：  
若输入的两个矩阵的规模是匹配的，则按照输入的格式输出乘积矩阵AB，否则输出“Error: Ca != Rb”，其中Ca是A的列数，Rb是B的行数。

输入样例1：  
2 3  
1 2 3  
4 5 6  
3 4  
7 8 9 0  
-1 -2 -3 -4  
5 6 7 8

输出样例1：  
2 4  
20 22 24 16  
53 58 63 28

输入样例2：  
3 2  
38 26  
43 -5  
0 17  
3 2  
-11 57  
99 68  
81 72

输出样例2：  
Error: 2 != 3

---

## 题解： {#题解}

简单的矩阵运算，行×列。

---

### AC代码： {#ac代码：}

```cpp
#include<iostream>
#include<cstdio>
#include<string>
#include<cstring>
#include<cfloat>
#include<queue>
#include<stack>
#include<vector>

using namespace std;

int rect1[100][100];
int rect2[100][100];

int main() {

    int r1, c1;
    cin >> r1 >> c1;
    for(int i = 0; i < r1; i++) {
        for(int j = 0; j < c1; j++) {
            cin >> rect1[i][j];
        }
    }
    int r2, c2;
    cin >> r2 >> c2;
    for(int i = 0; i < r2; i++) {
        for(int j = 0; j < c2; j++) {
            cin >> rect2[i][j];
        }
    }

    if(c1 != r2) {
        cout << "Error: " << c1 << " != " << r2 << endl;
    }else {
        cout << r1 << " " << c2 << endl;
        for(int i = 0; i < r1; i++) {
            for(int j = 0; j < c2; j++) {
                int sum = 0;
                for(int k = 0; k < c1; k++){
                    sum += rect1[i][k] * rect2[k][j];           
                }
                if(j < c2 - 1) {
                    cout << sum << " ";
                }else {
                    cout << sum << endl;
                }
            }
        }
    }
}
```



