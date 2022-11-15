#### [剑指 Offer 48. 最长不含重复字符的子字符串](https://leetcode.cn/problems/zui-chang-bu-han-zhong-fu-zi-fu-de-zi-zi-fu-chuan-lcof/)

请从字符串中找出一个最长的不包含重复字符的子字符串，计算该最长子字符串的长度。

 

示例 1:

```
输入: "abcabcbb"
输出: 3 
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。
```

示例 2:

```
输入: "bbbbb"
输出: 1
解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。
```

示例 3:

```
输入: "pwwkew"
输出: 3
解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。
     请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。
```


提示：

```
s.length <= 40000
```

注意：本题与主站 3 题相同：https://leetcode-cn.com/problems/longest-substring-without-repeating-characters/



题解

动态规划+双指针，还要用哈希表来存储字母最后一次出现的索引，注意制作key为字符的哈希表的方法

```go
func lengthOfLongestSubstring(s string) int {
    if len(s) == 0{
        return 0
    }
    str := []byte(s)
    indexMap := make(map[byte]int)
    dp := make([]int, len(s))
    res := 1
    for id, val := range str{
        i := -1
        if key, ok := indexMap[val]; ok{
            i = key
        }
        indexMap[val] = id
        if id == 0{
            dp[id] = 1
            continue
        }
        if dp[id-1] >= id - i{
            dp[id] = id - i
        }else{
            dp[id] = dp[id-1]+1
        }
        if dp[id] > res{
            res = dp[id]
        }   
    }
    return res
}
```

节约空间复杂度的方法，将dp数组用常数替换

```go
func lengthOfLongestSubstring(s string) int {
    if len(s) == 0{
        return 0
    }
    str := []byte(s)
    indexMap := make(map[byte]int)
    res := 1
    a, b := 1, 1
    for id, val := range str{
        i := -1
        if key, ok := indexMap[val]; ok{
            i = key
        }
        indexMap[val] = id
        if a >= id - i{
            b = id - i
        }else{
            b = a + 1
        }
        if b > res{
            res = b
        }
        a = b   
    }
    return res
}
```

