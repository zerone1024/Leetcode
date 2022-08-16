#### [剑指 Offer 24. 反转链表](https://leetcode.cn/problems/fan-zhuan-lian-biao-lcof/)

定义一个函数，输入一个链表的头节点，反转该链表并输出反转后链表的头节点。

 

```
示例:

输入: 1->2->3->4->5->NULL
输出: 5->4->3->2->1->NULL


限制：

0 <= 节点个数 <= 5000
```

 

注意：本题与主站 206 题相同：https://leetcode-cn.com/problems/reverse-linked-list/



题解：

迭代法

```go
func reverseList(head *ListNode) *ListNode {
    var prev *ListNode = nil
    var curr *ListNode = head
    for curr != nil{
        next := curr.Next
        curr.Next = prev
        prev = curr
        curr = next
    }
    return prev
}
```

递归法

```go
func reverseList(head *ListNode) *ListNode {
    // 递归终止条件
    if head == nil || head.Next == nil{
        return head
    }
    // 递归函数之前是递的过程中要做的事
    newHead := reverseList(head.Next)
    // 递归函数之后是归的过程中要做的事，即子问题已解决的情况下，当前问题的操作应该是什么
    head.Next.Next = head
    head.Next = nil

    return newHead
}
```

