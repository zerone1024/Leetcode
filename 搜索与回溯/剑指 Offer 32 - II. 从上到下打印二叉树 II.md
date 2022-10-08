#### [剑指 Offer 32 - II. 从上到下打印二叉树 II](https://leetcode.cn/problems/cong-shang-dao-xia-da-yin-er-cha-shu-ii-lcof/)

从上到下按层打印二叉树，同一层的节点按从左到右的顺序打印，每一层打印到一行。

 

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
  [9,20],
  [15,7]
]
```


提示：

```
节点总数 <= 1000
```

注意：本题与主站 102 题相同：https://leetcode-cn.com/problems/binary-tree-level-order-traversal/



题解：

需要两层遍历，注意内层遍历的循环次数即为当前队列的元素个数。将本层节点打印到一行，并将下一层节点加入队列。

```go
func levelOrder(root *TreeNode) [][]int {
    var res [][]int
    //res := make([][]int, 0)
    if root == nil{
        return res
    }
	nodeQueue := []*TreeNode{root}

    for len(nodeQueue) != 0{
        rows := make([]int, 0)
        n := len(nodeQueue)
        for i := 0; i <= n - 1; i++{
            node := nodeQueue[0]
            nodeQueue = nodeQueue[1:]
            if node != nil{
                rows = append(rows, node.Val)
            }
            if node.Left != nil{
                nodeQueue = append(nodeQueue, node.Left)
            }
            if node.Right != nil{
                nodeQueue = append(nodeQueue, node.Right)
            }
        }
        res = append(res, rows)
    }
	return res
}
```


**错误解法**

错误原因：
        if len(nodeQueue) > n{
            nodeQueue = nodeQueue[n:]
        }

 导致nodeQueue一直有值而无法退出，这里无需进行长度判断，即便nodeQueue长度为n，nodeQueue[n:]也不会超限，而会直接返回一个空切片

```go
func levelOrder(root *TreeNode) [][]int {
    var res [][]int
    //res := make([][]int, 0)
    if root == nil{
        return res
    }
    nodeQueue := []*TreeNode{root}

    for len(nodeQueue) != 0{
        rows := make([]int, 0)
        n := len(nodeQueue)
        for i := 0; i <= n - 1; i++{
            rows = append(rows, nodeQueue[i].Val)
            if nodeQueue[i].Left != nil{
                nodeQueue = append(nodeQueue, nodeQueue[i].Left)
            }
            if nodeQueue[i].Right != nil{
                nodeQueue = append(nodeQueue, nodeQueue[i].Right)
            }
        }
        if len(nodeQueue) > n{
            nodeQueue = nodeQueue[n:]
        }
        if len(rows) > 0{
            res = append(res, rows) 
        }

    }
    return res
}
```
