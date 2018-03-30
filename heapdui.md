# heap堆 {#heap堆}

STL中的堆默认是最大堆，想用最小堆的话，必须在push\_heap， pop\_heap，make\_heap等每一个函数后面加第三个参数greater&lt;int&gt;\(\)，括号不能省略。

---

## heap堆的方法 {#heap堆的方法}

1. make\_heap\(\_First, \_Last\)：使序列变成堆。默认是建立最大堆的。
2. push\_heap\(\_First, \_Last\)：新添加一个元素在末尾，然后重新调整堆序。该算法必须是在一个已经满足堆序的条件下，添加元素。
3. pop\_heap\(\_First, \_Last\)：与push\_heap类似，参数一样。把堆顶元素取出来，重新调整堆序。
4. sort\_heap\(\_First, \_Last\)：每次pop\_heap可以获得堆中最大的元素，那么我们持续对整个heap做pop\_heap操作，每次将操作的范围向前缩减一个元素。当整个程序执行完毕后，我们得到一个非降的序列。



