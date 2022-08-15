#### [剑指 Offer 30. 包含min函数的栈](https://leetcode.cn/problems/bao-han-minhan-shu-de-zhan-lcof/)

定义栈的数据结构，请在该类型中实现一个能够得到栈的最小元素的 min 函数在该栈中，调用 min、push 及 pop 的时间复杂度都是 O(1)。

示例:

```
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.min();   --> 返回 -3.
minStack.pop();
minStack.top();      --> 返回 0.
minStack.min();   --> 返回 -2.
```


提示：

各函数的调用总次数不超过 20000 次

注意：本题与主站 155 题相同：https://leetcode-cn.com/problems/min-stack/



题解：

用数组来表示两个栈

```go
type MinStack struct {
    stack []int
    minStack []int
}


/** initialize your data structure here. */
func Constructor() MinStack {
    return MinStack{
        stack : []int{},
        minStack : []int{math.MaxInt64},
    }
}


func (this *MinStack) Push(x int)  {
    this.stack = append(this.stack, x)
    top := this.minStack[len(this.minStack)-1]
    this.minStack = append(this.minStack, min(x, top))
}


func (this *MinStack) Pop()  {
    this.stack = this.stack[:len(this.stack)-1]
    this.minStack = this.minStack[:len(this.minStack)-1]
}


func (this *MinStack) Top() int {
    return this.stack[len(this.stack)-1]
}


func (this *MinStack) Min() int {
    return this.minStack[len(this.minStack)-1]
}

func min(x, y int) int{
    if x < y{
        return x
    }
    return y
}


/**
 * Your MinStack object will be instantiated and called as such:
 * obj := Constructor();
 * obj.Push(x);
 * obj.Pop();
 * param_3 := obj.Top();
 * param_4 := obj.Min();
 */
```

