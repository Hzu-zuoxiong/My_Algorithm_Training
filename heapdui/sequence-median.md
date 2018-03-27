### Sequence Median {#sequence-median}

Given a sequence of N nonnegative integers. Let’s define the median of such sequence. If N is odd the median is the element with stands in the middle of the sequence after it is sorted. One may notice that in this case the median has position \( N+1\)/2 in sorted sequence if sequence elements are numbered starting with 1. If N is even then the median is the semi-sum of the two “middle” elements of sorted sequence. I.e. semi-sum of the elements in positions N/2 and \( N/2\)+1 of sorted sequence. But original sequence might be unsorted.  
Your task is to write program to find the median of given sequence.

Input  
The first line of input contains the only integer number N — the length of the sequence. Sequence itself follows in subsequent lines, one number in a line. The length of the sequence lies in the range from 1 to 250000. Each element of the sequence is a positive integer not greater than 2 31−1 inclusive.

Output  
You should print the value of the median with exactly one digit after decimal point.  
Example

input  
4  
3  
6  
4  
5  
output  
4.5

---

### 解题思路： {#解题思路}

题意为求某序列的中位数，所以只需要记录前N+1位数字并对其排序即可。该题可通过运用最大堆进行求解。

---

### AC代码： {#ac代码}

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

unsigned int a[125005];

int main() {

    unsigned int n, i, x, s1, s2;
    scanf("%d", &n);

    for(i = 0; i < n/2 + 1; i++) {
        scanf("%d", &a[i]);
    }
    make_heap(a, a+n/2+1);
    for(i = n/2 + 1; i < n; i++) {
        scanf("%d", &x);
        a[n/2 + 1] = x;
        push_heap(a, a+n/2 + 2);
        pop_heap(a, a+n/2 + 2);
    }

    if(n % 2) {
        printf("%.1lf\n", (double)a[0]);
    }else {
        s1 = a[0];
        pop_heap(a, a+n/2 + 1);
        s2 = a[0];
        double sum = s1 + s2;
        printf("%.1lf\n", sum / 2);
    }
}
```



