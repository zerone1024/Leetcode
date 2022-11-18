#### [剑指 Offer 12. 矩阵中的路径](https://leetcode.cn/problems/ju-zhen-zhong-de-lu-jing-lcof/)

给定一个 m x n 二维字符网格 board 和一个字符串单词 word 。如果 word 存在于网格中，返回 true ；否则，返回 false 。

单词必须按照字母顺序，通过相邻的单元格内的字母构成，其中“相邻”单元格是那些水平相邻或垂直相邻的单元格。同一个单元格内的字母不允许被重复使用。

 

例如，在下面的 3×4 的矩阵中包含单词 "ABCCED"（单词中的字母已标出）。

![img](https://assets.leetcode.com/uploads/2020/11/04/word2.jpg)

 

示例 1：

```
输入：board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"

输出：true
```

示例 2：

```
输入：board = [["a","b"],["c","d"]], word = "abcd"
输出：false
```


提示：

```
m == board.length
n = board[i].length
1 <= m, n <= 6
1 <= word.length <= 15
board 和 word 仅由大小写英文字母组成
```

注意：本题与主站 79 题相同：https://leetcode-cn.com/problems/word-search/



题解

dfs + 剪枝，先遍历矩阵，然后对每个元素dfs,dfs函数中剪枝条件的判断要熟练掌握，dfs本质是递归

```go
func exist(board [][]byte, word string) bool {
    rows := len(board)
    if rows == 0{
        return false
    }
    cols := len(board[0])
    for i := 0; i <= rows - 1; i++{
        for j := 0; j <= cols - 1; j++{
            if dfs(board, word, i, j, 0){
                return true
            }
        }
    }
    return false
}

func dfs(board [][]byte, word string, i, j, k int)(res bool){
    rows := len(board)
    cols := len(board[0])
    if i < 0 || i >= rows || j < 0 || j >= cols || board[i][j] != word[k]{
        return false
    } 
    if k == len(word) - 1{
        return true
    }
    board[i][j] = '.'
    res = dfs(board, word, i + 1, j, k + 1) || dfs(board, word, i - 1, j, k + 1) || dfs(board, word, i, j + 1, k + 1) || dfs(board, word, i, j - 1, k + 1)
    board[i][j] = word[k]
    return res
}
```

