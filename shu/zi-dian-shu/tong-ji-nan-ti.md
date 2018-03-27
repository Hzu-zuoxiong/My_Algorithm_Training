## 统计难题 {#统计难题}

Ignatius最近遇到一个难题,老师交给他很多单词\(只有小写字母组成,不会有重复的单词出现\),现在老师要他统计出以某个字符串为前缀的单词数量\(单词本身也是自己的前缀\).

Input

输入数据的第一部分是一张单词表,每行一个单词,单词的长度不超过10,它们代表的是老师交给Ignatius统计的单词,一个空行代表单词表的结束.第二部分是一连串的提问,每行一个提问,每个提问都是一个字符串.

注意:本题只有一组测试数据,处理到文件结束.

Output

对于每个提问,给出以该字符串为前缀的单词的数量.

Sample Input

```
banana
band
bee
absolute
acm

ba
b
band
abc

```

Sample Output

```
2
3
1
0

```

---

## 解题思路：

直接利用字典树即可求解。

---

## AC代码：

```cpp
#include<iostream>
#include<cstdio>
#include<cstdlib>
#include<string>
#include<cstring>

using namespace std;

const int MAX = 26;

struct Trie {
    int v;
    Trie* next[MAX];
};

Trie root;

void creatTrie(char *str) {
    int len = strlen(str);
    Trie* p = &root, *q;
    for(int i = 0; i < len; ++i) {
        int id = str[i] - 'a';
        if(p->next[id] == NULL) {
            q = (Trie*)malloc(sizeof(root));
            q->v = 1;
            for(int j = 0; j < MAX; ++j) {
                q->next[j] = NULL;
            }
            p->next[id] = q;
            p = p->next[id];
        } else {
            p->next[id]->v++;
            p = p->next[id];
        }                
    }    
}

int findTrie(char *str) {
    int len = strlen(str);
    Trie* p = &root;
    for(int i = 0; i < len; ++i) {
        int id = str[i] - 'a';
        p = p->next[id];
        if(p == NULL) {
            return 0;
        }
    }
    return p->v;
}

int main() {
    char str[15];
    for(int i = 0; i < MAX; ++i) {
        root.next[i] = NULL;
    }

    while(gets(str) && str[0] != '\0') {
        creatTrie(str);
    }
    while(cin >> str) {
        cout << findTrie(str) << endl;
    }
}
```



