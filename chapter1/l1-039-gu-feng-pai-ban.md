## L1-039. 古风排版 {#l1-039-古风排版}

题目链接：[L1-039. 古风排版](https://www.patest.cn/contests/gplt/L1-039)

中国的古人写文字，是从右向左竖向排版的。本题就请你编写程序，把一段文字按古风排版。  
输入格式：  
输入在第一行给出一个正整数N（&lt;100），是每一列的字符数。第二行给出一个长度不超过1000的非空字符串，以回车结束。  
输出格式：  
按古风格式排版给定的字符串，每列N个字符（除了最后一列可能不足N个）

输入样例：  
4  
This is a test case  
输出样例：  
asa T  
st ih  
e tsi  
ce s

---

### 题解： {#题解}

这道题的规律并不难发现，只要算出其列数col的值，从最后一列开始，row从0到n依次输出，直到输出完第0列即可。此题还有两点需要注意：

1. 输入一整行字符串，包括空格，需使用getline\(cin, str\);
2. 创建了二维数组之后，需要将数组全初始化为’ ’，不然会出现格式不正确的情况。

---

### AC代码： {#ac代码：}

```cpp
#include<iostream>
#include<cstdio>
#include<set>
#include<string>
#include<stack>
#include<vector>

using namespace std;

char s[105][105]; 
string str;
int n;

int main() {
  cin >> n;
  getchar();
  getline(cin, str);
  int col = (str.length() - 1) / n + 1;
  vector<vector<char> > v(n, vector<char>(col, ' '));
  int index = 0;

  for(int i = 0; i < n; i++) {
    for(int j = 0; j < col; j++) {
      s[i][j] = ' ';
    }
  }

  for(int j = col - 1; j >= 0; j--) {
    for(int i = 0; i < n; i++) {
      if(index < str.length()) {
        v[i][j] = str[index++];
      }

    }
  }

  for(int i = 0; i < n; i++) {
    for(int j = 0; j < col; j++) {
      cout << v[i][j];
    }
    cout << endl;
  }

}
```



