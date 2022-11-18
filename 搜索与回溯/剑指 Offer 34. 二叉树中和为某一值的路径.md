#### [剑指 Offer 34. 二叉树中和为某一值的路径](https://leetcode.cn/problems/er-cha-shu-zhong-he-wei-mou-yi-zhi-de-lu-jing-lcof/)

给你二叉树的根节点 root 和一个整数目标和 targetSum ，找出所有 从根节点到叶子节点 路径总和等于给定目标和的路径。

叶子节点 是指没有子节点的节点。

示例 1：

![img](https://assets.leetcode.com/uploads/2021/01/18/pathsumii1.jpg)

```
输入：root = [5,4,8,11,null,13,4,7,2,null,null,5,1], targetSum = 22
输出：[[5,4,11,2],[5,8,4,5]]
```

示例 2：

![img](https://assets.leetcode.com/uploads/2021/01/18/pathsum2.jpg)

```
输入：root = [1,2,3], targetSum = 5
输出：[]
```

示例 3：

```
输入：root = [1,2], targetSum = 0
输出：[]
```


提示：

```
树中节点总数在范围 [0, 5000] 内
-1000 <= Node.val <= 1000
-1000 <= targetSum <= 1000
```

注意：本题与主站 113 题相同：https://leetcode-cn.com/problems/path-sum-ii/



题解

这题不想做过多评论，做的极其不开心，扔了，面试碰上认栽
学会在函数内定义和调用函数， path和res这两个数组都不用出现在递归函数的出入参里，而是作为一个局部的全局函数出现； res = append(res, append([]int(nil), path...))仔细 推敲下，让res和path解耦

```go
func pathSum(root *TreeNode, target int) [][]int {
    var path []int = make([]int, 0)
    var res [][]int = make([][]int, 0)
    var dfs func(*TreeNode, int)
    dfs = func(node *TreeNode, target int){
        if node == nil{
            return
        }
        path = append(path, node.Val)
        target = target - node.Val
        if node.Left == nil && node.Right == nil && target == 0{
            res = append(res, append([]int(nil), path...))
        }
        dfs(node.Left, target)
        dfs(node.Right, target)
        path = path[:len(path)-1]
    }
    dfs(root, target)
    return res
}
```

