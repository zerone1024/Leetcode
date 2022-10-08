#### [剑指 Offer 27. 二叉树的镜像](https://leetcode.cn/problems/er-cha-shu-de-jing-xiang-lcof/)

请完成一个函数，输入一个二叉树，该函数输出它的镜像。

例如输入：

```
	 4
   /   \
  2     7
 / \   / \
1   3 6   9
```

镜像输出：

```
	 4
   /   \
  7     2
 / \   / \
9   6 3   1
```

 

示例 1：

```
输入：root = [4,2,7,1,3,6,9]
输出：[4,7,2,9,6,3,1]
```


限制：

```
0 <= 节点个数 <= 1000
```

注意：本题与主站 226 题相同：https://leetcode-cn.com/problems/invert-binary-tree/



题解：

完美ac，注意判断下左子树和右子树是否为空

```go
func mirrorTree(root *TreeNode) *TreeNode {
    if root == nil{
        return nil
    }
    var left,right *TreeNode
    if root.Left != nil{
        left = mirrorTree(root.Left)
    }
    if root.Right != nil{
        right = mirrorTree(root.Right)
    }
    root.Left = right
    root.Right = left
    return root
}
```

