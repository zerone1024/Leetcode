#### [剑指 Offer 58 - II. 左旋转字符串](https://leetcode.cn/problems/zuo-xuan-zhuan-zi-fu-chuan-lcof/)

字符串的左旋转操作是把字符串前面的若干个字符转移到字符串的尾部。请定义一个函数实现字符串左旋转操作的功能。比如，输入字符串"abcdefg"和数字2，该函数将返回左旋转两位得到的结果"cdefgab"。

 

示例 1：

```
输入: s = "abcdefg", k = 2
输出: "cdefgab"
```

示例 2：

```
输入: s = "lrloseumgh", k = 6
输出: "umghlrlose"
```


限制：

1 <= k < s.length <= 10000



题解：

**常规数组拼接方法**

```go

func reverseLeftWords(s string, n int) string {
    s1 := []byte(s[:n])
    sTotal := []byte(s)
    sTotal = append(sTotal, s1...)
    ans := sTotal[n:]
    return string(ans)
}

```



**原地局部反转+整体反转**
为了让本题更有意义，提升一下本题难度：不能申请额外空间，只能在本串上操作。

不能使用额外空间的话，模拟在本串操作要实现左旋转字符串的功能还是有点困难的。

那么我们可以想一下上一题目字符串：花式反转还不够！中讲过，使用整体反转+局部反转就可以实现，反转单词顺序的目的。

这道题目也非常类似，依然可以通过局部反转+整体反转 达到左旋转的目的。

具体步骤为：

反转区间为前n的子串
反转区间为n到末尾的子串
反转整个字符串
最后就可以得到左旋n的目的，而不用定义新的字符串，完全在本串上操作。

例如 ：示例1中 输入：字符串abcdefg，n=2

作者：carlsun-2
链接：https://leetcode-cn.com/problems/zuo-xuan-zhuan-zi-fu-chuan-lcof/solution/dai-ma-sui-xiang-lu-dai-ni-gao-ding-zuo-vs2oc/

```go
func reverseLeftWords(s string, n int) string {
    b := []byte(s)
    reverse(b, 0, n-1)
    reverse(b, n ,len(b)-1)
    reverse(b, 0, len(b)-1)
    return string(b)
}

func reverse(b []byte, left, right int){
    for left < right{
        b[left], b[right] = b[right], b[left]
        left++
        right--
    }
}
```

