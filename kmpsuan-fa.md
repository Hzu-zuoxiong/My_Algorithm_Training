# KMP算法 {#kmp算法}

KMP算法在算法题中较为常见，是一种改进的字符串匹配算法。KMP算法的关键是利用匹配失败后的信息，尽量减少模式串与主串的匹配次数，以达到快速匹配的目的。时间复杂度为O（N+M）。

### 普通字符串匹配算法： {#普通字符串匹配算法：}

字符串匹配最普通的解法是从左到右遍历str的每一个字符，然后看如果以当前字符作为第一个字符出发是否匹配出match。普通解法的时间复杂度较高，从每个字符出发时，匹配的代价都可能是O（M），那么一共有N个字符，所以整体的时间复杂度为O（N×M）。

### KMP算法： {#kmp算法：}

* 生成match字符串的next数组，next\[ i \]的含义是
  **在match\[ 0 ... i-1 \]中，必须以match\[ i-1 \]结尾的后缀字串与必须以match\[ 0 \]开头的前缀字串相等的最大长度。**
  如何生成next数组，后面再详解。
* 假设从str\[i\]字符出发，匹配到j位置时发现与match中的字符不一致，也就是str\[ i... j-1 \]与match\[ 0...j-i \]这两个字符串匹配相等
  ![](https://hzu-zuoxiong.gitbooks.io/algorithm_training/content/assets/KMP图1.png)

因为已有next数组，则next\[ j-i \]表示match\[ 0...j-i-1 \]这一串字符串的前缀与后缀的最长匹配长度。假设前缀是下图中a区域，后缀是下图中的b区域，a区域的下一个字符为match\[ k \]。![](https://hzu-zuoxiong.gitbooks.io/algorithm_training/content/assets/KMP图2.png)

那么下次的匹配不再像普通解法那样退回到str\[ i+1\]重新开始，而是直接让str\[ j \]与match\[ k \]进行匹配检查，如下图：![](https://hzu-zuoxiong.gitbooks.io/algorithm_training/content/assets/import3.png)

在上图中，在str中要匹配的位置仍然是j，而不进行回退。接下来解释为什么这样做是正确的。

在下图中，在A字符与B字符时发生不匹配，所以 c 区域等于 b 区域，b 区域又与 a 区域相等，所以 c 区域和 a 区域不需要检查，必然相等。所以直接把字符C滑到字符A的位置开始检查即可。![](https://hzu-zuoxiong.gitbooks.io/algorithm_training/content/assets/KMP图4.png)

至于“不用检查，必然匹配不出”的区域为什么不需要检查。假设假设从这段区域的某一个位置能够匹配出match，则从这个位置到A这一段应该与match\[0\]开始的一段字符串相等，而这段字符串比 a 区域与 c 区域还要大，则说明找到了比match\[ 0...j-i-1 \]字符串的一个更大的前后缀匹配这与next\[i\]的含义相违背，所以这种情况绝不会发生。

匹配的全部过程参看代码：

```java
public int getIndexOf(String s, String m) {
        if(s == null || m == null m.length() < 1 || s.length() < m.length()) {
            return -1;
        }
        char[] ss = s.toCharArray();
        char[] ms = m.toCharArray();
        int si = 0;
        int mi = 0;
        int[] next = getNextArray(ms);
        while(si < ss.length && mi < ms.length) {
            if(ss[si] == ms[mi]) {
                si++;
                mi++;
            } else if(next[mi] == -1) {
                si++;
            } else {
                mi = next[mi];
            }
        }
        return mi == ms.length ? si - mi : -1;        
}
```

最后解释如何快速获得match字符串的next数组：

* 对于match\[ 0 \]，它之前没有字符，所以规定next\[ 0 \] 为-1；
* 对于match\[ 1 \]，它之前只有match\[ 0 \]，但next数组定义要求任何字串的前缀不能包含第一个字符，所以math\[ 1 \] = 0；
* 因为是从左到右求解next数组，所以在求解next\[ i \]时，next\[ 0...i-1 \]的值都已经求出，我们可以根据之前的值求出next\[ i \]。

假设match\[ i \]字符为A，math\[ i-1 \]字符为B，字符C为match\[ i-1 \]位置的最长前缀字串之后的字符。![](https://hzu-zuoxiong.gitbooks.io/algorithm_training/content/assets/KMP%E5%9B%BE5.png)

* 如果字符C与字符B相等，则next\[ i \] = next \[ i-1 \] + 1；
* 如果字符C与字符B不想等，就看字符C之前的最长前缀和后缀的匹配长度。如下图：

  ![](https://hzu-zuoxiong.gitbooks.io/algorithm_training/content/assets/KMP%E5%9B%BE6.png)

在上图中，N与M区域是字符C之前的字符串的最长匹配的前缀与后缀这是通过next\[ C \]的值确定的，当然两个区域是相等的，同理，M'与M区域也是相等的，字符D为N区域之后的一个字符，接下来比较字符D与字符B是否相等。

如果相等，A字符之前的字符串的最长前缀与后缀的匹配长度即可确定，即next\[ i \] = next\[ C \] + 1；

如果不等，则继续往前跳，跳的每一步都会有一个新字符与B进行比较，只要出现相等的情况，则next\[ i \]的值就能确定。

* 如果跳到最左位置（即match\[ 0 \]位置），此时nect\[ 0 \] = -1，说明match\[ i \]之前的字符串不存在前缀和后缀匹配的情况，则令next\[ i \] = 0。

求解next数组的具体过程参看下面代码：

```java
public int[] getNextArray(char[] ms) {
    if(ms.length == 1) {
        return new int[] {-1};
    }
    int[] next = new int[ms.length];
    next[0] = -1;
    next[1] = 1;
    int pos = 2;
    int cn = 0;
    while(pos < next.length) {
        if(ms[pos - 1] == ms[cn]) {
            next[pos++] = ++cn;
        } else if(cn > 0) {
            cn = next[cn];
        } else {
            next[pos++] = 0;
        }
    }
    return next;        
}
```

### 拓展： {#拓展：}

子树匹配问题：判断一棵树是否是另一棵树的子树

解法：将两棵树都分别序列化，空结点加上特殊字符，如‘ \# ’，在利用KMP算法进行判别。

例如：

![](https://hzu-zuoxiong.gitbooks.io/algorithm_training/content/assets/KMP%E5%9B%BE7.png)



