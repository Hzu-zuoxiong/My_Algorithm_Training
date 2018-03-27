## Tree Recovery {#tree-recovery}

Little Valentine liked playing with binary trees very much. Her favorite game was constructing randomly looking binary trees with capital letters in the nodes.

This is an example of one of her creations:

```
                                               D

                                              / \

                                             /   \

                                            B     E

                                           / \     \

                                          /   \     \

                                         A     C     G

                                                    /

                                                   /

                                                  F

```

To record her trees for future generations, she wrote down two strings for each tree: a preorder traversal \(root, left subtree, right subtree\) and an inorder traversal \(left subtree, root, right subtree\). For the tree drawn above the preorder traversal is DBACEGF and the inorder traversal is ABCDEFG.

She thought that such a pair of strings would give enough information to reconstruct the tree later \(but she never tried it\).

Now, years later, looking again at the strings, she realized that reconstructing the trees was indeed possible, but only because she never had used the same letter twice in the same tree.

However, doing the reconstruction by hand, soon turned out to be tedious.

So now she asks you to write a program that does the job for her!

Input

The input will contain one or more test cases.

Each test case consists of one line containing two strings preord and inord, representing the preorder traversal and inorder traversal of a binary tree. Both strings consist of unique capital letters. \(Thus they are not longer than 26 characters.\)

Input is terminated by end of file.

Output

For each test case, recover Valentine's binary tree and print one line containing the tree's postorder traversal \(left subtree, right subtree, root\).

Sample Input

```
DBACEGF ABCDEFG
BCAD CBAD

```

Sample Output

```
ACBFGED
CDAB

```

---

## 解题思路： {#解题思路：}

题意：已知树的前序和中序遍历，求树的后序遍历。

题目很长，总结起来却很短，知道了题意，本题就很好解。

---

## AC代码： {#ac代码：}

```cpp
#include<iostream>
#include<string>
#include<queue>
#include<cstring>
#include<stack>

using namespace std;

string pre;
string mid;
int n;

void make_tree(int i, int j) {
    if(i > j) {
        return;
    }
    n++;
    int k;
    for(k = i; k <= j; k++) {
        if(pre[n] == mid[k]) {
            break;
        }
    }
    make_tree(i, k - 1);
    make_tree(k + 1, j);
    cout << mid[k];
}

int main() {
    cin.sync_with_stdio(false);

    while(cin >> pre >> mid) {
        n = -1;
        make_tree(0, pre.length() - 1);
        cout << endl;
    }
}
```



