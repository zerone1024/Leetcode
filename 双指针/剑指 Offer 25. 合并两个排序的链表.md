#### [剑指 Offer 25. 合并两个排序的链表](https://leetcode.cn/problems/he-bing-liang-ge-pai-xu-de-lian-biao-lcof/)

输入两个递增排序的链表，合并这两个链表并使新链表中的节点仍然是递增排序的。

示例1：

```
输入：1->2->4, 1->3->4
输出：1->1->2->3->4->4
```

限制：

0 <= 链表长度 <= 1000

注意：本题与主站 21 题相同：https://leetcode-cn.com/problems/merge-two-sorted-lists/



题解

```go
轻松ac，两个链表对应两个指针，伪头节点
func mergeTwoLists(l1 *ListNode, l2 *ListNode) *ListNode {
    if l1 == nil && l2 == nil{
        return nil
    }else if l1 == nil{
        return l2
    }else if l2 == nil{
        return l1
    }
    res := &ListNode{Val:0}
    cur := res
    node1, node2 := l1, l2
    for node1 != nil && node2 != nil{
        if node1.Val <= node2.Val{
            cur.Next = node1
            node1 = node1.Next
        }else{
            cur.Next = node2
            node2 = node2.Next
        }
        cur = cur.Next
    }
    if node1 == nil{
        cur.Next = node2
    }else if node2 == nil{
        cur.Next = node1
    }
    return res.Next
}
```

