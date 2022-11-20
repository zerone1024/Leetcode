#### [剑指 Offer 64. 求1+2+…+n](https://leetcode.cn/problems/qiu-12n-lcof/)

求 1+2+...+n ，要求不能使用乘除法、for、while、if、else、switch、case等关键字及条件判断语句（A?B:C）。

 

示例 1：

```
输入: n = 3
输出: 6
```

示例 2：

```
输入: n = 9
输出: 45
```


限制：

1 <= n <= 10000



题解

用递归又不用if来判断终止条件，这里加入了&&短路，即a&&b，当a为false时短路b，这样就可以实现a为true的时候递归，a为false的时候终止递归，这题要多理解几遍

```go
func sumNums(n int) int {
    res := 0
    var sum func(n int) bool
    sum = func(n int) bool{
        res = res + n
        return n > 1 && sum(n-1) 
    }
    sum(n)
    return res
}
```

