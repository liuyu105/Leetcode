#  题目

一个整型数组 nums 里除两个数字之外，其他数字都出现了两次。请写程序找出这两个只出现一次的数字。要求时间复杂度是O(n)，空间复杂度是O(1)。

示例 1：

> 输入：nums = [4,1,4,6]
> 输出：[1,6] 或 [6,1]

示例 2：

> 输入：nums = [1,2,10,4,1,4,3,3]
> 输出：[2,10] 或 [10,2]

# 标签

数组；异或

# 解题思路

假如除了一个数字之外，其他数字都出现了两次，便可以用全员异或来求得该数字。

异或的基本公式：a^a=0   a^0=a

当有两个数字时，全员异或的结果即为两个不同数字的异或结果。两个数字不同，那么（二进制数）至少有一位不同，才能使得异或结果不为0。所以可以根据这个规律，将以上所有数字分为两个数组，同时也将两个待求数字分隔开。

# 代码

```java
class Solution {
    public int[] singleNumbers(int[] nums) {
        int sum = 0;
        for (int i : nums) {
            sum ^= i;//求全员异或
        }
        int div = 1;
        //寻找最低位为1的位置
        while ((sum & div) == 0) {
            div <<= 1;
        }
        int a = 0, b = 0;
        //分成两个数组
        for (int n : nums) {
            if ((n & div) == 0) {
                a ^= n;
            } else {
                b ^= n;
            }
        }
        return new int[]{a, b};
    }
}
```

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/shu-zu-zhong-shu-zi-chu-xian-de-ci-shu-lcof
