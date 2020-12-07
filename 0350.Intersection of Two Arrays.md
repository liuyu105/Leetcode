# 0350-Intersection of Two Arrays Ⅱ

# 题目
给定两个数组，编写一个函数来计算它们的交集。<br />
<br />示例 1：
> 输入：nums1 = [1,2,2,1], nums2 = [2,2]
> 
> 输出：[2,2]

示例 2:
> 输入：nums1 = [4,9,5], nums2 = [9,4,9,8,4]
> 输出：[4,9]

# 标签
哈希表；排序；数组；双指针
# 解题思路
## 方法一：哈希表

- 由于同一个数字在两个数组中都可能出现多次，因此可以用哈希表存储每个数字出现的次数。对于一个数字，其在交集中出现的次数等于该数字在两个数组中出现次数的最小值。
- 首先遍历第一个数组，并在哈希表中记录第一个数组中的每个数字以及对应出现的次数，然后遍历第二个数组，对于第二个数组中的每个数字，如果在哈希表中存在这个数字，则将该数字添加到答案，并减少哈希表中该数字出现的次数。
- 为了降低空间复杂度，**首先遍历较短的数组**并在哈希表中记录每个数字以及对应出现的次数，然后遍历较长的数组得到交集。
## 方法二：排序

- 如果两个数组是有序的，则可以便捷地计算两个数组的交集。
- 首先对两个数组进行排序，然后使用两个指针遍历两个数组。
- 初始时，两个指针分别指向两个数组的头部。每次比较两个指针指向的两个数组中的数字，如果两个数字不相等，则将指向较小数字的指针右移一位，如果两个数字相等，将该数字添加到答案，并将两个指针都右移一位。当至少有一个指针超出数组范围时，遍历结束。
# 代码
```java
//给定两个数组，编写一个函数来计算它们的交集。
public class Leetcode350 {
    public static void main(String[] args) {
        int[] nums1 = {1, 2, 2, 1};
        int[] nums2 = {2};
        int[] result = Leetcode350.intersect2(nums1, nums2);
        for (int i = 0; i < result.length; i++) {
            System.out.print(result[i] + " ");
        }
    }

    public static int[] intersect(int[] nums1, int[] nums2) {
        //方法一：哈希表
        //先比较nums1与nums2的数组大小，将较小的作为参照对象，减少空间复杂度
        if (nums1.length > nums2.length) {
            return intersect(nums2, nums1);
        }
        //建立哈希映射，将元素与次数进行对应
        Map<Integer, Integer> map = new HashMap<>();
        //遍历较短的数组，统计每个元素出现的次数
        for (int num : nums1) {
            //刚开始键值对为null,count记录每个元素出现的次数
            //getOrDefault:如果get(num)为空，则返回defaultValue，否则返回get(num)
            int count = map.getOrDefault(num, 0) + 1;
            map.put(num, count);
        }
        int[] result = new int[nums1.length]; //定义结果数组
        int index = 0; //结果数组索引
        //遍历较长的数组，进行比较
        for (int num : nums2) {
            //取较长数组的元素个数
            int count = map.getOrDefault(num, 0);
            //判断count是否大于0
            if (count > 0) {
                result[index++] = num;
                count--;
                if (count > 0) {
                    map.put(num, count);
                } else {
                    map.remove(num);
                }
            }
        }
        return Arrays.copyOfRange(result, 0, index);
    }

    public static int[] intersect2(int[] nums1, int[] nums2) {
        //方法二：排序
        //先比较nums1与nums2的数组大小，将较小的作为参照对象，减少空间复杂度
        if (nums1.length > nums2.length) {
            return intersect2(nums2, nums1);
        }
        //排序
        Arrays.sort(nums1);
        Arrays.sort(nums2);
        //定义结果数组及索引
        int[] result = new int[nums1.length];
        int index = 0;
        //核心功能：双指针定位比较
        for (int i = 0, j = 0; i < nums1.length && j < nums2.length; ) {
            if (nums1[i] < nums2[j]) {
                i++;
            } else if (nums1[i] == nums2[j]) {
                result[index++] = nums1[i];
                i++;
                j++;
            } else {
                j++;
            }
        }
        return Arrays.copyOfRange(result, 0, index);

    }
}
```
来源：力扣（LeetCode）<br />链接：[https://leetcode-cn.com/problems/intersection-of-two-arrays-ii](https://leetcode-cn.com/problems/intersection-of-two-arrays-ii)<br />

