#### [剑指 Offer 47. 礼物的最大价值](https://leetcode.cn/problems/li-wu-de-zui-da-jie-zhi-lcof/)

在一个 m*n 的棋盘的每一格都放有一个礼物，每个礼物都有一定的价值（价值大于 0）。你可以从棋盘的左上角开始拿格子里的礼物，并每次向右或者向下移动一格、直到到达棋盘的右下角。给定一个棋盘及其上面的礼物的价值，请计算你最多能拿到多少价值的礼物？

 示例 1:

```
输入: 
[
  [1,3,1],
  [1,5,1],
  [4,2,1]
]
输出: 12
解释: 路径 1→3→5→2→1 可以拿到最多价值的礼物
```


提示：

```
0 < grid.length <= 200
0 < grid[0].length <= 200
```



题解

动态规划，列出状态转移方程轻松ac

```go
func maxValue(grid [][]int) int {
    rows := len(grid)
    if rows == 0{
        return 0
    }
    cols := len(grid[0])
    dp := make([][]int, rows+1)
    for i, _ := range dp{
        dp[i] = make([]int, cols+1)
    }
    for i := 0; i <= rows-1; i++{
        dp[i][0] = 0
    }
    for j := 0; j <= cols-1; j++{
        dp[0][j] = 0
    }
    for i := 1; i <= rows; i++{
        for j := 1; j <= cols; j++{
            dp[i][j] = max(dp[i][j-1], dp[i-1][j]) + grid[i-1][j-1]
        }
    }
    return dp[rows][cols]
}

func max(a, b int) int{
    if a >= b{
        return a
    }else{
        return b
    }
}
```

原数组原地修改减小空间复杂度的方法，添加条件判断即可

```go
func maxValue(grid [][]int) int {
    rows := len(grid)
    if rows == 0{
        return 0
    }
    cols := len(grid[0])

    for i := 0; i <= rows-1; i++{
        for j := 0; j <= cols-1; j++{
            if i == 0 && j != 0{
                grid[i][j] = grid[i][j] + grid[i][j-1]
            }else if i != 0 && j == 0{
                grid[i][j] = grid[i][j] + grid[i-1][j]
            }else if i != 0 && j != 0{
                grid[i][j] = max(grid[i-1][j], grid[i][j-1]) + grid[i][j]
            }
        }
    }
    return grid[rows-1][cols-1]
}

func max(a, b int) int{
    if a >= b{
        return a
    }else{
        return b
    }
}
```

