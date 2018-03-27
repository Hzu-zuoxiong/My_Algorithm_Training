## cdoj 1017 王之困惑 {#cdoj-1017-王之困惑}

众所周知，绩点王（以下简称王）是集训队中的学神，因为他的绩点总是满的。  
一天晚上，王做了一个奇奇怪怪的梦。在这个奇奇怪怪的梦里，绩点是以一串01串表示的。而王则拥有两种神奇的魔法可以改变自己的绩点。  
魔法1：使用此魔法时，王可以去掉当前绩点的最左边的第一个数。  
魔法2：使用此魔法时，王可以在当前绩点的最右边增加一个数x。其中，若当前绩点的01串中，1的个数为奇数，那么x=1；若1的个数为偶数，那么x=0。  
假设王的绩点以AA串表示，王想得到的绩点以BB串表示。王想知道，能否通过使用以上两种魔法，使得自己的绩点变为BB。（魔法的使用次数不限）

Input  
第一行输入一个TT，表示测试数据组数。（T≤1000）（T≤1000）  
每一组测试数据包括两行。  
第一行包含一个01串，表示王的绩点A。  
第二行包含一个01串，表示王希望得到的绩点B。  
（01串的长度均不超过10001000）

Output  
每组测试数据的输出包含一行，如果能，则输出YES，否则，输出NO。

Sample Input  
2  
01011  
0110  
0011  
1110  
Sample Output  
YES  
NO

---

### 题解： {#题解}

设A串中’1’的个数为len1，设B串中’1’的个数为len2。  
当len1为偶数时，A串明显无法增加’1’的个数，则当len1 &gt;= len2 就能将够A串转换为B串。  
当len2为奇数时，此时A串’1’的个数最多为len1 + 1，则当len1 + 1 &gt;= len2 就能够将A串转换为B串。

---

### AC代码: {#ac代码}

```cpp
#include<iostream>
#include<cstdio>
#include<string>

using namespace std;

int cal(string str) {
    int len = str.length();
    int num = 0;
    for(int i = 0; i < len; ++i) {
        if(str[i] == '1') {
            num++;
        }
    }
    return num;
}

int main() {
    cin.sync_with_stdio(false);

    int n;
    cin >> n;
    for(int i = 0; i < n; ++i) {
        string a, b;
        cin >> a >> b;
        int len1 = cal(a);
        int len2 = cal(b);
        if(len1 & 1) {
            if(len1 + 1 >= len2) {
                cout << "YES" << endl;
            } else {
                cout << "NO" << endl;
            }
        } else {
            if(len1 >= len2) {
                cout << "YES" << endl;
            } else {
                cout << "NO" << endl;
            }
        }
    }
}
```



