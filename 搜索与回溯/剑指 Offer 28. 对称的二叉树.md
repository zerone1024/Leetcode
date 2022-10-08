#### [剑指 Offer 28. 对称的二叉树](https://leetcode.cn/problems/dui-cheng-de-er-cha-shu-lcof/)

请实现一个函数，用来判断一棵二叉树是不是对称的。如果一棵二叉树和它的镜像一样，那么它是对称的。

例如，二叉树 [1,2,2,3,4,4,3] 是对称的。

```
	1
   / \
  2   2
 / \ / \
3  4 4  3
```

但是下面这个 [1,2,2,null,3,null,3] 则不是镜像对称的:

```
	1
   / \
  2   2
   \   \
   3    3
```

 

示例 1：

```
输入：root = [1,2,2,3,4,4,3]
输出：true
```

示例 2：

```
输入：root = [1,2,2,null,3,null,3]
输出：false
```


限制：

```
0 <= 节点个数 <= 1000
```

注意：本题与主站 101 题相同：https://leetcode-cn.com/problems/symmetric-tree/



题解：

对称的树用一个递归函数即可实现，关键是要想清楚递归的终止条件，然后再执行递推

```go
func isSymmetric(root *TreeNode) bool {
    if root == nil{
        return true
    }
    return recur(root.Left, root.Right)
}

func recur(left, right *TreeNode) bool{
    if left == nil && right == nil{
        return true
    }
    if left == nil || right == nil || left.Val != right.Val{
        return false
    }
    return recur(left.Left, right.Right) && recur(left.Right, right.Left)
}
```


