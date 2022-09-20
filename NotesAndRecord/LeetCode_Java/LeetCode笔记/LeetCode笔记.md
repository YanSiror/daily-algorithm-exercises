# 数组

## 1 、删除排序数组中的重复项

给你一个 升序排列 的数组 nums ，请你 原地 删除重复出现的元素，使每个元素 只出现一次 ，返回删除后数组的新长度。元素的 相对顺序 应该保持 一致 。

由于在某些语言中不能改变数组的长度，所以必须将结果放在数组nums的第一部分。更规范地说，如果在删除重复项之后有 k 个元素，那么 nums 的前 k 个元素应该保存最终结果。

将最终结果插入 nums 的前 k 个位置后返回 k 。

不要使用额外的空间，你必须在 原地 修改输入数组 并在使用 O(1) 额外空间的条件下完成。

**示例 1：**

```
输入：nums = [1,1,2]
输出：2, nums = [1,2,_]
解释：函数应该返回新的长度 2 ，并且原数组 nums 的前两个元素被修改为 1, 2 。不需要考虑数组中超出新长度后面的元素。
```

**示例 2：**

```
输入：nums = [0,0,1,1,1,2,2,3,3,4]
输出：5, nums = [0,1,2,3,4]
解释：函数应该返回新的长度 5 ， 并且原数组 nums 的前五个元素被修改为 0, 1, 2, 3, 4 。不需要考虑数组中超出新长度后面的元素。
```

**提示：**

>1 <= nums.length <= 3 * 104
>-104 <= nums[i] <= 104
>nums 已按 升序 排列

**代码:**

```java
class Solution {
    public int removeDuplicates(int[] nums) {
        int pre = nums[0];
        int count = nums.length;
        for(int i = 1; i < count; i++){
            if(nums[i] == pre){
                //处理重复的
                for(int j = i; j < nums.length - 1; j++){
                    nums[j] = nums[j+1];
                }
                i--;
                count--;
            } else {
                pre = nums[i];
            }
        }
        return count;
    }
}
```



## 2、买卖股票的最佳时机 II

给你一个整数数组 prices ，其中 prices[i] 表示某支股票第 i 天的价格。在每一天，你可以决定是否购买和/或出售股票。你在任何时候 最多 只能持有 一股 股票。你也可以先购买，然后在 同一天 出售。

返回 你能获得的 最大 利润 。

 

**示例 1：**

```
输入：prices = [7,1,5,3,6,4]
输出：7
解释：在第 2 天（股票价格 = 1）的时候买入，在第 3 天（股票价格 = 5）的时候卖出, 这笔交易所能获得利润 = 5 - 1 = 4 。
     随后，在第 4 天（股票价格 = 3）的时候买入，在第 5 天（股票价格 = 6）的时候卖出, 这笔交易所能获得利润 = 6 - 3 = 3 。
     总利润为 4 + 3 = 7 。
```

**示例 2：**

```
输入：prices = [1,2,3,4,5]
输出：4
解释：在第 1 天（股票价格 = 1）的时候买入，在第 5 天 （股票价格 = 5）的时候卖出, 这笔交易所能获得利润 = 5 - 1 = 4 。
     总利润为 4 。
```

**示例 3：**

```
输入：prices = [7,6,4,3,1]
输出：0
解释：在这种情况下, 交易无法获得正利润，所以不参与交易可以获得最大利润，最大利润为 0 。
```

**提示：**

>1 <= prices.length <= 3 * 104
>0 <= prices[i] <= 104

**代码**

```java
    public int maxProfit(int[] prices) {
        //贪心算法
        if(prices.length < 2)
            return 0;
        int length = prices.length;
        int min = 0,max = 0,index = 0,sum = 0;
        for(int i = 0; i < length; i++){
            while(index < length - 1 && prices[index] >= prices[index+1])
                index++;
            min = prices[index];
            while(index < length - 1 && prices[index] <= prices[index+1])
                index++;
            max = prices[index];
            sum += max - min;
        }
        return sum;
    }
```



## 3、旋转数组
给你一个数组，将数组中的元素向右轮转 k 个位置，其中 k 是非负数。

**示例 1:**

```
输入: nums = [1,2,3,4,5,6,7], k = 3
输出: [5,6,7,1,2,3,4]
解释:
向右轮转 1 步: [7,1,2,3,4,5,6]
向右轮转 2 步: [6,7,1,2,3,4,5]
向右轮转 3 步: [5,6,7,1,2,3,4]
```

**示例 2:**

```
输入：nums = [-1,-100,3,99], k = 2
输出：[3,99,-1,-100]
解释: 
向右轮转 1 步: [99,-1,-100,3]
向右轮转 2 步: [3,99,-1,-100]
```

**提示：**

>1 <= nums.length <= 105
>-231 <= nums[i] <= 231 - 1
>0 <= k <= 105

**代码**

```java
    public static void rotate(int[] nums, int k) {
        //实质上就是取模调换位置
        int [] indexs = new int[nums.length];
        for(int i = 0; i < nums.length; i++){
            indexs[i] = (i+k) % nums.length;
        }
        int [] result = new int[indexs.length];
        for(int i = 0; i < nums.length; i++){
            result[indexs[i]] = nums[i];
        }
        //赋值回去
        for (int i = 0; i < nums.length; i++) {
            nums[i] = result[i];
        }
    }
```



## 4、存在重复元素

给你一个整数数组 nums 。如果任一值在数组中出现 至少两次 ，返回 true ；如果数组中每个元素互不相同，返回 false 。

**示例 1：**

```
输入：nums = [1,2,3,1]
输出：true
```

**示例 2：**

```
输入：nums = [1,2,3,4]
输出：false
```

**示例 3：**

```
输入：nums = [1,1,1,3,3,4,3,2,4,2]
输出：true
```

**提示：**

>1 <= nums.length <= 105
>-109 <= nums[i] <= 109

**代码**

```java
    public boolean containsDuplicate(int[] nums) {
        Arrays.sort(nums);
        for(int i = 1; i < nums.length; i++){
            if(nums[i-1] == nums[i])
                return true;
        }
        return false;
    }
```



## 5、只出现一次的数字
给定一个非空整数数组，除了某个元素只出现一次以外，其余每个元素均出现两次。找出那个只出现了一次的元素。

说明：

你的算法应该具有线性时间复杂度。 你可以不使用额外空间来实现吗？

**示例 1:**

```
输入: [2,2,1]
输出: 1
```

**示例 2:**

```
输入: [4,1,2,1,2]
输出: 4
```

**代码**

```java
    public int singleNumber(int[] nums) {
        Arrays.sort(nums);
        for(int i = 1; i < nums.length; i+=2){
            if(nums[i-1] == nums[i])
                nums[i] = nums[i-1] = -10;
        }
        for(int i = 0; i < nums.length; i++)
            if(nums[i] != -10)
                return nums[i];
        return nums.length == 1 ? nums[0] : 0;
    }
```



## 6、两个数组的交集 II
给你两个整数数组 nums1 和 nums2 ，请你以数组形式返回两数组的交集。返回结果中每个元素出现的次数，应与元素在两个数组中都出现的次数一致（如果出现次数不一致，则考虑取较小值）。可以不考虑输出结果的顺序。

**示例 1：**

```
输入：nums1 = [1,2,2,1], nums2 = [2,2]
输出：[2,2]
```

**示例 2:**

```
输入：nums1 = [4,9,5], nums2 = [9,4,9,8,4]
输出：[4,9]
```


**提示：**

>1 <= nums1.length, nums2.length <= 1000
>0 <= nums1[i], nums2[i] <= 1000

**代码**

```java
    public int[] intersect(int[] nums1, int[] nums2) {
        //暴力
        int [] result = new int[nums1.length > nums2.length ? nums1.length : nums2.length];
        if(nums1.length == 0 || nums2.length == 0)
            return result;
        Arrays.sort(nums1);
        Arrays.sort(nums2);
        int i = 0,j = 0,k = 0;
        while(i < nums1.length && j < nums2.length){
            if(nums1[i] == nums2[j]){
                result[k++] = nums1[i];
                i++;
                j++;
            }else if(nums1[i] < nums2[j]){
                i++;
            }else{
                j++;
            }
        }
        return Arrays.copyOfRange(result,0,k);
    }
```



## 7、加一



给定一个由 整数 组成的 非空 数组所表示的非负整数，在该数的基础上加一。最高位数字存放在数组的首位， 数组中每个元素只存储单个数字。

你可以假设除了整数 0 之外，这个整数不会以零开头。

 

**示例 1：**

```
输入：digits = [1,2,3]
输出：[1,2,4]
解释：输入数组表示数字 123。
```

**示例 2：**

```
输入：digits = [4,3,2,1]
输出：[4,3,2,2]
解释：输入数组表示数字 4321。
```

**示例 3：**

```
输入：digits = [0]
输出：[1]
```

**提示：**

>1 <= digits.length <= 100
>0 <= digits[i] <= 9

**代码**

```java
    public int[] plusOne(int[] digits) {
        if(digits[digits.length - 1] + 1 != 10){
            digits[digits.length - 1]++;
            return digits;
        }


        int [] result = new int[digits.length + 1];
        result[0] = 0;
        for(int i = 0; i < digits.length; i++){
            result[i+1] = digits[i];
        }

        int i = 0;
        for(i = result.length - 1; i >= 0; i--){
            if(result[i] + 1 == 10){
                result[i] = 0;
            } else{
                break;
            }
        }
        result[i] += 1;

        //赋值
        if(result[0] == 0){
            for(i = 0; i < digits.length; i++){
                digits[i] = result[i+1];
            }
            return digits;
        }
        return result;
    }
```



## 8、移动零

给定一个数组 nums，编写一个函数将所有 0 移动到数组的末尾，同时保持非零元素的相对顺序。

请注意 ，必须在不复制数组的情况下原地对数组进行操作。

**示例 1:**

```
输入: nums = [0,1,0,3,12]
输出: [1,3,12,0,0]
```

**示例 2:**

```
输入: nums = [0]
输出: [0]
```


**提示:**

```
1 <= nums.length <= 104
-231 <= nums[i] <= 231 - 1
```

**代码**

```java
    public void moveZeroes(int[] nums) {
        if(nums.length == 1)
            return;
        //记录0的个数
        int count = 0;
        int [] res = new int[nums.length];
        int k = 0;
        for(int i = 0; i < nums.length; i++){
            if(nums[i] == 0)
                count++;
            else{
                res[k++] = nums[i];
            }
        }
      //移动元素
        for(int i = 0; i < nums.length && res[i] != 0; i++){
            nums[i] = res[i];
        }
        //补0
        for (int i = 0; i < count; i++) {
            nums[nums.length - i - 1] = 0;
        }
    }
```



## 9、两数之和
给定一个整数数组 nums 和一个整数目标值 target，请你在该数组中找出 和为目标值 target  的那 两个 整数，并返回它们的数组下标。

你可以假设每种输入只会对应一个答案。但是，数组中同一个元素在答案里不能重复出现。

你可以按任意顺序返回答案。

**示例 1：**

输入：nums = [2,7,11,15], target = 9
输出：[0,1]
解释：因为 nums[0] + nums[1] == 9 ，返回 [0, 1] 。
**示例 2：**

输入：nums = [3,2,4], target = 6
输出：[1,2]
**示例 3：**

输入：nums = [3,3], target = 6
输出：[0,1]

**提示：**

>2 <= nums.length <= 104
>-109 <= nums[i] <= 109
>-109 <= target <= 109
>
>只会存在一个有效答案

**代码**

```java
    public int[] twoSum(int[] nums, int target) {
        for(int i = 0; i < nums.length - 1; i++){
            for(int j = i + 1; j < nums.length; j++){
                if(nums[i] + nums[j] == target){
                    return new int[]{i,j};
                }
            }
        }
        return nums;
    }
```



## 10、有效的数独

请你判断一个 9 x 9 的数独是否有效。只需要 根据以下规则 ，验证已经填入的数字是否有效即可。

- 数字 1-9 在每一行只能出现一次。
- 数字 1-9 在每一列只能出现一次。
- 数字 1-9 在每一个以粗实线分隔的 3x3 宫内只能出现一次。（请参考示例图）


注意：

一个有效的数独（部分已被填充）不一定是可解的。
只需要根据以上规则，验证已经填入的数字是否有效即可。
空白格用 '.' 表示。

**示例 1：**

```
输入：board = 
[["5","3",".",".","7",".",".",".","."]
,["6",".",".","1","9","5",".",".","."]
,[".","9","8",".",".",".",".","6","."]
,["8",".",".",".","6",".",".",".","3"]
,["4",".",".","8",".","3",".",".","1"]
,["7",".",".",".","2",".",".",".","6"]
,[".","6",".",".",".",".","2","8","."]
,[".",".",".","4","1","9",".",".","5"]
,[".",".",".",".","8",".",".","7","9"]]
输出：true
```

**示例 2：**

```
输入：board = 
[["8","3",".",".","7",".",".",".","."]
,["6",".",".","1","9","5",".",".","."]
,[".","9","8",".",".",".",".","6","."]
,["8",".",".",".","6",".",".",".","3"]
,["4",".",".","8",".","3",".",".","1"]
,["7",".",".",".","2",".",".",".","6"]
,[".","6",".",".",".",".","2","8","."]
,[".",".",".","4","1","9",".",".","5"]
,[".",".",".",".","8",".",".","7","9"]]
输出：false
解释：除了第一行的第一个数字从 5 改为 8 以外，空格内其他数字均与 示例1 相同。 但由于位于左上角的 3x3 宫内有两个 8 存在, 因此这个数独是无效的。
```


提示：

>board.length == 9
>board[i].length == 9
>board[i][j] 是一位数字（1-9）或者 '.'





**代码**

```java
    public boolean isValidSudoku(char board[][]) {
        int length = board.length;
        //二维数组line表示的是对应的行中是否有对应的数字，比如line[0][3]
        //表示的是第0行（实际上是第1行，因为数组的下标是从0开始的）是否有数字3
        int line[][] = new int[length][length];
        int column[][] = new int[length][length];
        int cell[][] = new int[length][length];
        for (int i = 0; i < length; ++i)
            for (int j = 0; j < length; ++j) {
                //如果还没有填数字，直接跳过
                if (board[i][j] == '.')
                    continue;
                //num是当前格子的数字
                int num = board[i][j] - '0' - 1;
                //k是第几个单元格，9宫格数独横着和竖着都是3个单元格
                int k = i / 3 * 3 + j / 3;
                //如果当前数字对应的行和列以及单元格，只要一个由数字，说明冲突了，直接返回false。
                //举个例子，如果line[i][num]不等于0，说明第i（i从0开始）行有num这个数字。
                if (line[i][num] != 0 || column[j][num] != 0 || cell[k][num] != 0)
                    return false;
                //表示第i行有num这个数字，第j列有num这个数字，对应的单元格内也有num这个数字
                line[i][num] = column[j][num] = cell[k][num] = 1;
            }
        return true;
    }
```



## 11、旋转图像

给定一个 n × n 的二维矩阵 matrix 表示一个图像。请你将图像顺时针旋转 90 度。

你必须在 原地 旋转图像，这意味着你需要直接修改输入的二维矩阵。请不要 使用另一个矩阵来旋转图像。

![image-20220916124356040](C:\Users\yanjing\Desktop\LeetCode_Java\LeetCode笔记\imgs\image-20220916124356040.png)



**代码**

```java
    public void rotate(int[][] matrix) {
        int length = matrix.length;
        //先上下交换
        for (int i = 0; i < length / 2; i++) {
            int temp[] = matrix[i];
            matrix[i] = matrix[length - i - 1];
            matrix[length - i - 1] = temp;
        }
        //在按照对角线交换
        for (int i = 0; i < length; ++i) {
            for (int j = i + 1; j < length; ++j) {
                int temp = matrix[i][j];
                matrix[i][j] = matrix[j][i];
                matrix[j][i] = temp;
            }
        }
    }
```

---



# 字符串

## 1、翻转字符串

编写一个函数，其作用是将输入的字符串反转过来。输入字符串以字符数组 s 的形式给出。

不要给另外的数组分配额外的空间，你必须原地修改输入数组、使用 O(1) 的额外空间解决这一问题。

**示例 1：**

```
输入：s = ["h","e","l","l","o"]
输出：["o","l","l","e","h"]
```

**示例 2：**

```
输入：s = ["H","a","n","n","a","h"]
输出：["h","a","n","n","a","H"]
```

**提示：**

>1 <= s.length <= 105
>s[i] 都是 ASCII 码表中的可打印字符



**代码**

```java
    public void reverseString(char[] s) {
        for (int i = 0; i < s.length/2; i++) {
            char c = s[i];
            s[i] = s[s.length - i - 1];
            s[s.length - i - 1] = c;
        }
    }
```



## 2、整数反转

给你一个 32 位的有符号整数 x ，返回将 x 中的数字部分反转后的结果。

如果反转后整数超过 32 位的有符号整数的范围 [−231,  231 − 1] ，就返回 0。

假设环境不允许存储 64 位整数（有符号或无符号）。

**示例 1：**

```
输入：x = 123
输出：321
```

**示例 2：**

```
输入：x = -123
输出：-321
```

**示例 3：**

```
输入：x = 120
输出：21
```

**示例 4：**

```
输入：x = 0
输出：0
```


提示：

>-231 <= x <= 231 - 1

**代码**

```java
    public static int reverse(int x) {
        long res = 0;
        while(x != 0){
            res = res * 10 + x % 10;
            x /= 10;
        }
        if(res >Integer.MAX_VALUE || res < Integer.MIN_VALUE) return 0;
        return (int)res;
    }
```



## 3、字符串中的第一个唯一字符

 给定一个字符串 s ，找到 它的第一个不重复的字符，并返回它的索引 。如果不存在，则返回 -1 。

**示例 1：**

```
输入: s = "leetcode"
输出: 0
```

**示例 2:**

```
输入: s = "loveleetcode"
输出: 2
```

**示例 3:**

```
输入: s = "aabb"
输出: -1
```




提示:

>1 <= s.length <= 105
>s 只包含小写字母

**代码**

```java
public int firstUniqChar(String s) {
        //哈希表
        int [] a = new int[26];
        int [] b = new int[26];
        //初始化
        for(int i = 0; i < b.length; i++){
            a[i] = 0;
            b[i] = 0;
        }

        for (int i = 0; i < s.length(); i++) {
            a[s.charAt(i) - 'a']++;        //记录出现次数
            b[s.charAt(i) - 'a'] = i;      //记录先后
        }


        for(int i=0;i<s.length();i++)
        {
            if(a[s.charAt(i)-'a']==1)
            {
                return b[s.charAt(i)-'a'];
            }
        }
        return -1;
    }
```





## 4、有效的字母异位词

给定两个字符串 s 和 t ，编写一个函数来判断 t 是否是 s 的字母异位词。

注意：若 s 和 t 中每个字符出现的次数都相同，则称 s 和 t 互为字母异位词。

**示例 1:**

```
输入: s = "anagram", t = "nagaram"
输出: true
```

**示例 2:**

```
输入: s = "rat", t = "car"
输出: false
```

**代码**

```java
    public boolean isAnagram(String s, String t) {
        if(s.length() != t.length())
            return false;
        //哈希表解法
        int []a = new int[26];
        int []b = new int[26];
        Arrays.fill(a, 0);
        Arrays.fill(b, 0);
        for(int i = 0; i < s.length(); i++)
            a[s.charAt(i) - 'a']++;
        for(int i = 0; i < t.length(); i++)
            b[t.charAt(i) - 'a']++;

        for(int i = 0; i < 26; i++)
            if(a[i] != b[i])
                return false;
        return true;
    }
```









# 链表

## 1、删除链表的倒数第N个节点

**示例 1:**

```
输入：head = [1,2,3,4,5], n = 2
输出：[1,2,3,5]
```

**示例 2：**

```
输入：head = [1], n = 1
输出：[]
```

**示例 3：**

```
输入：head = [1,2], n = 1
输出：[1]
```

**代码**

```java
    public ListNode removeNthFromEnd(ListNode head, int n) {
        int count = 1;
        ListNode p = head;
        while(p.next != null){
            count++;
            p = p.next;
        }
        if(count - n == 0)
            return head.next;

        //倒数n 正 count - n
        ListNode q = head;
        for(int i = 0;i < count - n - 1;i++)
            q = q.next;
        q.next = q.next.next;
        return head;
    }
```



## 2、翻转链表

给你单链表的头节点 `head` ，请你反转链表，并返回反转后的链表。

**代码**

```java
    public ListNode reverseList(ListNode head) {
        //新链表
        ListNode newHead = null;
        while (head != null) {
            ListNode temp = head.next;
            head.next = newHead;
            newHead = head;
            head = temp;
        }
        //返回新链表
        return newHead;
    }
```



## 3、合并两个有序链表

将两个升序链表合并为一个新的 升序 链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。 

**示例 1：**

```
输入：l1 = [1,2,4], l2 = [1,3,4]
输出：[1,1,2,3,4,4]
```

**示例 2：**

```
输入：l1 = [], l2 = []
输出：[]
```

**示例 3：**

```
输入：l1 = [], l2 = [0]
输出：[0]
```

**提示：**

>两个链表的节点数目范围是 [0, 50]
>-100 <= Node.val <= 100
>l1 和 l2 均按 非递减顺序 排列



```java
    public ListNode mergeTwoLists(ListNode list1, ListNode list2) {
        int []nums = new int[100];
        int tag = 0,lens = 0;
        //先保存两个链表的值到一个数组中
        while(list1 != null){
            nums[tag++] = list1.val;
            list1 = list1.next;
            lens++;
        }
        while(list2 != null){
            nums[tag++] = list2.val;
            list2 = list2.next;
            lens++;
        }
        //排序
        Arrays.sort(nums,0,lens);
        //输出到链表
        ListNode head = new ListNode();
        ListNode p = head;
        for(int i = 0; i < lens; i++){
            ListNode temp = new ListNode();
            temp.val = nums[i];
            p.next = temp;
            p = p.next;
        }
        p.next = null;
        return head.next;
    }
```



## 4、回文链表

给你一个单链表的头节点 head ，请你判断该链表是否为回文链表。如果是，返回 true ；否则，返回 false 。

**示例 1：**

```
输入：head = [1,2,2,1]
输出：true
```

**示例 2：**

```
输入：head = [1,2]
输出：false
```

**提示：**

>链表中节点数目在范围[1, 105] 内
>0 <= Node.val <= 9

**代码**

```java
    public boolean isPalindrome(ListNode head) {
        ListNode temp = head;
        int len = 0;
        while(temp != null){
            temp = temp.next;
            len++;
        }

        temp = head;
        int []nums = new int[len];
        for(int i = 0; i < len; i++){
            nums[i] = temp.val;
            temp = temp.next;
        }
        //判断回文
        for(int i = 0; i < len/2; i++){
            if(nums[i] != nums[len - i - 1])
                return false;
        }
        return true;
    }
```





# 树

## 1、二叉树的最大深度

给定一个二叉树，找出其最大深度。二叉树的深度为根节点到最远叶子节点的最长路径上的节点数。

**说明: 叶子节点是指没有子节点的节点。**

**示例：**

    给定二叉树 [3,9,20,null,null,15,7]，
    	3
       / \
      9  20
        /  \
       15   7
返回它的最大深度 3 。

**代码**

```java
public int maxDepth(TreeNode root) {
    if(root == null)
        return 0;
    return Math.max(maxDepth(root.left),maxDepth(root.right)) + 1;
}
```



## 2、











# 排序和搜索

## 1、合并有序数组

给你两个按 非递减顺序 排列的整数数组 nums1 和 nums2，另有两个整数 m 和 n ，分别表示 nums1 和 nums2 中的元素数目。

请你 合并 nums2 到 nums1 中，使合并后的数组同样按 非递减顺序 排列。

注意：最终，合并后数组不应由函数返回，而是存储在数组 nums1 中。为了应对这种情况，nums1 的初始长度为 m + n，其中前 m 个元素表示应合并的元素，后 n 个元素为 0 ，应忽略。nums2 的长度为 n 。

**示例 1：**

```
输入：nums1 = [1,2,3,0,0,0], m = 3, nums2 = [2,5,6], n = 3
输出：[1,2,2,3,5,6]
解释：需要合并 [1,2,3] 和 [2,5,6] 。
合并结果是 [1,2,2,3,5,6] ，其中斜体加粗标注的为 nums1 中的元素。
```

**示例 2：**

```
输入：nums1 = [1], m = 1, nums2 = [], n = 0
输出：[1]
解释：需要合并 [1] 和 [] 。
合并结果是 [1] 。
```

**示例 3：**

```
输入：nums1 = [0], m = 0, nums2 = [1], n = 1
输出：[1]
解释：需要合并的数组是 [] 和 [1] 。
合并结果是 [1] 。
注意，因为 m = 0 ，所以 nums1 中没有元素。nums1 中仅存的 0 仅仅是为了确保合并结果可以顺利存放到 nums1 中。
```

**代码**

```java
public void merge(int[] nums1, int m, int[] nums2, int n) {
    for(int i = 0; i < n; i++)
        nums1[m+i] = nums2[i];
    Arrays.sort(nums1);
}
```



## 2、第一个错误的版本

你是产品经理，目前正在带领一个团队开发新的产品。不幸的是，你的产品的最新版本没有通过质量检测。由于每个版本都是基于之前的版本开发的，所以错误的版本之后的所有版本都是错的。

假设你有 n 个版本 [1, 2, ..., n]，你想找出导致之后所有版本出错的第一个错误的版本。

你可以通过调用 bool isBadVersion(version) 接口来判断版本号 version 是否在单元测试中出错。实现一个函数来查找第一个错误的版本。你应该尽量减少对调用 API 的次数。

**示例 1：**

```
输入：n = 5, bad = 4
输出：4
解释：
调用 isBadVersion(3) -> false 
调用 isBadVersion(5) -> true 
调用 isBadVersion(4) -> true
所以，4 是第一个错误的版本。
```

**示例 2：**

```
输入：n = 1, bad = 1
输出：1
```

**代码**

```java
public int firstBadVersion(int n) {
    int start = 1, end = n;
    while (start < end) {
        int mid = start + (end - start) / 2;
        if (!isBadVersion(mid))
            start = mid + 1;
        else
            end = mid;
    }
    return start;
}
```





# 动态规划

## 1、爬楼梯

假设你正在爬楼梯。需要 n 阶你才能到达楼顶。

每次你可以爬 1 或 2 个台阶。你有多少种不同的方法可以爬到楼顶呢？

**示例 1：**

```
输入：n = 2
输出：2
解释：有两种方法可以爬到楼顶。

1. 1 阶 + 1 阶
2. 2 阶
```

**示例 2：**

```
输入：n = 3
输出：3
解释：
有三种方法可以爬到楼顶。
1. 1 阶 + 1 阶 + 1 阶
2. 1 阶 + 2 阶
3. 2 阶 + 1 阶
```

**代码**

非递归算法, 需要记住每一层楼梯能够爬到的方法数。

$dp[i] = dp[i-1] + dp[i-2]$

```java
    public int climbStairs(int n) {
        if(n <= 1)
            return 1;
        int []dp = new int[n];
        dp[0] = 1;
        dp[1] = 2;

        int res = 0;
        for(int i = 2;i < n;i++){
            dp[i] = dp[i-1] + dp[i-2];
        }
        return dp[n-1];
    }
```



## 2、买卖股票的最佳时机

给定一个数组 prices ，它的第 i 个元素 prices[i] 表示一支给定股票第 i 天的价格。

你只能选择 某一天 买入这只股票，并选择在 未来的某一个不同的日子 卖出该股票。设计一个算法来计算你所能获取的最大利润。

返回你可以从这笔交易中获取的最大利润。如果你不能获取任何利润，返回 0 。

**示例 1：**

```
输入：[7,1,5,3,6,4]
输出：5
解释：在第 2 天（股票价格 = 1）的时候买入，在第 5 天（股票价格 = 6）的时候卖出，最大利润 = 6-1 = 5 。
     注意利润不能是 7-1 = 6, 因为卖出价格需要大于买入价格；同时，你不能在买入前卖出股票。
```

**示例 2：**

```
输入：prices = [7,6,4,3,1]
输出：0
解释：在这种情况下, 没有交易完成, 所以最大利润为 0。
```

**代码**

暴力法

```java
    public int maxProfit(int[] prices) {
        //暴力
        int [] ans = new int[prices.length];
        for(int i = 0; i < prices.length; i++){
            ans[i] = 0;
            for(int j = i; j < prices.length; j++){
                if(prices[j] - prices[i] > 0){
                    ans[i] = Math.max(ans[i], prices[j] - prices[i]);
                }
            }
        }
        Arrays.sort(ans);
        return ans[prices.length - 1];
    }
```

双指针

```java
    public int maxProfit(int[] prices) {
        int pre, maxProfit;
        pre = maxProfit = 0;
        pre = prices[0];
        for(int i = 0; i < prices.length; i++){
            pre = Math.min(pre, prices[i]);
            maxProfit = Math.max(maxProfit, prices[i] - pre);
        }
        return  maxProfit;
    }
```





# 
