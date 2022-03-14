# 数组部分

## 1 两数之和

给定一个整数数组 nums 和一个整数目标值 target，请你在该数组中找出 和为目标值 target  的那 两个 整数，并返回它们的数组下标。

你可以假设每种输入只会对应一个答案。但是，数组中同一个元素在答案里不能重复出现。

你可以按任意顺序返回答案。

```
示例 1：
    输入：nums = [2,7,11,15], target = 9
    输出：[0,1]
    解释：因为 nums[0] + nums[1] == 9 ，返回 [0, 1] 。
示例 2：
    输入：nums = [3,2,4], target = 6
    输出：[1,2]
示例 3：
    输入：nums = [3,3], target = 6
    输出：[0,1]
```

**解答**

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int []result = new int[2];
        //非有序,暴力
        for(int i = 0;i < nums.length;i++){
            for(int j = i + 1;j < nums.length;j++){
                if(nums[i] + nums[j] == target){
                    result[0] = i;
                    result[1] = j;
                }
            }
        }
        return result;
    }
}
```



## 2 盛最多水的容器

给定一个长度为 n 的整数数组 height 。有 n 条垂线，第 i 条线的两个端点是 (i, 0) 和 (i, height[i]) 。

找出其中的两条线，使得它们与 x 轴共同构成的容器可以容纳最多的水。

返回容器可以储存的最大水量。

说明：你不能倾斜容器。



**示例 1**

![img](img/question_11.jpg)

```
输入：[1,8,6,2,5,4,8,3,7]
输出：49 
解释：图中垂直线代表输入数组 [1,8,6,2,5,4,8,3,7]。在此情况下，容器能够容纳水（表示为蓝色部分）的最大值为 49。
```

**示例 2**

```
输入：height = [1,1]
输出：1
```

**解答**

`动态规划`   使用左右指针进行截取, 想要取到最大的值,就要考虑距离和高度的二优化。这时我们使用左指针和右指针分别处于数组开头和结尾。每执行一次进行一次比较并将值保存到 max 变量中,再移动左右指针中高度较小的,最终就一定可以取得最大值。

```
public class Solution {
    public int maxArea(int[] height) {
        //实质上就是找 row1 * row2 的 maxvalue
        //使用双指针
        int left =0,right = height.length - 1,max=0;
        while(left < right){
            int min = Math.min(height[left],height[right]);
            int distance = right - left;
            max = Math.max(max,min * distance);
            //移动高度较小的
            if(height[left] < height[right])
                left++;
            else
                right--;
        }
        return max;
    }
}
```



3 











