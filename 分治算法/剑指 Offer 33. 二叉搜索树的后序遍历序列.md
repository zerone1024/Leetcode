#### [剑指 Offer 33. 二叉搜索树的后序遍历序列](https://leetcode.cn/problems/er-cha-sou-suo-shu-de-hou-xu-bian-li-xu-lie-lcof/)

输入一个整数数组，判断该数组是不是某二叉搜索树的后序遍历结果。如果是则返回 true，否则返回 false。假设输入的数组的任意两个数字都互不相同。

 

参考以下这颗二叉搜索树：

```
     5
    / \
   2   6
  / \
 1   3
```

示例 1：

```
输入: [1,6,3,2,5]
输出: false
```

示例 2：

```
输入: [1,3,2,6,5]
输出: true
```


提示：

```
数组长度 <= 1000
```



题解

注意是二叉搜索树（条件是：左子树都小于根，右子树都大于根），所以数组的最后一个数必为根。要把根前面的区间划分出左右子树，第一个大于根的即为分界点。然后递归验证左右子树是否为二叉搜索树，直到区间为0，直接返回true。

```go
func verifyPostorder(postorder []int) bool {
    return recur(0, len(postorder)-1, postorder)
}

func recur(i, j int, postorder []int) bool{
    if i >= j{
        return true
    }
    m := i
    for m <= j-1{
        if postorder[m] > postorder[j]{
            break
        }
        m++
    }
    for k := m; k <= j-1; k++{
        if postorder[k] < postorder[j]{
            return false
        }
    }
    return recur(i, m-1, postorder) && recur(m, j-1, postorder)
}
```

