# LeetCode [371. 两整数之和](https://leetcode-cn.com/problems/sum-of-two-integers/)

<p align="center">
  <a href="https://mp.weixin.qq.com/s/TsTcCDboXwnTnUeIW3Zg9Q"><img src="https://img.shields.io/badge/LeetCode组队刷题群-blueviolet" alt=""></a>
</p>

## 题解

题目要求不能使用 $+、-$​，自然想到使用其他的二元运算符，我们可以根据二进制位，选择位运算符计算得到两数之和。

**二进制相加，思想类似于十进制加法，但从「逢十进一」变为 「逢二进一」。**

**两个二进制位相加有以下四种情况。**

```
1 + 1 = 0 (进位)

1 + 0 = 1 

0 + 1 = 1

0 + 0 = 0
```

直接使用异或 ^ 运算符的话，需要额外处理进位的情况， 即两个二进制位都为1。

我们可以使用 bit位为进位符，来判断这种情况。

下面考虑bit进位符，两个二进制位如何相加。



**假设现在统计到二进制的第 i 位。**

```
bit = 0 的情况         

二进制位相加                    运算后结果    

1 + 1 = 0 (进位)      -->    答案加 0       bit=1
1 + 0 = 1            -->    答案加 2^i     bit=0
0 + 1 = 1            -->    答案加 2^i     bit=0
0 + 0 = 0            -->    答案加 2^i     bit=0
```



```
bit = 1 的情况

二进制位相加                    运算后结果

1 + 1 = 0 (进位)   -->     答案加 2^i      bit=1
1 + 0 = 1          -->    答案加 0        bit=1
0 + 1 = 1          -->    答案加 0        bit=1
0 + 0 = 0          -->    答案加 2^i      bit=0
```

数据范围是 $-1000<=x<=1000$，如果没有负数，根据二进制位，我们只需要统计10个二进制位，因为 $2^{10}=1024>100$。

有负数的情况，我们需要统计到最高位，判断是否为负数，因此要统计32位。

时间复杂度: $O(C)$ C为常数32。

空间复杂度: $O(1)$。

## 代码



```c++
class Solution {
public:
    int getSum(int a, int b) {
        int ans = 0, bit = 0;
        for (int i = 0; i < 32; i++) {
            int x = (a >> i) & 1, y = (b >> i) & 1;
            if (x & y) {
                ans |= (bit << i);
                bit = 1;
            } else if (x | y) {
                ans |= (1 ^ bit) << i;
            } else {
                ans |= (bit << i);
                bit = 0;
            }
        }
        return ans;
    }
};
```


## 最后

大家好，我是编程熊，字节跳动、旷视科技前员工，ACM亚洲区域赛金牌，欢迎 [关注我](https://leetcode-cn.com/u/bianchengxiong/) 和加入 [LeetCode组队刷题群](https://mp.weixin.qq.com/s/TsTcCDboXwnTnUeIW3Zg9Q)。 



**分享几篇算法超级易懂的文章，希望对你有所帮助**

1、[ACM金牌选手讲解LeetCode算法《线性表》](https://mp.weixin.qq.com/s/qwaYOFIksFVqZtA_nisl6g)

2、[ACM金牌选手讲解LeetCode算法《栈和队列的高级应用》](https://mp.weixin.qq.com/s/I3DQOUmABmWav4nrAiI3Fg)

3、[ACM金牌选手讲解LeetCode算法《哈希表》](https://mp.weixin.qq.com/s/af4gvYURUoCTfsyzsI9Www)

4、[ACM金牌选手讲解LeetCode算法《二叉树》](https://mp.weixin.qq.com/s/8AcRNQS0Nno2_fU6kMtZeQ)

5、[编程熊讲解LeetCode算法《堆》](https://mp.weixin.qq.com/s/ggd42G_QJ6I43F-vXSbpdA) 



如果题解和文章对你有所帮助，欢迎**点赞**支持。