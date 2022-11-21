#### [剑指 Offer 56 - I. 数组中数字出现的次数](https://leetcode.cn/problems/shu-zu-zhong-shu-zi-chu-xian-de-ci-shu-lcof/)

一个整型数组 nums 里除两个数字之外，其他数字都出现了两次。请写程序找出这两个只出现一次的数字。要求时间复杂度是O(n)，空间复杂度是O(1)。

 

示例 1：

```
输入：nums = [4,1,4,6]
输出：[1,6] 或 [6,1]
```

示例 2：

```
输入：nums = [1,2,10,4,1,4,3,3]
输出：[2,10] 或 [10,2]
```


限制：

```
2 <= nums.length <= 10000
```



题解

这题的基础版本是找到一个没有重复出现的数字，当有两个没重复出现过的数字（a,b）时，需要把这两个数字区分出来，分即成两个只有一个不重复数字（只有a或者只有b）的数组，然后继续求解。如何拆分成两个数组？找到a和b不相同的一位m即可（即a异或b不为0的一位）,然后数组中所有数字&m，得到0或者非0则可以区分出两组。最后用0异或则可得解。

```go
func singleNumbers(nums []int) []int {
    temp := 0
    for _, val := range nums{
        temp ^= val
    }
    m := 1
    for m & temp == 0{
        m <<= 1
    }
    x, y := 0, 0
    for _, val := range nums{
        if val & m != 0{
            x ^= val
        }else if val & m == 0{
            y ^= val
        }
    }
    return []int{x, y}
}
```

