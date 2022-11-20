#### [面试题45. 把数组排成最小的数](https://leetcode.cn/problems/ba-shu-zu-pai-cheng-zui-xiao-de-shu-lcof/)

输入一个非负整数数组，把数组里所有数字拼接起来排成一个数，打印能拼接出的所有数字中最小的一个。

 

示例 1:

```
输入: [10,2]
输出: "102"
```

示例 2:

```
输入: [3,30,34,5,9]
输出: "3033459"
```


提示:

```
0 < nums.length <= 100
```

说明:

输出结果可能非常大，所以你需要返回一个字符串而不是整数
拼接起来的数字可能会有前导 0，最后结果不需要去掉前导 0



题解

首先是思路，要认识到这是一个排序问题，只要把所有数按“从小到大”规则排列，然后串起来就是最小数字
然后就是“从小到大”的规则，如何比较两个数的大小，比较直观的就是字符串加和，a + b < b + a，则 a < b
然后就是排序方法，这里用快排，优化时间复杂度

```go
func minNumber(nums []int) string {
    if len(nums) == 0{
        return "0"
    }
    strArr := make([]string, 0)
    for _, val := range nums{
        valStr := strconv.Itoa(val)
        strArr = append(strArr, valStr)
    }

    var quicksort func (strArr []string, l, r int) 
    quicksort = func(strArr []string, l, r int){
        if l >= r {
            return
        }
        i, j := l, r
        for i < j{
            for strArr[j] + strArr[l] >= strArr[l] + strArr[j] && i < j{
                j--
            }
            for strArr[i] + strArr[l] <= strArr[l] + strArr[i] && i < j {
                i++
            }       
            strArr[i], strArr[j] = strArr[j], strArr[i]
        }
        strArr[i], strArr[l] = strArr[l], strArr[i]
        quicksort(strArr, l, i-1)
        quicksort(strArr, i+1, r)
    }
    quicksort(strArr, 0, len(nums)-1)
    var res string
    for _, val := range strArr{
        res = res + val
    }
    return res
}
```

