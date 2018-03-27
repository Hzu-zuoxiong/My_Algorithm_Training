## 完全背包

在n种物品中选取若干件（同一种物品可多次选取）放在空间为v的背包里，每种物品的体积为c1，c2，…，cn，与之相对应的价值为w1,w2，…，wn.求解怎么装物品可使背包里物品总价值最大

完全背包问题与01背包问题的区别：完全背包每一件物品的数量都有无限个，而01背包每件物品数量只有1个。

f\[i\]\[v\]表示前i种物品恰放入一个容量为v的背包的最大价值，那我们应该用k表示当前容量下可以装第i种物品的件数，那么k的范围应该是0≤k≤v/c\[i\]，其状态转移方程：f\[i\]\[j\] = max{f\[i-1\]\[v\],f\[i-1\]\[v - k \* c\[i\]\] + k \* w\[i\]}\(0&lt;=k\*c\[i\]&lt;=v\)。

代码：

```cpp
for (int i=1;i<=n;++i) {　
     for (int j=v;j>=0;--j) {
          if(c[i]<=j)//如果当前物品可以放入当前空间的背包
               f[i][j]=max(f[i-1][j],f[i-1][j-c[i]]+w[i]);
          else 
               f[i][j]=f[i-1][j];//如果当前物品放不进去，那么继承前i个物品在当前空间大小时的价值
　　　}
}

```

### 举例： {#举例：}

有2件物品和一个容量为6的背包，物件的重量和价值如下：

![](https://hzu-zuoxiong.gitbooks.io/algorithm_training/content/assets/%E5%AE%8C%E5%85%A8%E8%83%8C%E5%8C%850.png)

表格：

![](https://hzu-zuoxiong.gitbooks.io/algorithm_training/content/assets/%E5%AE%8C%E5%85%A8%E8%83%8C%E5%8C%851.png)

### 优化： {#优化：}

f\[i\]\[j\]表示出在前i种物品中选取若干件物品放入容量为j的背包所得的最大价值，则对于第i件物品有放或不放两种情况，而放的情况里又分为放1件、2件、......v/c\[i\]件

第一种情况，不放入：f\[i\]\[j\]=f\[i-1\]\[j\]；

第二种情况，放入：那么背包中应该出现至少一件第i种物品，所以f\[i\]\[j\]中至少应该出现一件第i种物品,即f\[i\]\[j\]=f\[i\]\[j-c\[i\]\]+w\[i\]；（注意：01背包的是f\[i\]\[j\]=f\[i-1\]\[j-c\[i\]\]+w\[i\]，即只考虑加入一件当前物品的情况下）。

所以，其状态转移方程为：f\[i\]\[j\]=max\(f\[i-1\]\[j\],f\[i\]\[j-c\[i\]\]+w\[i\]\)

代码：

```cpp
for(int i = 0 ; i < n ; i ++)  { 
    for(int j = 1 ; j <= v ; j++)  {
        if(c[i]<=j)
            f[i][j] = max(f[i-1][j],f[i][j-c[i]]+w[i]); 
        else
            f[i][j]=f[i-1][j];
    }
}
```

### 继续优化：用一维数组代替二维数组 {#继续优化：用一维数组代替二维数组}

f\[j\]表示当前可用体积j的价值，我们可以得到和01背包一样的递推式：f\[j\] = max\(f\[j\],f\[j-c\[i\]\]+w\[i\]\)

代码：

```cpp
for(int i = 0 ; i < n ; i ++) { 
    for(int j = c[i] ; j <= v ; j++) {
        if(c[i]<j)
            f[j] = max(f[j],f[j-c[i]]+w[i]);
        else
            f[j]=f[j];
    }    
}
```

[  
](https://hzu-zuoxiong.gitbooks.io/algorithm_training/content/zui-chang-hui-wen-zi-xu-lie.html)

