## Largest Rectangle in a Histogram {#largest-rectangle-in-a-histogram}

题目链接：[http://acm.hdu.edu.cn/showproblem.php?pid=1506](http://acm.hdu.edu.cn/showproblem.php?pid=1506)

Problem Description  
A histogram is a polygon composed of a sequence of rectangles aligned at a common base line. The rectangles have equal widths but may have different heights. For example, the figure on the left shows the histogram that consists of rectangles with the heights 2, 1, 4, 5, 1, 3, 3, measured in units where 1 is the width of the rectangles:

![](http://img.blog.csdn.net/20171029144507998)

Usually, histograms are used to represent discrete distributions, e.g., the frequencies of characters in texts. Note that the order of the rectangles, i.e., their heights, is important. Calculate the area of the largest rectangle in a histogram that is aligned at the common base line, too. The figure on the right shows the largest aligned rectangle for the depicted histogram.

Input  
The input contains several test cases. Each test case describes a histogram and starts with an integer n, denoting the number of rectangles it is composed of. You may assume that 1 &lt;= n &lt;= 100000. Then follow n integers h1, …, hn, where 0 &lt;= hi &lt;= 1000000000. These numbers denote the heights of the rectangles of the histogram in left-to-right order. The width of each rectangle is 1. A zero follows the input for the last test case.

Output  
For each test case output on a single line the area of the largest rectangle in the specified histogram. Remember that this rectangle must be aligned at the common base line.

Sample Input  
7 2 1 4 5 1 3 3  
4 1000 1000 1000 1000  
0

Sample Output  
8  
4000

---

### 解题思路： {#解题思路}

运用动态规划的思路求解（即DP），设置left和right数组，记录每一个柱子最左边和最右边的比自己高的主子的位置，则\(r\[i\] - l\[i\] + 1\) \* a\[i\] 的最大值为答案。

1. 首先初始化left和right数组，left\[1\]=1,right\[n\]=n
2. 记录left数组（left数组为从第i个开始，记录可以推进的最左边的柱子的位置），从第i+1个开始，若这个数比上一个数小，则记录上一个数的值，直至到遇到比这个数大的值为止，记录其下标。
3. 记录right数组，与left同理，从n-1位置开始逆推，记录其最右数值。
4. 求\(r\[i\] - l\[i\] +0 1\) \* a\[i\] 的最大值即可。

---

### AC代码： {#ac代码：}

```cpp
#include<iostream>
#include<algorithm>
#include<cstdio>
#include<string>
#include<cstring>
#include<queue>
#include<stack>
#include<vector>

using namespace std;

long long a[100005]; 
long long l[100005];
long long r[100005];

int main() {
    int i, n, t;
    long long max;

    while(scanf("%d", &n) && n) {
        for(i = 1; i <= n; i++) {
            scanf("%I64d", &a[i]);
        }
        l[1] = 1;
        r[n] = n;
        for(i = 2; i <= n; ++i) {
            t = i;
            while(t > 1 && a[i] <= a[t - 1]) {
                t = l[t - 1];
            }
            l[i] = t;
        }
        for(i = n - 1; i >= 1; --i) {
            t = i;
            while(t < n && a[i] <= a[t + 1]) {
                t = r[t + 1];
            }
            r[i] = t;
        }
        max = 0;
        for(i = 1; i <= n; i++) {
            if((r[i] - l[i] + 1) * a[i] > max) {
                max= (r[i] - l[i] + 1) * a[i];
            }
        }
        printf("%I64d\n", max);
    }
}
```



