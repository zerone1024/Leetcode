#### [剑指 Offer 65. 不用加减乘除做加法](https://leetcode.cn/problems/bu-yong-jia-jian-cheng-chu-zuo-jia-fa-lcof/)

写一个函数，求两个整数之和，要求在函数体内不得使用 “+”、“-”、“*”、“/” 四则运算符号。

 

示例:

```
输入: a = 1, b = 1
输出: 2
```


提示：

```
a, b 均可能是负数或 0
结果不会溢出 32 位整数
```



题解

此题的关键是拆分加法为 非进位和（a^b） + 进位值 (a&b<<1)，然后把非进位和给a，把进位值给b，当b不为0时一直循环，b为0时跳出返回a值即为和

```go
func add(a int, b int) int {
    for{
        sum := a ^ b
        c := (a & b) << 1
        a = sum
        b = c
        if b == 0{
            return a
        }
    }
}
```

