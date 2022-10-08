#### [剑指 Offer 04. 二维数组中的查找](https://leetcode.cn/problems/er-wei-shu-zu-zhong-de-cha-zhao-lcof/)

在一个 n * m 的二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个高效的函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

 

示例:

现有矩阵 matrix 如下：

```
[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]
```

给定 target = 5，返回 true。

给定 target = 20，返回 false。

 

限制：

```
0 <= n <= 1000

0 <= m <= 1000
```

 

注意：本题与主站 240 题相同：https://leetcode-cn.com/problems/search-a-2d-matrix-ii/



题解：

```go
func findNumberIn2DArray(matrix [][]int, target int) bool {
    if len(matrix) == 0 {
        return false
    }
    m := len(matrix) - 1
    n := len(matrix[0]) - 1

	i, j := m, 0
	for i >= 0 && j <= n{
    	flag := matrix[i][j]
    	if flag > target{
        	i--
    	}else if flag < target{
        	j++
    	}else{
        	return true
    	}
	}
	return false
}
```

