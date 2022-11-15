#### [剑指 Offer 46. 把数字翻译成字符串](https://leetcode.cn/problems/ba-shu-zi-fan-yi-cheng-zi-fu-chuan-lcof/)

给定一个数字，我们按照如下规则把它翻译为字符串：0 翻译成 “a” ，1 翻译成 “b”，……，11 翻译成 “l”，……，25 翻译成 “z”。一个数字可能有多个翻译。请编程实现一个函数，用来计算一个数字有多少种不同的翻译方法。

 

示例 1:

```
输入: 12258
输出: 5
解释: 12258有5种不同的翻译，分别是"bccfi", "bwfi", "bczi", "mcfi"和"mzi"
```


提示：

```
0 <= num < 231
```



题解

属于看了答案也很难ac的题，需要重点关照一下，对思路和代码能力的要求都比较高：
1. 要把数字转成数组，要用到切片反转
2. 状态转移方程要理解，和青蛙跳台阶有相似性，都是可能和前两步有关系，即有条件的跳台阶
3. dp[0] = 1，要知道怎么来的，dp比nums多出来最开始的一个数

```go
func translateNum(num int) int {
    nums := make([]int, 0)
    for num != 0{
        nums = append(nums, num%10) 
        num = num/10
    }
    n := len(nums)
    if n == 0{
        return 1
    }
    for i, j := 0, n-1; i < j; i,j = i+1, j-1{
        nums[i], nums[j] = nums[j], nums[i]
    }
    dp := make([]int, n+1)
    dp[0] = 1
    dp[1] = 1
    for i := 2; i <= n; i++{
        if (10*nums[i-2] + nums[i-1] <= 25) && (10*nums[i-2] + nums[i-1] >= 10){
            dp[i] = dp[i-1] + dp[i-2]
        }else{
            dp[i] = dp[i-1]
        }
    }
    return dp[n]
}
```

虽然节约了空间，但我鄙视这种做法，各种值替换把人都整晕了，而且要证明逆向动规和正向一样

```go
func translateNum(num int) int {
    a, b := 1, 1
    x, y := num%10, num%10
    for num != 0{
        num = num/10
        x = num%10
        c := 1
        if (10 * x + y) <=25 && (10 * x + y) >=10{
            c = a + b
        }else{
            c = a
        }
        b = a
        a = c
        y = x
    }
    return b
}
```

