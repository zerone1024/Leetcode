#### [剑指 Offer 32 - I. 从上到下打印二叉树](https://leetcode.cn/problems/cong-shang-dao-xia-da-yin-er-cha-shu-lcof/)

从上到下打印出二叉树的每个节点，同一层的节点按照从左到右的顺序打印。

 

例如:
给定二叉树: [3,9,20,null,null,15,7],

```
	3
   / \
  9  20
    /  \
   15   7
```

返回：

```
[3,9,20,15,7]
```


提示：

```
节点总数 <= 1000
```



题解：

广度优先遍历，通过队列来实现，注意go中仅能通过数组实现队列

```go
func levelOrder(root *TreeNode) []int {
    res := make([]int, 0)
    if root == nil{
        return res
    }
    queueNode := []*TreeNode{root}
    for len(queueNode) != 0{
        node := queueNode[0]
        queueNode = queueNode[1:]
        res = append(res, node.Val)
        if node.Left != nil{
            queueNode = append(queueNode, node.Left)
        }
        if node.Right != nil{
            queueNode = append(queueNode, node.Right)
        }
    }
    return res
}
```

