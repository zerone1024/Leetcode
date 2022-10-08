#### [剑指 Offer 63. 股票的最大利润](https://leetcode.cn/problems/gu-piao-de-zui-da-li-run-lcof/)

假设把某股票的价格按照时间先后顺序存储在数组中，请问买卖该股票一次可能获得的最大利润是多少？

 

示例 1:

```
输入: [7,1,5,3,6,4]
输出: 5
解释: 在第 2 天（股票价格 = 1）的时候买入，在第 5 天（股票价格 = 6）的时候卖出，最大利润 = 6-1 = 5 。
     注意利润不能是 7-1 = 6, 因为卖出价格需要大于买入价格。
```

示例 2:

```
输入: [7,6,4,3,1]
输出: 0
解释: 在这种情况下, 没有交易完成, 所以最大利润为 0。
```


限制：

```
0 <= 数组长度 <= 10^5
```

 

注意：本题与主站 121 题相同：https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock/



题解：

太牛逼了，动态规划直接ac

```go
func maxProfit(prices []int) int {
    length := len(prices)
    if length <= 0{
        return 0
    }
    res := make([]int, length)
    res[0] = 0
    minPrice := prices[0]
    for i := 1; i <= length-1; i++{
        res[i] = prices[i] - minPrice
        res[i] = max(res[i], res[i-1])
        if prices[i] < minPrice{
            minPrice = prices[i]
        }
    }
    return res[length-1]
}

func max(a, b int) int{
    if a >= b {
        return a
    }else{
        return b
    }
}
```



节约空间复杂度的做法，无非是把数组换成常量

```go
func maxProfit(prices []int) int {
    length := len(prices)
    if length <= 0{
        return 0
    }
    var profit, minPrice int
    minPrice = prices[0]
    for _, val := range prices{
        profit = max(profit, val-minPrice)
        if val < minPrice{
            minPrice = val
        }
    }
    return profit
}

func max(a, b int) int{
    if a >= b {
        return a
    }else{
        return b
    }
}
```


