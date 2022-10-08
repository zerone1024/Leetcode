#### [剑指 Offer 32 - III. 从上到下打印二叉树 III](https://leetcode.cn/problems/cong-shang-dao-xia-da-yin-er-cha-shu-iii-lcof/)

请实现一个函数按照之字形顺序打印二叉树，即第一行按照从左到右的顺序打印，第二层按照从右到左的顺序打印，第三行再按照从左到右的顺序打印，其他行以此类推。

 

例如:
给定二叉树: [3,9,20,null,null,15,7],

```
	3
   / \
  9  20
    /  \
   15   7
```

返回其层次遍历结果：

```
[
  [3],
  [20,9],
  [15,7]
]
```


提示：

节点总数 <= 1000

来源：力扣（LeetCode）
链接：https://leetcode.cn/problems/cong-shang-dao-xia-da-yin-er-cha-shu-iii-lcof



题解：

关键技巧，要判断res的长度（二维数组行数），若为奇数则说明当前是偶数行，需要倒序打印；若为偶数，则需要正序打印。然后在写入数组的时候注意顺序即可。


```go
func levelOrder(root *TreeNode) [][]int {
    res := make([][]int, 0)
    if root == nil{
        return res
    }
    nodeQueue := []*TreeNode{root}
    for len(nodeQueue) != 0{
        n := len(nodeQueue)
        rows := make([]int, n)
        for i := 0; i <= n - 1; i++{
            if len(res) % 2 == 0{
                rows[i] = nodeQueue[i].Val
            }else{
                rows[n-1-i] = nodeQueue[i].Val
            }
            if nodeQueue[i].Left != nil{
                nodeQueue = append(nodeQueue, nodeQueue[i].Left)
            }
            if nodeQueue[i].Right != nil{
                nodeQueue = append(nodeQueue, nodeQueue[i].Right)
            } 
        }
        nodeQueue = nodeQueue[n:]
        res = append(res, rows)
    }
    return res
}
```
