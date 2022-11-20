#### [剑指 Offer 40. 最小的k个数](https://leetcode.cn/problems/zui-xiao-de-kge-shu-lcof/)

输入整数数组 arr ，找出其中最小的 k 个数。例如，输入4、5、1、6、2、7、3、8这8个数字，则最小的4个数字是1、2、3、4。

 

示例 1：

```
输入：arr = [3,2,1], k = 2
输出：[1,2] 或者 [2,1]
```

示例 2：

```
输入：arr = [0,1,2,1], k = 1
输出：[0]
```


限制：

```
0 <= k <= arr.length <= 10000
0 <= arr[i] <= 10000
```



题解

快排，轻松ac

```go
func getLeastNumbers(arr []int, k int) []int {
    if k == 0{
        return nil
    }
    quickSort(arr, 0, len(arr)-1)
    res := make([]int, 0)
    for i := 0; i <= k-1; i++{
        res = append(res, arr[i])
    } 
    return res
}

func quickSort(nums []int, l, r int){
    if l > r {
        return
    }
    i, j := l, r
    for i < j{
        for nums[j] >= nums[l] && i < j{
            j--
        }
        for nums[i] <= nums[l] && i < j{
            i++
        }
        nums[i], nums[j] = nums[j], nums[i]
    }
    nums[i], nums[l] = nums[l], nums[i]
    quickSort(nums, l, i-1)
    quickSort(nums, i+1, r)
}
```

基于快速排序的数组划分，把时间复杂度优化到O（N）
注意终止递归的条件变了，不再是子数组长度为1了

```GO
func getLeastNumbers(arr []int, k int) []int {
    if k >= len(arr){
        return arr
    }
    return quickSort(arr, 0, len(arr)-1, k)
}

func quickSort(nums []int, l, r, k int) ([]int){
    i, j := l, r
    for i < j{
        for nums[j] >= nums[l] && i < j{
            j--
        }
        for nums[i] <= nums[l] && i < j{
            i++
        }
        nums[i], nums[j] = nums[j], nums[i]
    }
    nums[i], nums[l] = nums[l], nums[i]
    if i < k{
        return quickSort(nums, i+1, r, k)
    }
    if i > k{
        return quickSort(nums, l, i-1, k)
    }
    res := make([]int, 0)
    for n := 0; n <= k-1; n++{
        res = append(res, nums[n])
    }
    return res
}
```

