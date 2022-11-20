#### [剑指 Offer 55 - I. 二叉树的深度](https://leetcode.cn/problems/er-cha-shu-de-shen-du-lcof/)

输入一棵二叉树的根节点，求该树的深度。从根节点到叶节点依次经过的节点（含根、叶节点）形成树的一条路径，最长路径的长度为树的深度。

例如：

给定二叉树 [3,9,20,null,null,15,7]，

```
    3
   / \
  9  20
    /  \
   15   7
```

返回它的最大深度 3 。

 

提示：

节点总数 <= 10000
注意：本题与主站 104 题相同：https://leetcode-cn.com/problems/maximum-depth-of-binary-tree/



题解

有点遗憾，其实很简单，要领会思想：本质上是后序遍历，既然想到要递归，就要找到递推关系和终止条件：此树深度 = max(left, right) + 1, 终止条件是叶子结点返回深度0. 注意在原函数上递归就可以，不用再写个递归函数

```
func maxDepth(root *TreeNode) int {
    if root == nil{
        return 0
    }
    return max(maxDepth(root.Left), maxDepth(root.Right)) + 1
}

func max (a, b int) int{
    if a > b{
        return a
    }else{
        return b
    }
}
```

