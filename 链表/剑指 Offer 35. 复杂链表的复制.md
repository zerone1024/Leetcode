#### [剑指 Offer 35. 复杂链表的复制](https://leetcode.cn/problems/fu-za-lian-biao-de-fu-zhi-lcof/)

请实现 copyRandomList 函数，复制一个复杂链表。在复杂链表中，每个节点除了有一个 next 指针指向下一个节点，还有一个 random 指针指向链表中的任意节点或者 null。

**示例 1：**

![image-20221005000605510](/Users/lizhaoran/Library/Application Support/typora-user-images/image-20221005000605510.png)

```
输入：head = [[7,null],[13,0],[11,4],[10,2],[1,0]]
输出：[[7,null],[13,0],[11,4],[10,2],[1,0]]
```

**示例 2：**

![image-20221005000620501](/Users/lizhaoran/Library/Application Support/typora-user-images/image-20221005000620501.png)

```
输入：head = [[1,1],[2,1]]
输出：[[1,1],[2,1]]
```

**示例 3：**

![image-20221005000723481](/Users/lizhaoran/Library/Application Support/typora-user-images/image-20221005000723481.png)

```
输入：head = [[3,null],[3,0],[3,null]]
输出：[[3,null],[3,0],[3,null]]
```

**示例 4：**

```
输入：head = []
输出：[]
解释：给定的链表为空（空指针），因此返回 null。
```



**题解**

方法一：哈希表
利用哈希表的查询特点，考虑构建 原链表节点 和 新链表对应节点 的键值对映射关系，再遍历构建新链表各节点的 next 和 random 引用指向即可。

算法流程：
若头节点 head 为空节点，直接返回 nullnull ；
初始化： 哈希表 dic ， 节点 cur 指向头节点；
复制链表：
建立新节点，并向 dic 添加键值对 (原 cur 节点, 新 cur 节点） ；
cur 遍历至原链表下一节点；
构建新链表的引用指向：
构建新节点的 next 和 random 引用指向；
cur 遍历至原链表下一节点；
返回值： 新链表的头节点 dic[cur] ；
复杂度分析：
时间复杂度 O(N)O(N) ： 两轮遍历链表，使用 O(N)O(N) 时间。
空间复杂度 O(N)O(N) ： 哈希表 dic 使用线性大小的额外空间。

```go
func copyRandomList(head *Node) *Node {
    // 1 若头结点head为nil直接返回空
    if head == nil {
        return nil
    }
    // 2 初始化
    var cur *Node = head
    copyMap := make(map[*Node]*Node)
    // 3 复制链表
    for cur != nil{
        copyMap[cur] = &Node{Val : cur.Val}
        cur = cur.Next
    }
    // 4 构建新链表的引用指向
    cur = head
    for cur != nil{
        copyMap[cur].Next = copyMap[cur.Next]
        copyMap[cur].Random = copyMap[cur.Random]
        cur = cur.Next
    }
    // 5 返回值
    return copyMap[head]
}
```



方法二：拼接 + 拆分
考虑构建 原节点 1 -> 新节点 1 -> 原节点 2 -> 新节点 2 -> …… 的拼接链表，如此便可在访问原节点的 random 指向节点的同时找到新对应新节点的 random 指向节点。

```golang
func copyRandomList(head *Node) *Node {
    if head == nil{
        return nil
    }
    cur := head
    // 1 复制各节点，构建拼接链表
    for cur != nil{
        temp := &Node{Val : cur.Val}
        temp.Next = cur.Next
        cur.Next = temp
        cur = temp.Next
    }
    // 2 构建新链表各节点的random指向
    cur = head
    for cur != nil{
        if cur.Random != nil{
            cur.Next.Random = cur.Random.Next
        }
        cur = cur.Next.Next
    }
    // 3 拆分原/新链表
    cur = head.Next
    pre := head
    res := head.Next
    for cur.Next != nil{
        pre.Next = pre.Next.Next
        cur.Next = cur.Next.Next
        pre = pre.Next
        cur = cur.Next 
    }
    pre.Next = nil
    // 4 返回新链表头部节点
    return res
}
```

