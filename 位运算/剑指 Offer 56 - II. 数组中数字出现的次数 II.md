#### [剑指 Offer 56 - II. 数组中数字出现的次数 II](https://leetcode.cn/problems/shu-zu-zhong-shu-zi-chu-xian-de-ci-shu-ii-lcof/)

在一个数组 nums 中除一个数字只出现一次之外，其他数字都出现了三次。请找出那个只出现一次的数字。

 

示例 1：

```
输入：nums = [3,4,3,3]
输出：4
```

示例 2：

```
输入：nums = [9,1,7,9,7,9,7]
输出：1
```


限制：

```
1 <= nums.length <= 10000
1 <= nums[i] < 2^31
```



题解

其实也很简单，对于每一位（0-31位），计算所有数对应的二进制在该位上为1和个数和，出现三次则和为3的倍数，最后对3取余数则得到出现一次的数字在该位的数字，最后左移加和即可。

```go
func singleNumber(nums []int) int {
    res := 0
    for i := 0; i <=31; i++{
        bits := 0
        for _, val := range nums{
            bits += ((val >> i) & 1)
        }
        res += ((bits % 3) << i)
    }
    return res
}
```

