## 2n皇后问题 {#2n皇后问题}

问题描述

　　给定一个n\*n的棋盘，棋盘中有一些位置不能放皇后。现在要向棋盘中放入n个黑皇后和n个白皇后，使任意的两个黑皇后都不在同一行、同一列或同一条对角线上，任意的两个白皇后都不在同一行、同一列或同一条对角线上。问总共有多少种放法？n小于等于8。

输入格式

　　输入的第一行为一个整数n，表示棋盘的大小。

　　接下来n行，每行n个0或1的整数，如果一个整数为1，表示对应的位置可以放皇后，如果一个整数为0，表示对应的位置不可以放皇后。

输出格式

　　输出一个整数，表示总共有多少种放法。

样例输入

4

1 1 1 1

1 1 1 1

1 1 1 1

1 1 1 1

样例输出

2

样例输入

4

1 0 1 1

1 1 1 1

1 1 1 1

1 1 1 1

样例输出

0

---

## 解题思路：

经典八皇后问题的变形，核心算法：回溯。

采用先放置黑皇后，再放置白皇后。放置白皇后时要注意不要与黑皇后位置产生冲突。

---

## AC代码：

```cpp
#include<iostream>
#include<string>
#include<queue>
#include<cstring>
#include<stack>
#include<cmath>
#include<algorithm>

using namespace std;

const int N = 100;
int wq[N];          //白皇后放置的位置 
int bq[N];            //黑皇后放置的位置 
int cb[N][N];        //棋盘 
int num;            //皇后数目 
int ans;            //不同放置的方案数 

//白皇后放置 
int wqueen(int pos) {
    //放置之前，判断与之前已放入的皇后位置是否冲突 
    for(int i = 0; i < pos - 1; ++i) {
        int judge =  wq[i] - wq[pos - 1];
        //判断同列或同对角线 
        if(0 == judge || judge == pos - 1 - i || -judge == pos - 1 -i) {
            return 0;
        }        
    }

    if(pos == num) {
        ans++;
        return 0;
    }

    //从第0列开始测试放入 
    for(int i = 0; i < num; ++i) {
        //棋盘可以放置皇后且不与黑皇后冲突 
        if(i != bq[pos] && cb[pos][i]) {
            wq[pos] = i;
            wqueen(pos + 1);
        }
    }    

}

//黑皇后放置
int bqueen(int pos) {

    //放置之前，判断与之前已放入的皇后位置是否冲突 
    for(int i = 0; i < pos - 1; ++i) {
        int judge =  bq[i] - bq[pos - 1];
        //判断同列或同对角线 
        if(0 == judge || judge == pos - 1 - i || -judge == pos - 1 -i) {
            return 0;
        }        
    }

    if(pos == num) {
        wqueen(0);
        return 0;
    }

    //从第0列开始测试放入 
    for(int i = 0; i < num; ++i) {
        //棋盘可以放置皇后
        if(cb[pos][i]) {
            bq[pos] = i;
            bqueen(pos + 1);
        }
    }    
}

int main() {
    ios::sync_with_stdio(false);

    cin >> num;
    for(int i = 0; i < num; ++i) {
        for(int j = 0; j < num; ++j) {
            cin >> cb[i][j];
        }
    }

    bqueen(0);

    cout << ans << endl;        
}
```



