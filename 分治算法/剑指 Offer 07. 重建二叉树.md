#### [剑指 Offer 07. 重建二叉树](https://leetcode.cn/problems/zhong-jian-er-cha-shu-lcof/)

输入某二叉树的前序遍历和中序遍历的结果，请构建该二叉树并返回其根节点。

假设输入的前序遍历和中序遍历的结果中都不含重复的数字。

 

示例 1:

![img](https://assets.leetcode.com/uploads/2021/02/19/tree.jpg)

```
Input: preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]
Output: [3,9,20,null,null,15,7]
```


示例 2:

```
Input: preorder = [-1], inorder = [-1]
Output: [-1]
```


限制：

```
0 <= 节点个数 <= 5000
```

注意：本题与主站 105 题重复：https://leetcode-cn.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/



题解

这题难就难在要搞清楚每次分治递归的边界是什么，分治本身不用做什么，但要会分治，重要前提是所有节点数字都不一样：
三个递归参数：root：在preorder中的根节点的index, left: 在inorder中子树的左边界id, right在inorder中子树的右边界id，然后要搞清楚在每次向左右子树递归的过程中递归参数的递推关系

```go
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func buildTree(preorder []int, inorder []int) *TreeNode {
    if len(preorder) == 0{
        return nil
    }
    inOrderMap := make(map[int]int)
    for id, val := range inorder{
        inOrderMap[val] = id
    }
    
    left := 0
    right := len(inorder)-1
    var recur func(root, left, right int) (node *TreeNode)
    recur = func(root, left, right int) (node *TreeNode){
        if left > right {
            return nil
        }
        rootNode := &TreeNode{
            Val : preorder[root],
        }
        i := inOrderMap[preorder[root]]
        rootNode.Left = recur(root+1, left, i-1)
        rootNode.Right = recur(i-left+root+1, i+1, right)
        return rootNode
    }
    res := recur(0, left, right)
    return res
}
```

