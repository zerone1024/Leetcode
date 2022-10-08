#### [剑指 Offer 10- I. 斐波那契数列](https://leetcode.cn/problems/fei-bo-na-qi-shu-lie-lcof/)

写一个函数，输入 n ，求斐波那契（Fibonacci）数列的第 n 项（即 F(N)）。斐波那契数列的定义如下：

F(0) = 0,   F(1) = 1
F(N) = F(N - 1) + F(N - 2), 其中 N > 1.
斐波那契数列由 0 和 1 开始，之后的斐波那契数就是由之前的两数相加而得出。

答案需要取模 1e9+7（1000000007），如计算初始结果为：1000000008，请返回 1。

 

示例 1：

```
输入：n = 2
输出：1
```

示例 2：

```
输入：n = 5
输出：5
```


提示：

```
0 <= n <= 100
```



题解：

用三个数轮回赋值取代动规数组的解法

```go
func fib(n int) int {
    if n == 0 {
        return 0
    }
    if n == 1 {
        return 1
    }
    var a, b, sums int
    a = 0
    b = 1
    for i := 2; i <= n; i++{
        sums = (a + b)%1000000007
        a = b
        b = sums
    }
    return sums
}
```



利用数组进行动态规划的解法， 记得在每次求和时取余

```go
func fib(n int) int {
    if n == 0 {
        return 0
    }
    if n == 1 {
        return 1
    }
    nums := make([]int, n+1)
    nums[0] = 0
    nums[1] = 1
    for i := 2; i <= n; i++{
        nums[i] = (nums[i-1] + nums[i-2])%1000000007
    }
    return nums[n]
}
```



递归法，直接超时

```c++
class Solution {
public:
    int fib(int n) {
        if(n == 0) return 0;
        else if(n == 1) return 1;
        else return fib(n-1) + fib(n-2);
    }
};
```

