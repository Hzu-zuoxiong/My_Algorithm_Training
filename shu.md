# 树 {#树}

## 树的定义： {#树的定义：}

树是由根结点和若干颗子树构成的。树是由一个集合以及在该集合上定义的一种关系构成的。集合中的元素称为树的结点，所定义的关系称为父子关系。父子关系在树的结点之间建立了一个层次结构。在这种层次结构中有一个结点具有特殊的地位，这个结点称为该树的根结点，或称为树根。

单个结点是一棵树，树根就是该结点本身。

空集合也是树，称为空树。空树中没有结点。

![](https://hzu-zuoxiong.gitbooks.io/algorithm_training/content/assets/%E6%A0%911.png)

## 树的特点： {#树的特点：}

1. 每个节点有零个或多个节点；
2. 没有父节点的节点称之为根节点；
3. 每个非根节点有且只有一个父节点；
4. 除根节点外，每个子节点可以分为多个不相交的树。

## 树的相关术语： {#树的相关术语：}

* 节点的度：节点的子树个数；
* 树的度：树的所有节点中最大的度数；
* 叶节点：度为0的节点；
* 父节点：有子树的节点是其子树的根节点的父节点；
* 子节点/孩子节点：若A节点是B节点的父节点，则B节点是A节点的子节点；
* 兄弟节点：具有同一个父节点的各个节点彼此是兄弟节点；
* 路径和路径长度：从节点$$n1$$到$$nk$$的路径为一个节点序列$$n1,n2, ... ,nk$$。$$ni$$是$$ni+1$$的父节点。路径所包含边的个数为路径长度；
* 祖先节点：沿树根到某一结点路径上的所有节点都是这些节点的祖先节点；
* 子孙节点：某一节点的子树中的所有节点是这个节点的子孙节点；
* 节点的层次：规定根节点在1曾，其他任一节点的层次是其父节点的层次加1；
* 树的深度：树中所有节点中的最大层次是这棵树的深度。

## 树的种类： {#树的种类：}

* 无序树：树中任意节点的子结点之间没有顺序关系，这种树称为无序树,也称为自由树；

* 有序树：树中任意节点的子结点之间有顺序关系，这种树称为有序树；

* 二叉树：每个节点最多含有两个子树的树称为二叉树；

* 完全二叉树：叶节点只能出现在最下层和次下层，并且最下面一层的结点都集中在该层最左边的若干位置的二叉树

* 满二叉树：一个二叉树，如果每一个层的结点数都达到最大值，则这个二叉树就是满二叉树。

* 哈夫曼树：带权路径最短的二叉树称为哈夫曼树或最优二叉树；

## 树的遍历： {#树的遍历：}

* 前序遍历：

```cpp
void PreOrderTree(Node node){  
    if (node != NULL) {  
        printf("%d\n",node->data);  
        PreOrderTree(node->lchild);  
        PreOrderTree(node->rchild);  
    }  
}
```

* 中序遍历：

```cpp
void InOrderTree(Node node){  
    if (node != NULL) {  
        InOrderTree(node->lchild);  
        printf("%d\n",node->data);  
        InOrderTree(node->rchild);  
    }  
}
```

* 后序遍历：

```cpp
void postOrderTree(Node node){  
    if (node != NULL) {  
        postOrderTree(node->lchild);  
        postOrderTree(node->rchild);  
        printf("%d\n",node->data);  
    }  
}
```











