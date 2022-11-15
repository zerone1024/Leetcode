#### [剑指 Offer 42. 连续子数组的最大和](https://leetcode.cn/problems/lian-xu-zi-shu-zu-de-zui-da-he-lcof/)

输入一个整型数组，数组中的一个或连续多个整数组成一个子数组。求所有子数组的和的最大值。

要求时间复杂度为O(n)。

 

示例1:

```
输入: nums = [-2,1,-3,4,-1,2,1,-5,4]
输出: 6
解释: 连续子数组 [4,-1,2,1] 的和最大，为 6。
```


提示：

```
1 <= arr.length <= 10^5
-100 <= arr[i] <= 100
```

注意：本题与主站 53 题相同：https://leetcode-cn.com/problems/maximum-subarray/

**动态规划，要注意核心思想：dp[i]是以nums[i]为结尾的和的最大值，所以评估的是dp[i-1]对该值的贡献，判断其正负**

```go
func maxSubArray(nums []int) int {
    length := len(nums)
    if length == 0{
        return 0
    }
    dp := make([]int, length)
    dp[0] = nums[0]
    for i := 1; i <= length - 1; i++{
        if dp[i-1] <= 0{
            dp[i] = nums[i]
        }else{
            dp[i] = dp[i-1] + nums[i]
        }
    }
    res := dp[0]
    for _, val := range dp{
        if val > res{
            res = val
        }
    }
    return res
}

func max(a, b int) int{
    if a >= b{
        return a
    }else{
        return b
    }
}
```

**节省空间复杂度的做法，直接在nums数组上操作，还有遍历一次即可**

```go
func maxSubArray(nums []int) int {
    length := len(nums)
    if length == 0{
        return 0
    }
    res := nums [0]
    for i := 1; i <= length - 1; i++{
        if nums[i-1] > 0{
            nums[i] = nums[i-1] + nums[i]
        }
        if nums[i] > res{
            res = nums[i]
        }
    }
    return res
}

func max(a, b int) int{
    if a >= b{
        return a
    }else{
        return b
    }
}
```

