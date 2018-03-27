## 剪花布条 {#problem-title}

一块花布条，里面有些图案，另有一块直接可用的小饰条，里面也有一些图案。对于给定的花布条和小饰条，计算一下能从花布条中尽可能剪出几块小饰条来呢？

Input

输入中含有一些数据，分别是成对出现的花布条和小饰条，其布条都是用可见ASCII字符表示的，可见的ASCII字符有多少个，布条的花纹也有多少种花样。花纹条和小饰条不会超过1000个字符长。如果遇见\#字符，则不再进行工作。

Output

输出能从花纹布中剪出的最多小饰条个数，如果一块都没有，那就老老实实输出0，每个结果之间应换行。

Sample Input

```
abcde a3
aaaaaa  aa
#

```

Sample Output

```
0
3

```

---

## 解题思路： {#解题思路：}

1. 用普通的字符串匹配方法，逐步比对。
2. 利用C++的string函数方法，直接调用方法剪短字符串进行求解。
3. 利用KMP算法进行求解。

---

### 普通解法： {#普通解法：}

```cpp
#include<iostream>
#include<string>
#include<queue>
#include<cstring>
#include<stack>

using namespace std;

string str1;
string str2;

int main() {
    cin.sync_with_stdio(false);

    int num = 0;
    while(cin >> str1) {
        num = 0;
        if(str1[0] == '#') {
            break;
        }

        cin >> str2;
        int len1 = str1.length();
        int len2 = str2.length();

        int k;
        for(int i = 0; i < len1 - len2 + 1; i++) {
            k = i;
            for(int j = 0; j < len2;) {
                if(str1[k] == str2[j]) {
                    k++;
                    j++;
                    if(j == len2) {
                        num++;
                        j = 0;
                        i = i + len2 - 1;
                        break;
                    }
                } else {
                    j = 0;
                    break;
                }
            }
        }
        cout << num << endl;
    }
}
```

### C++函数方法: {#c函数方法}

```cpp
#include<iostream>
#include<string>
#include<queue>
#include<cstring>
#include<stack>

using namespace std;

string str1;
string str2;
int num;

int main() {
    cin.sync_with_stdio(false);

    while(cin >> str1) {
        num = 0;
        if(str1[0] == '#') {
            break;
        }
        cin >> str2;

        int len2 = str2.length();

        //string::find这类型的函数，返回值类型都是string::size_type, 而string::size_type其实是一种unsigned int类型。
        //find的结果记录匹配的位置，或者返回一个名为string::npos 的特殊值，说明查找没有匹配。
        //string 类将 npos 定义为保证大于任何有效下标的值。string::npos的值是无符号型类型的，其值是(unsigned int)(-1)，
        //也就是4294967295
        while(str1.find(str2) != string::npos) {
            str1.erase(str1.find(str2), len2);
            num++;
        }
        cout << num << endl;        
    }

}
```

### KMP解法： {#kmp解法：}

```cpp
#include<iostream>
#include<string>
#include<queue>
#include<cstring>
#include<stack>

using namespace std;

string str1;
string str2;
int Snext[1005];
int len1, len2;
int num;

void getNext() {
    Snext[0] = -1;
    Snext[1] = 0;
    int pos = 2;
    int cn = 0;
    while(pos < len2) {
        if(str2[pos - 1] == str2[cn]) {
            Snext[pos++] = ++cn;
        } else if(cn > 0) {
            cn = Snext[cn];
        } else {
            Snext[pos++] = 0;
        }
    }
}

void KMP() {
    int si = 0;
    int mi = 0;
    while(si < len1) {
        if(str1[si] == str2[mi]) {
            si++;
            mi++;
            if(mi == len2) {
                num++;
                mi = 0;
            }
        } else if(Snext[mi] == -1) {
            si++;
        } else {
            mi = Snext[mi];
        }
    }
} 

int main() {
    cin.sync_with_stdio(false);

    while(cin >> str1) {
        num = 0;
        if(str1[0] == '#') {
            break;
        }

        cin >> str2;
        len1 = str1.length();
        len2 = str2.length();

        getNext();
        KMP();
        cout << num << endl;
    }
}
```





