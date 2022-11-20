#### [剑指 Offer 55 - II. 平衡二叉树](https://leetcode.cn/problems/ping-heng-er-cha-shu-lcof/)

输入一棵二叉树的根节点，判断该树是不是平衡二叉树。如果某二叉树中任意节点的左右子树的深度相差不超过1，那么它就是一棵平衡二叉树。

 

示例 1:

给定二叉树 [3,9,20,null,null,15,7]

```
    3
   / \
  9  20
    /  \
   15   7
```

返回 true 。

示例 2:

给定二叉树 [1,2,2,3,3,null,null,4,4]

```
       1
      / \
     2   2
    / \
   3   3
  / \
 4   4
```

返回 false 。

 

限制：

0 <= 树的结点个数 <= 10000
注意：本题与主站 110 题相同：https://leetcode-cn.com/problems/balanced-binary-tree/



题解

这题需要一个辅助求深度的递归函数，然后还要在原来的函数上递归，注意递推方式

```go
func isBalanced(root *TreeNode) bool {
    if root == nil{
        return true
    }
    diff := dfs(root.Left) - dfs(root.Right)
    if diff <= 1 && diff >= -1{
        return isBalanced(root.Left)&&isBalanced(root.Right)
    }else{
        return false
    }
}

func dfs(node *TreeNode) int{
    if node == nil{
        return 0
    }
    return max(dfs(node.Left), dfs(node.Right)) + 1
}

func max(a, b int) int{
    if a > b{
        return a
    }else{
        return b
    }
}
```

