### 1 [交替合并字符串](https://leetcode.cn/problems/merge-strings-alternately/)

> 给你两个字符串 word1 和 word2 。请你从 word1 开始，通过交替添加字母来合并字符串。如果一个字符串比另一个字符串长，就将多出来的字母追加到合并后字符串的末尾。
>
> 返回 合并后的字符串 。

 ```
 示例 1：
 输入：word1 = "abc", word2 = "pqr"
 输出："apbqcr"
 解释：字符串合并情况如下所示：
 word1：  a   b   c
 word2：    p   q   r
 合并后：  a p b q c r
 示例 2：
 输入：word1 = "ab", word2 = "pqrs"
 输出："apbqrs"
 解释：注意，word2 比 word1 长，"rs" 需要追加到合并后字符串的末尾。
 word1：  a   b 
 word2：    p   q   r   s
 合并后：  a p b q   r   s
 示例 3：
 输入：word1 = "abcd", word2 = "pq"
 输出："apbqcd"
 解释：注意，word1 比 word2 长，"cd" 需要追加到合并后字符串的末尾。
 word1：  a   b   c   d
 word2：    p   q 
 合并后：  a p b q c   d
 ```

**题解**

```java
    public String mergeAlternately(String word1, String word2) {
        int length = word1.length() + word2.length();
        char []str = new char[length];
        int pre = 0,next = 0,tag = 0;
        for(int i = 0;i < length; i++){
            if(pre < word1.length()){
                str[tag++] = word1.charAt(pre++);
            }
            if(next < word2.length()){
                str[tag++] = word2.charAt(next++);
            }
        }
        return new String(str);
    }
```



### 2 [字符串的最大公因子](https://leetcode.cn/problems/greatest-common-divisor-of-strings/)

> 对于字符串 s 和 t，只有在 s = t + ... + t（t 自身连接 1 次或多次）时，我们才认定 “t 能除尽 s”。
>
> 给定两个字符串 str1 和 str2 。返回 最长字符串 x，要求满足 x 能除尽 str1 且 x 能除尽 str2 。
>

```
示例 1：
输入：str1 = "ABCABC", str2 = "ABC"
输出："ABC"
示例 2：
输入：str1 = "ABABAB", str2 = "ABAB"
输出："AB"
示例 3：
输入：str1 = "LEET", str2 = "CODE"
输出：""
```



```java
class Solution {
    public String gcdOfStrings(String str1, String str2) {
        if(!(str1 + str2).equals(str2 + str1)){
            return "";
        }
        return str1.substring(0, gcd(str1.length(), str2.length()));
    }

    //最大公因子算法 a = 24 b = 4 => return = 4
    public int gcd(int a,int b){
        int tag = a % b;
        while(tag != 0){
            a = b;
            b = tag;
            tag = a % b;
        }
        return b;
    }
}
```



### 3 [拥有最多糖果的孩子](https://leetcode.cn/problems/kids-with-the-greatest-number-of-candies/)

> 给你一个数组 candies 和一个整数 extraCandies ，其中 candies[i] 代表第 i 个孩子拥有的糖果数目。
>
> 对每一个孩子，检查是否存在一种方案，将额外的 extraCandies 个糖果分配给孩子们之后，此孩子有 最多 的糖果。注意，允许有多个孩子同时拥有 最多 的糖果数目。

```
示例 1：
输入：candies = [2,3,5,1,3], extraCandies = 3
输出：[true,true,true,false,true] 
解释：
孩子 1 有 2 个糖果，如果他得到所有额外的糖果（3个），那么他总共有 5 个糖果，他将成为拥有最多糖果的孩子。
孩子 2 有 3 个糖果，如果他得到至少 2 个额外糖果，那么他将成为拥有最多糖果的孩子。
孩子 3 有 5 个糖果，他已经是拥有最多糖果的孩子。
孩子 4 有 1 个糖果，即使他得到所有额外的糖果，他也只有 4 个糖果，无法成为拥有糖果最多的孩子。
孩子 5 有 3 个糖果，如果他得到至少 2 个额外糖果，那么他将成为拥有最多糖果的孩子。
示例 2：
输入：candies = [4,2,1,1,2], extraCandies = 1
输出：[true,false,false,false,false] 
解释：只有 1 个额外糖果，所以不管额外糖果给谁，只有孩子 1 可以成为拥有糖果最多的孩子。
示例 3：
输入：candies = [12,1,12], extraCandies = 10
输出：[true,false,true]
```

**题解**

```java
class Solution {
    public List<Boolean> kidsWithCandies(int[] candies, int extraCandies) {
        //记录最大的糖果数
        int max = -1;
        for(int i = 0; i < candies.length; i++){
            if(max < candies[i]){
                max = candies[i];
            }
        }
        List<Boolean> condition = new ArrayList<>();
        for (int i = 0; i < candies.length; i++) {
            if(candies[i] + extraCandies >= max){
                condition.add(true);
            } else{
                condition.add(false);
            }
        }
        return condition;
    }
}
```



### 4 种花问题

> 假设有一个很长的花坛，一部分地块种植了花，另一部分却没有。可是，花不能种植在相邻的地块上，它们会争夺水源，两者都会死去。
>
> 给你一个整数数组 flowerbed 表示花坛，由若干 0 和 1 组成，其中 0 表示没种植花，1 表示种植了花。另有一个数 n ，能否在不打破种植规则的情况下种入 n 朵花？能则返回 true ，不能则返回 false 。

```java
示例 1：
输入：flowerbed = [1,0,0,0,1], n = 1
输出：true
示例 2：
输入：flowerbed = [1,0,0,0,1], n = 2
输出：false
```

题解

```java
class Solution {
    public boolean canPlaceFlowers(int[] flowerbed, int n) {
        //暴力插入, 不断判定在0的位置插入数据是否可行
        int count = 0;
        for (int i = 0; i < flowerbed.length; i++) {
            if(flowerbed[i] == 1)
                continue;
            if(check(flowerbed, i)){
                count++;
                flowerbed[i] = 1;
            }
        }
        // 使用 Lambda 表达式打印整型数组
        Arrays.stream(flowerbed).forEach(num -> System.out.print(num + " "));
        return count >= n;
    }

    public boolean check(int[] flowerbed, int index) {
        if(flowerbed.length == 1 && flowerbed[index] == 0){
            return true;
        }
        if(index == 0){
            return flowerbed[index + 1] == 0;
        }
        if(index == flowerbed.length-1){
            return flowerbed[index - 1] == 0;
        }
        return flowerbed[index-1] == 0 && flowerbed[index+1] == 0;
    }
}
```





### 5 [反转字符串中的元音字母](https://leetcode.cn/problems/reverse-vowels-of-a-string/)

给你一个字符串 s ，仅反转字符串中的所有元音字母，并返回结果字符串。

元音字母包括 'a'、'e'、'i'、'o'、'u'，且可能以大小写两种形式出现不止一次。

`示例`

```java
示例 1：
输入：s = "hello"
输出："holle"
示例 2：
输入：s = "leetcode"
输出："leotcede"
```



**题解**

```java
package Solutions;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

public class Solution {
    public static String reverseVowels(String s) {
        //双指针
        char[] chars = s.toCharArray();
        int pre = 0, tail = s.length()-1;
        //初始化下标指针
        while(pre < tail){
            while(pre < tail && !checkChar(chars[pre])){
                pre++;
            }

            while(pre < tail && !checkChar(chars[tail])){
                tail--;
            }
            System.out.println(pre);
            System.out.println(tail);
            char temp = chars[pre];
            chars[pre] = chars[tail];
            chars[tail] = temp;
            pre++;
            tail--;
        }
        return new String(chars);
    }

    public static Boolean checkChar(char ch){
        return (ch == 'a' || ch == 'e' || ch == 'i' || ch == 'o' || ch == 'u' ||
                ch == 'A' || ch == 'E' || ch == 'I' || ch == 'O' || ch == 'U');
    }


    public static void main(String[] args) {
        System.out.println(reverseVowels("hello"));
    }
}
```



### [6. 反转字符串中的单词](https://leetcode.cn/problems/reverse-words-in-a-string/)

> 给你一个字符串 s ，请你反转字符串中 单词 的顺序。
>
> 单词 是由非空格字符组成的字符串。s 中使用至少一个空格将字符串中的 单词 分隔开。
>
> 返回 单词 顺序颠倒且 单词 之间用单个空格连接的结果字符串。
>
> 注意：输入字符串 s中可能会存在前导空格、尾随空格或者单词间的多个空格。返回的结果字符串中，单词间应当仅用单个空格分隔，且不包含任何额外的空格。

 ```
 示例 1：
 输入：s = "the sky is blue"
 输出："blue is sky the"
 示例 2：
 输入：s = "  hello world  "
 输出："world hello"
 解释：反转后的字符串中不能存在前导空格和尾随空格。
 示例 3：
 输入：s = "a good   example"
 输出："example good a"
 解释：如果两个单词间有多余的空格，反转后的字符串需要将单词间的空格减少到仅有一个。
 ```

**题解**

```java
class Solution {
    public String reverseWords(String s) {
        String[] splits = s.split(" ");
        // 使用 Lambda 表达式打印整型数组
        List<String> strs = new ArrayList<>();
        Arrays.stream(splits).forEach(num -> {
            System.out.print(num + " " + num.length() +"\n");
            if(num.length() != 0){
                strs.add(num);
            }
        });
        String str = "";
        for (int i = 0; i < strs.size(); i++) {
            str = str + strs.get(strs.size() - i - 1);
            if(i != strs.size() - 1){
                str += " ";
            }
        }
        System.out.println(str);
        return str;
    }
}
```



### 7 [除自身以外数组的乘积](https://leetcode.cn/problems/product-of-array-except-self/)

> 给你一个整数数组 nums，返回 数组 answer ，其中 answer[i] 等于 nums 中除 nums[i] 之外其余各元素的乘积 。
>
> 题目数据 保证 数组 nums之中任意元素的全部前缀元素和后缀的乘积都在  32 位 整数范围内。
>
> *请不要使用除法，且在 O(n) 时间复杂度内完成此题。*

 ```
 示例 1:
 输入: nums = [1,2,3,4]
 输出: [24,12,8,6]
 示例 2:
 输入: nums = [-1,1,0,-3,3]
 输出: [0,0,9,0,0]
 ```

**题解**

```java
public int[] productExceptSelf(int[] nums) {
    /**
         * 双指针: left 记录从左到右累乘的结果; right 记录从右到左累乘的结果
         * 在 [1,2,3,4] 数组中 index = 0 时. left 记录值为空, right 记录值为 2*3*4
         */
    int []arrs = new int[nums.length];
    for (int i = 0; i < nums.length; i++) {
        arrs[i] = 1;
    }
    int left = 1, right = 1;
    for (int i = 0; i < nums.length; i++) {
        arrs[i] *= left;
        left *= nums[i];

        arrs[nums.length - i - 1] *= right;
        right *= nums[nums.length - i - 1];
    }
    return arrs;
}
```



### 8 [递增的三元子序列](https://leetcode.cn/problems/increasing-triplet-subsequence/)

> 给你一个整数数组 nums ，判断这个数组中是否存在长度为 3 的递增子序列。
>
> 如果存在这样的三元组下标 (i, j, k) 且满足 i < j < k ，使得 nums[i] < nums[j] < nums[k] ，返回 true ；否则，返回 false 。

```
示例 1：

输入：nums = [1,2,3,4,5]
输出：true
解释：任何 i < j < k 的三元组都满足题意
示例 2：

输入：nums = [5,4,3,2,1]
输出：false
解释：不存在满足题意的三元组
示例 3：

输入：nums = [2,1,5,0,4,6]
输出：true
解释：三元组 (3, 4, 5) 满足题意，因为 nums[3] == 0 < nums[4] == 4 < nums[5] == 6
```



```java
class Solution {
    public boolean increasingTriplet(int[] nums) {
        //贪心算法: 使用变量暂存走过的路径; first 与 second
        if(nums.length < 3){
            return false;
        }
        int first = nums[0], second = Integer.MAX_VALUE;
        for (int i = 1; i < nums.length; i++) {
            ///如果当前值大于second, 代表找到了一条长度为3的通路
            if(nums[i] > second){
                return true;
            } 
            //如果值大于first, 代表找到了一个更小的值作为中点
            else if(nums[i] > first){
                second = nums[i];
            } 
            //如果值 < first, 代表找到了更小的值作为起点
            else{
                first = nums[i];
            }
        }
        return false;
    }
}
```

