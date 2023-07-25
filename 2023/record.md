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



### 9 [压缩字符串](https://leetcode.cn/problems/string-compression/)

> 给你一个字符数组 chars ，请使用下述算法压缩：
>
> 从一个空字符串 s 开始。对于 chars 中的每组 连续重复字符 ：
>
> 如果这一组长度为 1 ，则将字符追加到 s 中。
> 否则，需要向 s 追加字符，后跟这一组的长度。
> 压缩后得到的字符串 s 不应该直接返回 ，需要转储到字符数组 chars 中。需要注意的是，如果组长度为 10 或 10 以上，则在 chars 数组中会被拆分为多个字符。 请在修改完输入数组后 ，返回该数组的新长度。
>
> 你必须设计并实现一个只使用常量额外空间的算法来解决此问题。

 ```java
 示例 1：
 输入：chars = ["a","a","b","b","c","c","c"]
 输出：返回 6 ，输入数组的前 6 个字符应该是：["a","2","b","2","c","3"]
 解释："aa" 被 "a2" 替代。"bb" 被 "b2" 替代。"ccc" 被 "c3" 替代。
 示例 2：
 输入：chars = ["a"]
 输出：返回 1 ，输入数组的前 1 个字符应该是：["a"]
 解释：唯一的组是“a”，它保持未压缩，因为它是一个字符。
 示例 3：
 输入：chars = ["a","b","b","b","b","b","b","b","b","b","b","b","b"]
 输出：返回 4 ，输入数组的前 4 个字符应该是：["a","b","1","2"]。
 解释：由于字符 "a" 不重复，所以不会被压缩。"bbbbbbbbbbbb" 被 “b12” 替代。
 ```



**题解**

```java
    public static int compress(char[] chars) {
        if(chars.length == 1){
            return 1;
        }
        int []returned;
        int index = 0;
        for (int i = 0; i < chars.length; ) {
            returned = checkCount(chars, i);
            chars[index++] = chars[i];
            if(returned[0] > 1){
                char []charTemp = intToChar(returned[0]);
                for(int j = 0; j < charTemp.length; j++){
                    chars[index++] = charTemp[j];
                }
            }
            i += returned[0];
        }
        return index;
    }

    public static char[] intToChar(int num){
        ArrayList<Character> chars = new ArrayList<Character>();
        while(num >= 1){
            chars.add((char) ((char)num % 10 + '0'));
            num /= 10;
        }
        //翻转字符串
        char[] charTemp = new char[chars.size()];
        for (int i = 0; i < chars.size(); i++) {
            charTemp[i] = chars.get(chars.size() - i - 1);
        }
        System.out.println(charTemp);
        return charTemp;
    }



    public static int[] checkCount(char[] chars, int pre){
        int tail = pre + 1;
        int []returned = {1,0};
        for (int i = pre; i < chars.length; i++) {
            if(tail >= chars.length){
                break;
            }
            if(chars[pre] == chars[tail]){
                returned[0]++;
                tail++;
            } else{
                returned[1] = tail;
                break;
            }
        }
        System.out.println(returned[0] + " " + returned[1]);
        return returned;
    }
```



### 10 [移动零](https://leetcode.cn/problems/move-zeroes/)

> 给定一个数组 nums，编写一个函数将所有 0 移动到数组的末尾，同时保持非零元素的相对顺序。
>
> 请注意 ，必须在不复制数组的情况下原地对数组进行操作。

```
示例 1:
输入: nums = [0,1,0,3,12]
输出: [1,3,12,0,0]
示例 2:
输入: nums = [0]
输出: [0]
```

**题解**

```java
class Solution {
    public void moveZeroes(int[] nums) {
        //移动零 - 双指针
        //定义 pre tail
        int pre = 0, tail = nums.length - 1;
        while(pre < tail){
            while(pre < nums.length && nums[pre] != 0){
                pre++;
            }
            while(tail > 0 && nums[tail] == 0){
                tail--;
            }
            //整体前移
            for(int i = pre; i < tail; i++){
                nums[i] = nums[i+1];
            }
            if(pre < tail){
                nums[tail--] = 0;
            }
        }
    }
}
```



### 11 [判断子序列](https://leetcode.cn/problems/is-subsequence/)

> 给定字符串 s 和 t ，判断 s 是否为 t 的子序列。
>
> 字符串的一个子序列是原始字符串删除一些（也可以不删除）字符而不改变剩余字符相对位置形成的新字符串。（例如，"ace"是"abcde"的一个子序列，而"aec"不是）。
>
> 进阶：
>
> 如果有大量输入的 S，称作 S1, S2, ... , Sk 其中 k >= 10亿，你需要依次检查它们是否为 T 的子序列。在这种情况下，你会怎样改变代码？
>

```
示例 1：
输入：s = "abc", t = "ahbgdc"
输出：true
示例 2：
输入：s = "axc", t = "ahbgdc"
输出：false
```

**题解**

```java
class Solution {
    public boolean isSubsequence(String s, String t) {
        //双指针
        if(s.length()==0){
            return true;
        } else if(s.length()==1 && t.length()==1){
            return s.equals(t);
        } else if(s.length()==1){
            return t.contains(s);
        }
        char[] sc = s.toCharArray();
        char[] tc = t.toCharArray();
        char pre = sc[0], next = sc[1];
        int tag = 2;
        for(int i = 0; i < tc.length; i++){
            if(tc[i] == pre){
                pre = next;
                if(tag < sc.length){
                    next = sc[tag++];
                } else{
                    next = 'E';
                }
            }
        }
        if(pre == next && next == 'E' && pre == 'E'){
            return true;
        }
        return false;
    }
}
```



### 12 [盛最多水的容器](https://leetcode.cn/problems/container-with-most-water/)

> 给定一个长度为 n 的整数数组 height 。有 n 条垂线，第 i 条线的两个端点是 (i, 0) 和 (i, height[i]) 。
>
> 找出其中的两条线，使得它们与 x 轴共同构成的容器可以容纳最多的水。
>
> 返回容器可以储存的最大水量。
>
> 说明：你不能倾斜容器。

```
示例 1：
输入：[1,8,6,2,5,4,8,3,7]
输出：49 
解释：图中垂直线代表输入数组 [1,8,6,2,5,4,8,3,7]。在此情况下，容器能够容纳水（表示为蓝色部分）的最大值为 49。
示例 2：
输入：height = [1,1]
输出：1
```

**解答**

```java
class Solution {
    public int maxArea(int[] height) {
        //对撞指针: 维护最大值
        int max = Integer.MIN_VALUE;
        int pre = 0, tail = height.length - 1;
        System.out.println(tail);
        while(pre < tail){
            System.out.println(height[pre] + " " + height[tail]);
            if(height[pre] < height[tail]){
                max = Math.max(max, height[pre] * (tail - pre));
                pre++;
            } else if(height[pre] > height[tail]){
                max = Math.max(max, height[tail] * (tail - pre));
                tail--;
            } else{
                max = Math.max(max, height[tail] * (tail - pre));
                tail--;
            }
        }
        return max;
    }
}
```





## 哈希表

### 13 [找出两数组的不同](https://leetcode.cn/problems/find-the-difference-of-two-arrays/)

> 给你两个下标从 0 开始的整数数组 nums1 和 nums2 ，请你返回一个长度为 2 的列表 answer ，其中：
>
> answer[0] 是 nums1 中所有 不 存在于 nums2 中的 不同 整数组成的列表。
> answer[1] 是 nums2 中所有 不 存在于 nums1 中的 不同 整数组成的列表。
> 注意：列表中的整数可以按 任意 顺序返回。

```
示例 1：
输入：nums1 = [1,2,3], nums2 = [2,4,6]
输出：[[1,3],[4,6]]
解释：
对于 nums1 ，nums1[1] = 2 出现在 nums2 中下标 0 处，然而 nums1[0] = 1 和 nums1[2] = 3 没有出现在 nums2 中。因此，answer[0] = [1,3]。
对于 nums2 ，nums2[0] = 2 出现在 nums1 中下标 1 处，然而 nums2[1] = 4 和 nums2[2] = 6 没有出现在 nums2 中。因此，answer[1] = [4,6]。
示例 2：
输入：nums1 = [1,2,3,3], nums2 = [1,1,2,2]
输出：[[3],[]]
解释：
对于 nums1 ，nums1[2] 和 nums1[3] 没有出现在 nums2 中。由于 nums1[2] == nums1[3] ，二者的值只需要在 answer[0] 中出现一次，故 answer[0] = [3]。
nums2 中的每个整数都在 nums1 中出现，因此，answer[1] = [] 。 
```



**题解**

```java
class Solution {
    public List<List<Integer>> findDifference(int[] nums1, int[] nums2) {
        HashSet<Integer> set1 = new HashSet<Integer>();
        HashSet<Integer> set2 = new HashSet<Integer>();
        Arrays.stream(nums1).forEach(set1::add);
        Arrays.stream(nums2).forEach(set2::add);
        Arrays.stream(nums1).forEach(set2::remove);
        Arrays.stream(nums2).forEach(set1::remove);
        List<Integer> difference1 = new ArrayList<>(set1);
        List<Integer> difference2 = new ArrayList<>(set2);

        List<List<Integer>> result = new ArrayList<>();
        result.add(difference1);
        result.add(difference2);
        return result;
    }
}
```



### 14 [独一无二的出现次数](https://leetcode.cn/problems/unique-number-of-occurrences/)

> 给你一个整数数组 arr，请你帮忙统计数组中每个数的出现次数。
>
> 如果每个数的出现次数都是独一无二的，就返回 true；否则返回 false。
>

```
示例 1：
输入：arr = [1,2,2,1,1,3]
输出：true
解释：在该数组中，1 出现了 3 次，2 出现了 2 次，3 只出现了 1 次。没有两个数的出现次数相同。
示例 2：
输入：arr = [1,2]
输出：false
示例 3：
输入：arr = [-3,0,1,-3,1,1,1,-3,10,0]
输出：true
```



**题解**

```java
public boolean uniqueOccurrences(int[] arr) {
    //Hash 表
    HashMap<Integer, Integer> map = new HashMap<Integer, Integer>();
    for(int i = 0; i < arr.length; i++){
        //存放key, 存在则+1; 不存在默认为0
        map.put(arr[i], map.getOrDefault(arr[i], 0)+1);
    }
    //开辟set, 利用set的去重特性, 对次数进行去重
    HashSet<Integer> set = new HashSet<>();
    for(Map.Entry<Integer, Integer> entry : map.entrySet()){
        set.add(entry.getValue());
    }
    return set.size() == map.size();
}
```





## 队列

### 23 [最近的请求次数](https://leetcode.cn/problems/number-of-recent-calls/)

> 写一个 `RecentCounter` 类来计算特定时间范围内最近的请求。
>
> 请你实现 `RecentCounter` 类：
>
> - `RecentCounter()` 初始化计数器，请求数为 0 。
> - `int ping(int t)` 在时间 `t` 添加一个新请求，其中 `t` 表示以毫秒为单位的某个时间，并返回过去 `3000` 毫秒内发生的所有请求数（包括新请求）。确切地说，返回在 `[t-3000, t]` 内发生的请求数。
>
> **保证** 每次对 `ping` 的调用都使用比之前更大的 `t` 值。

**示例 1：**

```
输入：
["RecentCounter", "ping", "ping", "ping", "ping"]
[[], [1], [100], [3001], [3002]]
输出：
[null, 1, 2, 3, 3]

解释：
RecentCounter recentCounter = new RecentCounter();
recentCounter.ping(1);     // requests = [1]，范围是 [-2999,1]，返回 1
recentCounter.ping(100);   // requests = [1, 100]，范围是 [-2900,100]，返回 2
recentCounter.ping(3001);  // requests = [1, 100, 3001]，范围是 [1,3001]，返回 3
recentCounter.ping(3002);  // requests = [1, 100, 3001, 3002]，范围是 [2,3002]，返回 3
```

**题解**

> 实质上就是维护队列, 将队列头部`请求时间`不符合约束范围的数据`poll`出即可。

```java
class RecentCounter {
    Queue<Integer> queue;

    public RecentCounter() {
        queue = new ArrayDeque<Integer>();
    }

    public int ping(int t) {
        queue.add(t);
        // 时间 t 一定是递增的, 因此只需要判断队头是否超过了 [t-3000, t]
        while(queue.peek() < t - 3000){
            queue.poll();
        }
        return queue.size();
    }
}
```





## 栈

### 24 [从字符串中移除星号](https://leetcode.cn/problems/removing-stars-from-a-string/)

> 给你一个包含若干星号 `*` 的字符串 `s` 。
>
> 在一步操作中，你可以：
>
> - 选中 `s` 中的一个星号。
> - 移除星号 **左侧** 最近的那个 **非星号** 字符，并移除该星号自身。
>
> 返回移除 **所有** 星号之后的字符串**。**
>
> **注意：**
>
> - 生成的输入保证总是可以执行题面中描述的操作。
> - 可以证明结果字符串是唯一的。

**示例 1：**

```
输入：s = "leet**cod*e"
输出："lecoe"
解释：从左到右执行移除操作：
- 距离第 1 个星号最近的字符是 "leet**cod*e" 中的 't' ，s 变为 "lee*cod*e" 。
- 距离第 2 个星号最近的字符是 "lee*cod*e" 中的 'e' ，s 变为 "lecod*e" 。
- 距离第 3 个星号最近的字符是 "lecod*e" 中的 'd' ，s 变为 "lecoe" 。
不存在其他星号，返回 "lecoe" 。
```

**示例 2：**

```
输入：s = "erase*****"
输出：""
解释：整个字符串都会被移除，所以返回空字符串。
```

**题解**

```java
class Solution {
    public String removeStars(String s) {
        Stack stack = new Stack();
        for (int i = 0; i < s.length(); i++) {
            stack.push(s.charAt(i));
            //如果出现 '*' 字符, 则pop两个元素
            if((char)stack.peek() == '*'){
                stack.pop();
                stack.pop();
            }
        }
        StringBuilder sb = new StringBuilder();
        while(!stack.empty()){
            //直接拼接字符串
            sb.append(stack.pop());
        }
        //需要翻转, pop 出来的是逆序的
        return sb.reverse().toString();
    }
}
```



### 25 [行星碰撞](https://leetcode.cn/problems/asteroid-collision/)

> 给定一个整数数组 `asteroids`，表示在同一行的行星。
>
> 对于数组中的每一个元素，其绝对值表示行星的大小，正负表示行星的移动方向（正表示向右移动，负表示向左移动）。每一颗行星以相同的速度移动。
>
> 找出碰撞后剩下的所有行星。碰撞规则：两个行星相互碰撞，较小的行星会爆炸。如果两颗行星大小相同，则两颗行星都会爆炸。两颗移动方向相同的行星，永远不会发生碰撞。

**示例 1：**

```
输入：asteroids = [5,10,-5]
输出：[5,10]
解释：10 和 -5 碰撞后只剩下 10 。 5 和 10 永远不会发生碰撞。
```

**示例 2：**

```
输入：asteroids = [8,-8]
输出：[]
解释：8 和 -8 碰撞后，两者都发生爆炸。
```

**示例 3：**

```
输入：asteroids = [10,2,-5]
输出：[10]
解释：2 和 -5 发生碰撞后剩下 -5 。10 和 -5 发生碰撞后剩下 10 。
```

**题解**

```java
class Solution {
    public int[] asteroidCollision(int[] asteroids) {
        Stack<Integer> stack = new Stack<Integer>();
        for (int i = 0; i < asteroids.length; i++) {
            boolean live = true;
            //只有当右侧的行星值 < 0 才会发生碰撞
            if(asteroids[i] < 0){
                //可能发生循环相撞
               while(live && !stack.empty() && stack.peek() > 0){
                   //判定相撞的情形, 都损毁还是栈顶的行星被撞毁 live = true(只撞毁掉左侧行星)
                    live = stack.peek() < Math.abs(asteroids[i]);
                    if (stack.peek() <= Math.abs(asteroids[i])) {
                        stack.pop();
                    }
               }
               //live = false(都被撞毁)
                if(live){
                    stack.push(asteroids[i]);
                }
            } 
            // > 0 时则会直接飞出 | 平行飞行, 因此push进栈
            else {
                stack.push(asteroids[i]);
            }
        }

        int []arrs = new int[stack.size()];
        int i = 0;
        while(!stack.isEmpty()){
            arrs[arrs.length - i - 1] = (int)stack.pop();
            i++;
        }
        return arrs;
    }
}
```









## 链表

### 15 [删除链表的中间节点](https://leetcode.cn/problems/delete-the-middle-node-of-a-linked-list/)

> 给你一个链表的头节点 head 。删除 链表的 中间节点 ，并返回修改后的链表的头节点 head 。
>
> 长度为 n 链表的中间节点是从头数起第 ⌊n / 2⌋ 个节点（下标从 0 开始），其中 ⌊x⌋ 表示小于或等于 x 的最大整数。
>
> 对于 n = 1、2、3、4 和 5 的情况，中间节点的下标分别是 0、1、1、2 和 2 (向下取整)。

```
输入：head = [1,3,4,7,1,2,6]
输出：[1,3,4,1,2,6]
解释：
上图表示给出的链表。节点的下标分别标注在每个节点的下方。
由于 n = 7 ，值为 7 的节点 3 是中间节点，用红色标注。
返回结果为移除节点后的新链表。 

输入：head = [1,2,3,4]
输出：[1,2,4]
解释：
上图表示给出的链表。
对于 n = 4 ，值为 3 的节点 2 是中间节点，用红色标注。
输入：head = [2,1]
输出：[2]
解释：
上图表示给出的链表。
对于 n = 2 ，值为 1 的节点 1 是中间节点，用红色标注。
值为 2 的节点 0 是移除节点 1 后剩下的唯一一个节点。
```



**题解**

```java
class Solution {
    public ListNode deleteMiddle(ListNode head) {
        //首先获取整个链表的长度
        ListNode temp = head;
        int size = 0;
        while(temp != null){
            size++;
            temp = temp.next;
        }
        if(size == 1){
            return null;
        }
        //准备删除
        int index = size/2;
        System.out.println(index);
        System.out.println(size);
        temp = head;
        while(temp != null){
            if(index == 1){
                temp.next = temp.next.next;
            }
            index--;
            temp = temp.next;
        }
        return head;
    }
}
```



### 16 [ 奇偶链表](https://leetcode.cn/problems/odd-even-linked-list/)

> 给定单链表的头节点 head ，将所有索引为奇数的节点和索引为偶数的节点分别组合在一起，然后返回重新排序的列表。
>
> 第一个节点的索引被认为是 奇数 ， 第二个节点的索引为 偶数 ，以此类推。
>
> 请注意，偶数组和奇数组内部的相对顺序应该与输入时保持一致。
>
> 你必须在 O(1) 的额外空间复杂度和 O(n) 的时间复杂度下解决这个问题。
>

```
示例 1:
输入: head = [1,2,3,4,5]
输出: [1,3,5,2,4]
示例 2:
输入: head = [2,1,3,5,6,4,7]
输出: [2,3,6,7,1,5,4]
```

**题解**

```java
class Solution {
    public ListNode oddEvenList(ListNode head) {
        if (head == null) {
            return head;
        }
        //声明2个链表, 1存放奇数, 2存放偶数 - 带头结点方式
        ListNode node1 = new ListNode();
        ListNode node2 = new ListNode();

        ListNode node1_head = node1;
        ListNode node2_head = node2;
        int tag = 1;
        while(head != null){
            ListNode temp = new ListNode();
            temp = head;
            if(tag % 2 == 1){
                node1.next = temp;
                node1 = node1.next;
            } else if(tag % 2 == 0){
                node2.next = temp;
                node2 = node2.next;
            }
            head = head.next;
            tag++;
        }
        //拼接链表
        node2.next = null;
        node1.next = node2_head.next;
        return node1_head.next;        
    }
}
```



### 17 [反转链表](https://leetcode.cn/problems/reverse-linked-list/)

> 给你单链表的头节点 `head` ，请你反转链表，并返回反转后的链表。

```
输入：head = [1,2,3,4,5]
输出：[5,4,3,2,1]

输入：head = [1,2]
输出：[2,1]

输入：head = []
输出：[]
```

**题解**

```java
class Solution {
    public ListNode reverseList(ListNode head) {
        //直接开辟空间, 用数组来处理
        ArrayList<Integer> arrayList = new ArrayList<>();
        ListNode temp = head;
        while(temp != null){
            arrayList.add(temp.val);
            temp = temp.next;
        }
        temp = head;
        for (int i = 0; i < arrayList.size(); i++) {
            temp.val = arrayList.get(arrayList.size() - i - 1);
            temp = temp.next;
        }
        return head;
    }
}
```



## 二分查找

### 18 猜数字

> 猜数字游戏的规则如下：
>
> 每轮游戏，我都会从 1 到 n 随机选择一个数字。 请你猜选出的是哪个数字。
> 如果你猜错了，我会告诉你，你猜测的数字比我选出的数字是大了还是小了。
> 你可以通过调用一个预先定义好的接口 int guess(int num) 来获取猜测结果，返回值一共有 3 种可能的情况（-1，1 或 0）：
>
> -1：我选出的数字比你猜的数字小 pick < num
> 1：我选出的数字比你猜的数字大 pick > num
> 0：我选出的数字和你猜的数字一样。恭喜！你猜对了！pick == num
> 返回我选出的数字。

 ```
 示例 1：
 输入：n = 10, pick = 6
 输出：6
 示例 2：
 输入：n = 1, pick = 1
 输出：1
 示例 3：
 输入：n = 2, pick = 1
 输出：1
 示例 4：
 输入：n = 2, pick = 2
 输出：2
 ```



**题解**

```java
public class Solution extends GuessGame {
    public int guessNumber(int n) {
        int pre = 1, tail = n, mid = -1;
        while(pre <= tail){
            mid = pre +(tail - pre)/2; ;
            if(guess(mid) == 0){
                return mid;
            } else if(guess(mid) == -1){
                tail = mid - 1;
            } else if(guess(mid) == 1){
                pre = mid + 1;
            }
        }
        return mid;
    }
}
```



## 滑动窗口

### 19 [子数组最大平均数 I](https://leetcode.cn/problems/maximum-average-subarray-i/)

> 给你一个由 `n` 个元素组成的整数数组 `nums` 和一个整数 `k` 。
>
> 请你找出平均数最大且 **长度为 `k`** 的连续子数组，并输出该最大平均数。
>
> 任何误差小于 `10-5` 的答案都将被视为正确答案。

**示例 1：**

```
输入：nums = [1,12,-5,-6,50,3], k = 4
输出：12.75
解释：最大平均数 (12-5-6+50)/4 = 51/4 = 12.75
```

**示例 2：**

```
输入：nums = [5], k = 1
输出：5.00000
```

**题解**

```java
class Solution {
    public static double findMaxAverage(int[] nums, int k) {
        int temp = 0;
        if(nums.length < 4){
            for (int i = 0; i < nums.length; i++) {
                temp += nums[i];
            }
            return (double)temp/k;
        }

        //滑动窗口: 定义窗口 windows = k
        //初始化窗口
        int max = 0;
        for(int i = 0; i < k; i++){
            max += nums[i];
        }
        //间接变量, 用于判定是否交换窗口值
        temp = max;
        for(int i = 1; i < nums.length - k + 1; i++){
            temp -= nums[i-1];
            temp += nums[k+i-1];
            if(temp > max){
                max = temp;
            }
        }
        return (double)max/k;
    }
}
```



### 20 [最大连续1的个数 III](https://leetcode.cn/problems/max-consecutive-ones-iii/)

> 给定一个二进制数组 `nums` 和一个整数 `k`，如果可以翻转最多 `k` 个 `0` ，则返回 *数组中连续 `1` 的最大个数* 。
>
> notes:
>
> ​	维护了左右指针以及限定条件, 通过左右指针边界的移动以及区间内条件满足情况缩小左边界|右边界, 同时维护最优值来求解。

**示例 1：**

```
输入：nums = [1,1,1,0,0,0,1,1,1,1,0], K = 2
输出：6
解释：[1,1,1,0,0,1,1,1,1,1,1]
粗体数字从 0 翻转到 1，最长的子数组长度为 6。
```

**示例 2：**

```
输入：nums = [0,0,1,1,0,0,1,1,1,0,1,1,0,0,0,1,1,1,1], K = 3
输出：10
解释：[0,0,1,1,1,1,1,1,1,1,1,1,0,0,0,1,1,1,1]
粗体数字从 0 翻转到 1，最长的子数组长度为 10。
```

**题解**

```java
class Solution {
    public int longestOnes(int[] nums, int k) {
        //滑动窗口 + 双指针
        int left = 0, right = 0;
        int zeros = 0;
        int max = 0;
        while(right < nums.length){
            if(nums[right] == 0){
                zeros++;
            }

            while(zeros > k){
                if(nums[left] == 0){
                    zeros--;
                }
                left++;
            }
            max = Math.max(right-left+1, max);
            right++;
        }
        return max;
    }
}
```

**模板**

```python
def findSubArray(nums):
    N = len(nums) # 数组/字符串长度
    left, right = 0, 0 # 双指针，表示当前遍历的区间[left, right]，闭区间
    sums = 0 # 用于统计 子数组/子区间 是否有效，根据题目可能会改成求和/计数
    res = 0 # 保存最大的满足题目要求的 子数组/子串 长度
    while right < N: # 当右边的指针没有搜索到 数组/字符串 的结尾
        sums += nums[right] # 增加当前右边指针的数字/字符的求和/计数
        while 区间[left, right]不符合题意: # 此时需要一直移动左指针，直至找到一个符合题意的区间
            sums -= nums[left] # 移动左指针前需要从counter中减少left位置字符的求和/计数
            left += 1 # 真正的移动左指针，注意不能跟上面一行代码写反
        # 到 while 结束时，我们找到了一个符合题意要求的 子数组/子串
        res = max(res, right - left + 1) # 需要更新结果
        right += 1 # 移动右指针，去探索新的区间
    return res
```





## 前缀和

### 21 [找到最高海拔](https://leetcode.cn/problems/find-the-highest-altitude/)

> 有一个自行车手打算进行一场公路骑行，这条路线总共由 `n + 1` 个不同海拔的点组成。自行车手从海拔为 `0` 的点 `0` 开始骑行。
>
> 给你一个长度为 `n` 的整数数组 `gain` ，其中 `gain[i]` 是点 `i` 和点 `i + 1` 的 **净海拔高度差**（`0 <= i < n`）。请你返回 **最高点的海拔** 。

**示例 1：**

```
输入：gain = [-5,1,5,0,-7]
输出：1
解释：海拔高度依次为 [0,-5,-4,1,1,-6] 。最高海拔为 1 。
```

**示例 2：**

```
输入：gain = [-4,-3,-2,-1,4,3,2]
输出：0
解释：海拔高度依次为 [0,-4,-7,-9,-10,-6,-3,-1] 。最高海拔为 0 。
```

**题解**

```java
class Solution {
    public int largestAltitude(int[] gain) {
        int max = Integer.MIN_VALUE;
        int temp = 0;
        for (int i = 0; i < gain.length; i++) {
            temp += gain[i];
            max = Math.max(max, temp);
        }
        return Math.max(max, 0);
    }
}
```



### 22 [寻找数组的中心下标](https://leetcode.cn/problems/find-pivot-index/)

> 给你一个整数数组 `nums` ，请计算数组的 **中心下标** 。
>
> 数组 **中心下标** 是数组的一个下标，其左侧所有元素相加的和等于右侧所有元素相加的和。
>
> 如果中心下标位于数组最左端，那么左侧数之和视为 `0` ，因为在下标的左侧不存在元素。这一点对于中心下标位于数组最右端同样适用。
>
> 如果数组有多个中心下标，应该返回 **最靠近左边** 的那一个。如果数组不存在中心下标，返回 `-1` 。

**示例 1：**

```
输入：nums = [1, 7, 3, 6, 5, 6]
输出：3
解释：
中心下标是 3 。
左侧数之和 sum = nums[0] + nums[1] + nums[2] = 1 + 7 + 3 = 11 ，
右侧数之和 sum = nums[4] + nums[5] = 5 + 6 = 11 ，二者相等。
```

**示例 2：**

```
输入：nums = [1, 2, 3]
输出：-1
解释：
数组中不存在满足此条件的中心下标。
```

**示例 3：**

```
输入：nums = [2, 1, -1]
输出：0
解释：
中心下标是 0 。
左侧数之和 sum = 0 ，（下标 0 左侧不存在元素），
右侧数之和 sum = nums[1] + nums[2] = 1 + -1 = 0 。
```

**题解**

```java
class Solution {
    public int pivotIndex(int[] nums) {
        //利用滑动窗口的思想
        //定义双指针
        int left = nums[0], right = 0;
        for(int i = 1; i < nums.length; i++){
            right += nums[i];
        }
        if(right == 0){
            return 0;
        }
        //开始滑动判断
        for(int i = 1; i < nums.length; i++){
            right -= nums[i];
            if(right == left){
                return i;
            }
            left += nums[i];
        }
        return -1;
    }
}
```



## 位运算

### 26 [比特位计数](https://leetcode.cn/problems/counting-bits/)

> 给你一个整数 `n` ，对于 `0 <= i <= n` 中的每个 `i` ，计算其二进制表示中 **`1` 的个数** ，返回一个长度为 `n + 1` 的数组 `ans` 作为答案。

**示例 1：**

```
输入：n = 2
输出：[0,1,1]
解释：
0 --> 0
1 --> 1
2 --> 10
```

**示例 2：**

```
输入：n = 5
输出：[0,1,1,2,1,2]
解释：
0 --> 0
1 --> 1
2 --> 10
3 --> 11
4 --> 100
5 --> 101
```

**题解**

```java
class Solution {
    public int[] countBits(int n) {
        int []arrs = new int[n+1];
        arrs[0] = 0;
        for(int i = 1; i <= n; i++){
            if((i & 1) == 1){
                arrs[i] = arrs[i-1] + 1;
            } else {
                arrs[i] = arrs[i >> 1];
            }
        }
        return arrs;
    }
}
```



### 27 [只出现一次的数字](https://leetcode.cn/problems/single-number/)

给你一个 **非空** 整数数组 `nums` ，除了某个元素只出现一次以外，其余每个元素均出现两次。找出那个只出现了一次的元素。

你必须设计并实现线性时间复杂度的算法来解决此问题，且该算法只使用常量额外空间。

**示例 1 ：**

```
输入：nums = [2,2,1]
输出：1
```

**示例 2 ：**

```
输入：nums = [4,1,2,1,2]
输出：4
```

**示例 3 ：**

```
输入：nums = [1]
输出：1
```

**题解**

```java
class Solution {
    public int singleNumber(int[] nums) {
        //排序
        Arrays.sort(nums);
        //Arrays.stream(nums).forEach(System.out::println);
        //双指针遍历
        int pre = 0, next = 1;
        while(next < nums.length){
            if(nums[next] != nums[pre]){
                return nums[pre];
            }
            pre+=2;
            next+=2;
            if(next >= nums.length){
                break;
            }
        }
        return nums[pre];
    }
}
```

