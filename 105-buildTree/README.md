## 题目分析

给出树的先序遍历和中序遍历，要求还原整棵树。

## 题解思路

非常经典的树上递归题。

>  回顾一下先序遍历和中序遍历的顺序。先序遍历的递归定义是`根-左子树-右子树`，中序遍历的递归定义是`左子树-根-右子树`。

熟悉了这些以后就可以递归还原全树。传递四个参数：`l1, r1, l2, r2`，表示现在正在处理先序遍历的`[l1, r1]`和中序遍历的`[l2, r2]`。
根据定义先序遍历的`[l1]`这个节点是根节点，我们找到这个根节点在中序遍历`[l2, r2]`中的位置mid，显然此时也就知道了这个根左右子树的size（mid左边的那一段就是左子树size，右边那一段就是右子树size），于是我们成功将先序遍历序列划分成了`[root(l1)],[左子树],[右子树]`，将中序遍历序列划分成了`[左子树],[root(mid)],[右子树]`，现在问题就变成了：已经找到了root，构造它的左子树和右子树，由于我们已经知道了左右子树分别的下标边界，递归构造即可。

## 复杂度分析

递归构造后每个节点会进入一次，这里的复杂度是`O(n)`，进入每个节点中的主要开销在于*从中序遍历中寻找某一个值的位置*，可以直接循环从中序遍历中查找，复杂度是`O(n)`，总时间复杂度是`O(n^2)`；更加快速的做法是预处理把所有值和下标存入一个map映射中，需要查询时直接查找映射即可，这个做法中预处理复杂度`O(n*lgn)`，查找复杂度`O(lgn)`，递归到节点查找一次，总时间复杂度是`O(n*lgn)`。