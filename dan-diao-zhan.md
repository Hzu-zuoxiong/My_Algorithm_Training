## Bad Hair Day {#bad-hair-day}

Some of Farmer John’s N cows \(1 ≤ N ≤ 80,000\) are having a bad hair day! Since each cow is self-conscious about her messy hairstyle, FJ wants to count the number of other cows that can see the top of other cows’ heads.

Each cow i has a specified height hi \(1 ≤ hi ≤ 1,000,000,000\) and is standing in a line of cows all facing east \(to the right in our diagrams\). Therefore, cow i can see the tops of the heads of cows in front of her \(namely cows i+1, i+2, and so on\), for as long as these cows are strictly shorter than cow i.

Consider this example:  
=  
= =  
= - = Cows facing right –&gt;  
= = =  
= - = = =  
= = = = = =  
1 2 3 4 5 6  
Cow\#1 can see the hairstyle of cows \#2, 3, 4  
Cow\#2 can see no cow’s hairstyle  
Cow\#3 can see the hairstyle of cow \#4  
Cow\#4 can see no cow’s hairstyle  
Cow\#5 can see the hairstyle of cow 6  
Cow\#6 can see no cows at all!

Let ci denote the number of cows whose hairstyle is visible from cow i; please compute the sum of c1 through cN.For this example, the desired is answer 3 + 0 + 1 + 0 + 1 + 0 = 5.

Input  
Line 1: The number of cows, N.  
Lines 2..N+1: Line i+1 contains a single integer that is the height of cow i.  
Output  
Line 1: A single integer that is the sum of c 1 through cN.

Sample Input  
6  
10  
3  
7  
4  
12  
2  
Sample Output  
5

---

### 解题思路 {#解题思路}

题意：站着一排牛，牛从左往右看，只能看到比自己小的牛，计算每头牛能看到前面牛的数量的总和。

思路：题目要求每头牛能看到前方牛的数量之和，转换角度可为，求每头牛被其他牛看到的数量之和。此题可通过运用单调栈来计算，每加入一头牛的时候，把栈中比该牛小的元素删除，则栈中牛都能看到这头牛，及栈中元素的个数为能看到这头牛的个数，将其累加起来，再将这头牛加入栈中，对单调栈进行维护，可知栈底到栈顶中元素总是单调递减的。  
**PS：**题目数字较大，可能会超int，故使用long long。

---

### 代码： {#代码}

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

stack<int> st;

int main() {

    long long sum = 0;
    int n;
    cin >> n;
    int h;
    cin >> h;
    st.push(h);
    for(int i = 1; i < n; i++) {
        cin >> h;
        while(!st.empty() && h >= st.top()) {
            st.pop();
        }
        sum += st.size();
        st.push(h);
    }

    cout << sum << endl;
}
```



