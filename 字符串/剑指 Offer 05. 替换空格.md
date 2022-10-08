#### [剑指 Offer 05. 替换空格](https://leetcode.cn/problems/ti-huan-kong-ge-lcof/)

请实现一个函数，把字符串 s 中的每个空格替换成"%20"。

 

示例 1：

```
输入：s = "We are happy."
输出："We%20are%20happy."
```


限制：

0 <= s 的长度 <= 10000



题解：

```go
go无法原地修改数组
func replaceSpace(s string) string {
    count := 0
    length := len(s)
    // 统计空格数量
    for _, val := range s{
        if val == ' '{
            count++
        }
    }
    newLength := length + 2 * count
    // go无法原地扩充s，需要make一个新数组
    ans := make([]byte, newLength)
    i, j := length - 1, newLength - 1
    for ; i >= 0; i-- {
        if s[i] != ' '{
            ans[j] = s[i]
            j--
        }else{
            ans[j] = '0'
            ans[j-1] = '2'
            ans[j-2] = '%'
            j -= 3
        }
    }
    return string(ans)
}
```

