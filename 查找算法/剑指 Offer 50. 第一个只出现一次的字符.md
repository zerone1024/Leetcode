#### [剑指 Offer 50. 第一个只出现一次的字符](https://leetcode.cn/problems/di-yi-ge-zhi-chu-xian-yi-ci-de-zi-fu-lcof/)

在字符串 s 中找出第一个只出现一次的字符。如果没有，返回一个单空格。 s 只包含小写字母。

示例 1:

```
输入：s = "abaccdeff"
输出：'b'
```

示例 2:

```
输入：s = "" 
输出：' '
```


限制：

```
0 <= s 的长度 <= 50000
```



题解：

就是常规的哈希思想，要注意的是go 直接用map实现性能较差，需要很多类型转换，所以要用数组实现

```go
func firstUniqChar(s string) byte {
    cnt := [26]int{}
    for _, ch := range s{
        cnt[ch - 'a']++
    }
    for i, ch := range s{
        if cnt[ch - 'a'] == 1{
            return s[i]
        }
    }
    return ' '
}
```

