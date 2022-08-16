#### [剑指 Offer 06. 从尾到头打印链表](https://leetcode.cn/problems/cong-wei-dao-tou-da-yin-lian-biao-lcof/)

输入一个链表的头节点，从尾到头反过来返回每个节点的值（用数组返回）。

```
示例 1：

输入：head = [1,3,2]
输出：[2,3,1]
```



限制：

0 <= 链表长度 <= 10000



题解：

用数组记录链表各个节点的value，然后反转数组

```go
func reversePrint(head *ListNode) []int {
    nums1 := make([]int, 0)

    for node := head; node != nil; node = node.Next{
        nums1 = append(nums1, node.Val)
    }
    for i, j := 0, len(nums1)-1 ; i < j;{
        nums1[i], nums1[j] = nums1[j], nums1[i]
        i++
        j--
    }
    return nums1
}
```

