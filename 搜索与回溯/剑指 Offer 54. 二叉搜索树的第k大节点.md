#### [剑指 Offer 54. 二叉搜索树的第k大节点](https://leetcode.cn/problems/er-cha-sou-suo-shu-de-di-kda-jie-dian-lcof/)

给定一棵二叉搜索树，请找出其中第 k 大的节点的值。

 

示例 1:

```
输入: root = [3,1,4,null,2], k = 1
   3
  / \
 1   4
  \
   2
输出: 4
```

示例 2:

```
输入: root = [5,3,6,2,4,null,null,1], k = 3
       5
      / \
     3   6
    / \
   2   4
  /
 1
输出: 4
```


限制：

```
1 ≤ k ≤ 二叉搜索树元素个数
```



题解

正序中序遍历用一个数组ac，倒序中序遍历可用一个常量ac,节约空间复杂度

```go
func kthLargest(root *TreeNode, k int) int {
    res := 0
    var dfs func(*TreeNode)
    dfs = func(node *TreeNode){
        if node == nil{
            return
        }
        dfs(node.Right)
        k = k - 1
        if k == 0{
            res = node.Val
        }
        dfs(node.Left)
    }
    dfs(root)
    return res
}
```

