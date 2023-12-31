> 2021.10.1   		 1 - 3
>
> 2021.10.2   		 4 - 6
>
> 2021.10.3   		 7 - 9
>
> 2021.10.4   		 10 - 12
>
> 2021.10.5			13 - 15
>
> 2021.10.6			 16 - 18
>
> 2021.10.7 			19 - 21
>
> 2021.10.8			 22 - 24
>
> 2021.10.9			 25 - 27
>
> 2021.10.10			 28 - 30
>
> 2021.10.11 			31 - 33
>
> 2021.10.12			 33 - 36
>
> 2021.10.13			 37 - 39
>
> 2021.10.14			 40 - 42
>
> 2021.10.15 			43 - 45
>
> 2021.10.16 			46 - 48
>
> 2021.10.17 			49 - 51
>
> 2021.10.18 			52 - 54
>
> 2021.10.19 			55 - 57
>
> 2021.10.20 			55 - 57
>
> 2021.10.21 			58 - 60
>
> 2021.10.22 			61 - 63
>
> 2021.10.22 			64 - 66
>
> 2021.10.23 			67 - 69



## 1、删除重复的电子邮箱

编写一个 SQL 查询，来删除 `Person` 表中所有重复的电子邮箱，重复的邮箱里只保留 **Id** *最小* 的那个。

```sql
+----+------------------+
| Id | Email            |
+----+------------------+
| 1  | john@example.com |
| 2  | bob@example.com  |
| 3  | john@example.com |
+----+------------------+
Id 是这个表的主键。
```

例如，在运行你的查询语句之后，上面的 `Person` 表应返回以下几行:

```sql
+----+------------------+
| Id | Email            |
+----+------------------+
| 1  | john@example.com |
| 2  | bob@example.com  |
+----+------------------+
```

**代码**

```sql
DELETE b
FROM 
    Person AS a,
    Person AS b
WHERE 
    a.Email = b.Email AND a.Id < b.Id;
```



## 2、上升的温度

表 `Weather`

```sql
+---------------+---------+
| Column Name   | Type    |
+---------------+---------+
| id            | int     |
| recordDate    | date    |
| temperature   | int     |
+---------------+---------+
id 是这个表的主键
该表包含特定日期的温度信息
```

编写一个 SQL 查询，来查找与之前（昨天的）日期相比温度更高的所有日期的 `id` 。

返回结果 **不要求顺序** 。

查询结果格式如下例：

```sql
Weather
+----+------------+-------------+
| id | recordDate | Temperature |
+----+------------+-------------+
| 1  | 2015-01-01 | 10          |
| 2  | 2015-01-02 | 25          |
| 3  | 2015-01-03 | 20          |
| 4  | 2015-01-04 | 30          |
+----+------------+-------------+

Result table:
+----+
| id |
+----+
| 2  |
| 4  |
+----+
2015-01-02 的温度比前一天高（10 -> 25）
2015-01-04 的温度比前一天高（20 -> 30）
```

**代码**

```sql
SELECT a.id
FROM 
    Weather a, 
    Weather b
WHERE
    a.Temperature > b.Temperature AND dateDiff(a.recordDate,b.recordDate) = 1;
```



## 3、大的国家

这里有张 `World` 表

```sql
+-----------------+------------+------------+--------------+---------------+
| name            | continent  | area       | population   | gdp           |
+-----------------+------------+------------+--------------+---------------+
| Afghanistan     | Asia       | 652230     | 25500100     | 20343000      |
| Albania         | Europe     | 28748      | 2831741      | 12960000      |
| Algeria         | Africa     | 2381741    | 37100000     | 188681000     |
| Andorra         | Europe     | 468        | 78115        | 3712000       |
| Angola          | Africa     | 1246700    | 20609294     | 100990000     |
+-----------------+------------+------------+--------------+---------------+
```

如果一个国家的面积超过 300 万平方公里，或者人口超过 2500 万，那么这个国家就是大国家。

编写一个 SQL 查询，输出表中所有大国家的名称、人口和面积。

例如，根据上表，我们应该输出:

```sql
+--------------+-------------+--------------+
| name         | population  | area         |
+--------------+-------------+--------------+
| Afghanistan  | 25500100    | 652230       |
| Algeria      | 37100000    | 2381741      |
+--------------+-------------+--------------+
```

**代码**

```sql
SELECT name,population,area
FROM World
WHERE population > 25000000 OR area > 3000000;
```



## 4、超过5名学生的课

有一个`courses` 表 ，有: **student (学生)** 和 **class (课程)**。

请列出所有超过或等于5名学生的课。

例如，表：

```sql
+---------+------------+
| student | class      |
+---------+------------+
| A       | Math       |
| B       | English    |
| C       | Math       |
| D       | Biology    |
| E       | Math       |
| F       | Computer   |
| G       | Math       |
| H       | Math       |
| I       | Math       |
+---------+------------+
```

应该输出:

```sql
+---------+
| class   |
+---------+
| Math    |
+---------+
```

**代码**

```sql
SELECT class
FROM courses
GROUP BY class
HAVING COUNT(DISTINCT student) >= 5;
```



## 5、有趣的电影

某城市开了一家新的电影院，吸引了很多人过来看电影。该电影院特别注意用户体验，专门有个 LED显示板做电影推荐，上面公布着影评和相关电影描述。

作为该电影院的信息部主管，您需要编写一个 SQL查询，找出所有影片描述为非 boring (不无聊) 的并且 id 为奇数 的影片，结果请按等级 rating 排列。

例如，下表 `cinema`:

```sql
+---------+-----------+--------------+-----------+
|   id    | movie     |  description |  rating   |
+---------+-----------+--------------+-----------+
|   1     | War       |   great 3D   |   8.9     |
|   2     | Science   |   fiction    |   8.5     |
|   3     | irish     |   boring     |   6.2     |
|   4     | Ice song  |   Fantacy    |   8.6     |
|   5     | House card|   Interesting|   9.1     |
+---------+-----------+--------------+-----------+
```

对于上面的例子，则正确的输出是为：

```sql
+---------+-----------+--------------+-----------+
|   id    | movie     |  description |  rating   |
+---------+-----------+--------------+-----------+
|   5     | House card|   Interesting|   9.1     |
|   1     | War       |   great 3D   |   8.9     |
+---------+-----------+--------------+-----------+
```

**代码**

```sql
SELECT *
FROM cinema
WHERE description != 'boring' AND id % 2 != 0 
ORDER BY rating DESC;
```



## 6、变更性别

`Salary` 表：

```sql
+-------------+----------+
| Column Name | Type     |
+-------------+----------+
| id          | int      |
| name        | varchar  |
| sex         | ENUM     |
| salary      | int      |
+-------------+----------+
id 是这个表的主键。
sex 这一列的值是 ENUM 类型，只能从 ('m', 'f') 中取。
本表包含公司雇员的信息。
```

请你编写一个 SQL 查询来交换所有的 'f' 和 'm' （即，将所有 'f' 变为 'm' ，反之亦然），仅使用 单个 update 语句 ，且不产生中间临时表。

注意，你必须仅使用一条 update 语句，且 不能 使用 select 语句。

查询结果如下例所示：

```sql
Salary 表：
+----+------+-----+--------+
| id | name | sex | salary |
+----+------+-----+--------+
| 1  | A    | m   | 2500   |
| 2  | B    | f   | 1500   |
| 3  | C    | m   | 5500   |
| 4  | D    | f   | 500    |
+----+------+-----+--------+

Result 表：
+----+------+-----+--------+
| id | name | sex | salary |
+----+------+-----+--------+
| 1  | A    | f   | 2500   |
| 2  | B    | m   | 1500   |
| 3  | C    | f   | 5500   |
| 4  | D    | m   | 500    |
+----+------+-----+--------+
(1, A) 和 (3, C) 从 'm' 变为 'f' 。
(2, B) 和 (4, D) 从 'f' 变为 'm' 。
```

**代码**

```sql
UPDATE Salary 
SET sex = IF(sex = "f","m","f")
```



## 7、重新格式化部门表

部门表 `Department`：

```sql
+---------------+---------+
| Column Name   | Type    |
+---------------+---------+
| id            | int     |
| revenue       | int     |
| month         | varchar |
+---------------+---------+
(id, month) 是表的联合主键。
这个表格有关于每个部门每月收入的信息。
月份（month）可以取下列值 ["Jan","Feb","Mar","Apr","May","Jun","Jul","Aug","Sep","Oct","Nov","Dec"]。
```

编写一个 SQL 查询来重新格式化表，使得新的表中有一个部门 id 列和一些对应 **每个月** 的收入（revenue）列。

查询结果格式如下面的示例所示：

```sql
Department 表：
+------+---------+-------+
| id   | revenue | month |
+------+---------+-------+
| 1    | 8000    | Jan   |
| 2    | 9000    | Jan   |
| 3    | 10000   | Feb   |
| 1    | 7000    | Feb   |
| 1    | 6000    | Mar   |
+------+---------+-------+

查询得到的结果表：
+------+-------------+-------------+-------------+-----+-------------+
| id   | Jan_Revenue | Feb_Revenue | Mar_Revenue | ... | Dec_Revenue |
+------+-------------+-------------+-------------+-----+-------------+
| 1    | 8000        | 7000        | 6000        | ... | null        |
| 2    | 9000        | null        | null        | ... | null        |
| 3    | null        | 10000       | null        | ... | null        |
+------+-------------+-------------+-------------+-----+-------------+

注意，结果表有 13 列 (1个部门 id 列 + 12个月份的收入列)。
```

**代码**

```sql
# Write your MySQL query statement below
SELECT DISTINCT id,
    sum(IF(month="Jan",revenue,null)) as Jan_Revenue,
    sum(IF(month="Feb",revenue,null)) as Feb_Revenue,
    sum(IF(month="Mar",revenue,null)) as Mar_Revenue,
    sum(IF(month="Apr",revenue,null)) as Apr_Revenue,
    sum(IF(month="May",revenue,null)) as May_Revenue,
    sum(IF(month="Jun",revenue,null)) as Jun_Revenue,
    sum(IF(month="Jul",revenue,null)) as Jul_Revenue,
    sum(IF(month="Aug",revenue,null)) as Aug_Revenue,
    sum(IF(month="Sep",revenue,null)) as Sep_Revenue,
    sum(IF(month="Oct",revenue,null)) as Oct_Revenue,
    sum(IF(month="Nov",revenue,null)) as Nov_Revenue,
    sum(IF(month="Dec",revenue,null)) as Dec_Revenue
    FROM Department GROUP BY id ORDER BY id;
```



## 8、快乐数

编写一个算法来判断一个数 n 是不是快乐数。

「快乐数」定义为：

对于一个正整数，每一次将该数替换为它每个位置上的数字的平方和。
然后重复这个过程直到这个数变为 1，也可能是 无限循环 但始终变不到 1。
如果 可以变为  1，那么这个数就是快乐数。
如果 n 是快乐数就返回 true ；不是，则返回 false 。

**示例**

```
示例 1：
    输入：19
    输出：true
    解释：
    12 + 92 = 82
    82 + 22 = 68
    62 + 82 = 100
    12 + 02 + 02 = 1
示例 2：
    输入：n = 2
    输出：false
```

**代码**

```C
//求每位数的平方和
int getsum(int n)
{
    int sum=0;
    while(n)
    {
        sum += (n%10)*(n%10);
        n/=10;
    }
    return sum;
}

//这里比较模糊的概念是终止条件
//现在可以得到当判断快乐数的循环重复进行时, 也即 12 - 5 - 25 - 27 - 53 - 34 - 25
//在这里发生了重复, 所以它不是一个快乐数 , 也即快慢指针相撞了。
bool isHappy(int n){
    int slow=n,quick=n;
    do
    {
        //快指针每次走两步
        quick = getsum(quick);
        quick = getsum(quick); 
        //慢指针每次走一步         
        slow = getsum(slow); 
        //成功条件           
        if(slow==1 || quick==1)
            return true;
    }while(quick != slow);      //失败条件
    return false;
}
```



## 9、重复 N 次的元素(LC 961)

在大小为 `2N` 的数组 `A` 中有 `N+1` 个不同的元素，其中有一个元素重复了 `N` 次。

返回重复了 `N` 次的那个元素。

**示例**

```
示例 1：

输入：[1,2,3,3]
输出：3
示例 2：

输入：[2,1,2,5,3,2]
输出：2
示例 3：

输入：[5,1,5,2,5,3,5,4]
输出：5
```

**代码**

```c
int repeatedNTimes(int* nums, int numsSize){
    //暴力法遍历
    int i,j;
    for(i = 0;i < numsSize;i++){
        int times = 0;
        for(j = 0;j < numsSize;j++){
            if(nums[i] == nums[j])
                times++;
        }
        if(times == numsSize/2)
            break;
    }
    return nums[i];
}
```



## 10、链表中的下一个更大结点(LC 1019)

给出一个以头节点 head 作为第一个节点的链表。链表中的节点分别编号为：node_1, node_2, node_3, ... 。

每个节点都可能有下一个更大值（next larger value）：对于 node_i，如果其 next_larger(node_i) 是 node_j.val，那么就有 j > i 且  node_j.val > node_i.val，而 j 是可能的选项中最小的那个。如果不存在这样的 j，那么下一个更大值为 0 。

返回整数答案数组 answer，其中 answer[i] = next_larger(node_{i+1}) 。

注意：在下面的示例中，诸如 [2,1,5] 这样的输入（不是输出）是链表的序列化表示，其头节点的值为 2，第二个节点值为 1，第三个节点值为 5 。

**示例**

```
示例 1：

输入：[2,1,5]
输出：[5,5,0]
示例 2：

输入：[2,7,4,3,5]
输出：[7,0,5,5,0]
示例 3：

输入：[1,7,5,1,9,2,5,1]
输出：[7,9,9,9,0,5,0,0]
```

**代码**

```C
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     struct ListNode *next;
 * };
 */


/**
 * Note: The returned array must be malloced, assume caller calls free().
 */
int* nextLargerNodes(struct ListNode* head, int* returnSize){
    // 根据题解的意思是,返回结点i后第一个比其值大的结点,如果没有就返回0
    struct ListNode * p,*q,*k;
    p = head;
    //获取链表长度
    int len = 0;
    while(p){
        len++;
        p = p->next;
    }
    int * result = (int*)malloc(sizeof(int)*len);       //动态生成数组空间
    p = head;
    q = head->next;
    
    // p指向当前结点,q指向q的下一个结点
    //循环当p的值小于第一个q向后遍历获取的结点值时 break 并将该值赋值给result数组
    int i = 0;
    while(p){
        //分配空间 - 结果结点
        struct ListNode * h = (struct ListNode *)malloc(sizeof(struct ListNode));
        h->val = 0;         //初始为0, 如果没有大的值就为0
        while(q){
            //找到结果结点
            if(p->val < q->val){
                h->val = q->val;
                break;
            }
            q = q->next;
        }
        //向结果集合赋值
        result[i++] = h->val;
        p = p->next;                //后移节点
        if(p)
            q = p->next;            //后移节点
    }
    *returnSize = len;      //返回的数组大小
    return result;
}
```



## 11、特殊数组的特征值

给你一个非负整数数组 nums 。如果存在一个数 x ，使得 nums 中恰好有 x 个元素 大于或者等于 x ，那么就称 nums 是一个 特殊数组 ，而 x 是该数组的 特征值 。

注意： x 不必 是 nums 的中的元素。

如果数组 nums 是一个 特殊数组 ，请返回它的特征值 x 。否则，返回 -1 。可以证明的是，如果 nums 是特殊数组，那么其特征值 x 是 唯一的 。

**示例**

```
示例 1：

输入：nums = [3,5]
输出：2
解释：有 2 个元素（3 和 5）大于或等于 2 。
示例 2：

输入：nums = [0,0]
输出：-1
解释：没有满足题目要求的特殊数组，故而也不存在特征值 x 。
如果 x = 0，应该有 0 个元素 >= x，但实际有 2 个。
如果 x = 1，应该有 1 个元素 >= x，但实际有 0 个。
如果 x = 2，应该有 2 个元素 >= x，但实际有 0 个。
x 不能取更大的值，因为 nums 中只有两个元素。
示例 3：

输入：nums = [0,4,3,0,4]
输出：3
解释：有 3 个元素大于或等于 3 。
示例 4：

输入：nums = [3,6,7,7,0]
输出：-1
```

**代码**

```c
int specialArray(int* nums, int numsSize){
    //算法的终止条件是数组长度
    //从1开始 0 是不可能的, 因为不可能恰有0个数据大于等于0
    int i,j,tag=0;
    for(i = 1;i <= numsSize;i++){
        int times = 0;
        for(j = 0;j < numsSize;j++){
            if(i <= nums[j])
                times++;
        }
        if(times == i){
            tag = 1;
            break;
        }
   }
   return tag == 0 ? -1 : i;
}
```



## 12、链表中倒数第k个结点

输入一个链表，输出该链表中倒数第k个节点。为了符合大多数人的习惯，本题从1开始计数，即链表的尾节点是倒数第1个节点。

例如，一个链表有 6 个节点，从头节点开始，它们的值依次是 1、2、3、4、5、6。这个链表的倒数第 3 个节点是值为 4 的节点。

**示例**

```
示例：
给定一个链表: 1->2->3->4->5, 和 k = 2.
返回链表 4->5.
```

**代码**

```c
struct ListNode * getKthFromEnd(struct ListNode* head, int k){
    //取链表大小
    struct ListNode* p,q;
    p = head;
    int len = 0;
    while(p){
        len++;
        p = p->next;
    }
    p = head;

    // 取倒数第k个就相当于取正数 len - k + 1 结点(后移次数len - k)
    int tag = len - k;
    while(tag--){
        p = p->next;
    }
    return p;
}
```



## 13、种花问题(LC 605)

假设有一个很长的花坛，一部分地块种植了花，另一部分却没有。可是，花不能种植在相邻的地块上，它们会争夺水源，两者都会死去。

给你一个整数数组  flowerbed 表示花坛，由若干 0 和 1 组成，其中 0 表示没种植花，1 表示种植了花。另有一个数 n ，能否在不打破种植规则的情况下种入 n 朵花？能则返回 true ，不能则返回 false。

**示例**

```
示例 1：

输入：flowerbed = [1,0,0,0,1], n = 1
输出：true
示例 2：

输入：flowerbed = [1,0,0,0,1], n = 2
输出：false
```

**代码**

主要在于边界条件的确定,不能够下标越界

```c
bool canPlaceFlowers(int* flowerbed, int flowerbedSize, int n){
    //该题实际上是找 能种下花的位置个数
    //有以下的情况
    // 空 0 0    0 0 0    0 0 空 中间的 0 种植
    //也即找 左右都没有种植花(1) 的 0 个数
    int i;
    int position = 0;
    //边界
    if(flowerbedSize == 1 && flowerbed[0] == 0){
        position=1;
        flowerbedSize=0;        //不再执行循环
    }
        
    for(i = 0;i < flowerbedSize;i++){
        tag = 0;
        //左边界判断
        if(flowerbed[i] == 0 && i == 0 && flowerbed[i+1] == 0){
            position++;
            flowerbed[i]=1;     //种植上,方便后续计算
        }
        //右边界判断 - 防止越界
        else if(flowerbed[i] == 0 && i == flowerbedSize-1 && flowerbed[i-1] == 0){
            position++;
            flowerbed[i]=1;     //种植上,方便后续计算
        }
        //刨除左右边界计算的情况
        if(i != 0 && i != flowerbedSize-1){
            if(flowerbed[i] == 0 && flowerbed[i-1] == 0 && flowerbed[i+1] == 0){
                position++;
                flowerbed[i]=1;     //种植上,方便后续计算
            }
        }

    }
    return position >= n ? true : false;
}
```



## 14、第二高的薪资

编写一个 SQL 查询，获取 `Employee` 表中第二高的薪水（Salary） 。

```sql
+----+--------+
| Id | Salary |
+----+--------+
| 1  | 100    |
| 2  | 200    |
| 3  | 300    |
+----+--------+
```

例如上述 `Employee` 表，SQL查询应该返回 `200` 作为第二高的薪水。如果不存在第二高的薪水，那么查询应返回 `null`。

```sql
+---------------------+
| SecondHighestSalary |
+---------------------+
| 200                 |
+---------------------+
```

**代码**

外层 SELECT 是为了输出null, 内层 SELECT 使用 LIMIT 输出了降序排序后位于第二位的数据。  LIMIT 偏移为第 1 行(0开始), 数据个数 1 个(offset , count)。

```sql
SELECT
    (SELECT DISTINCT
            Salary
        FROM
            Employee
        ORDER BY Salary DESC
        LIMIT 1 OFFSET 1) AS SecondHighestSalary;
```

**LIMIT 概述**

在`SELECT`语句中使用`LIMIT`子句来约束结果集中的行数。`LIMIT`子句接受一个或两个参数。两个参数的值必须为零或正整数

下面说明了两个参数的`LIMIT`子句语法：

```sql
SELECT 
    column1,column2,...
FROM
    table
LIMIT offset , count;
SQL
```

我们来查看`LIMIT`子句参数：

- `offset`参数指定要返回的第一行的偏移量。第一行的偏移量为`0`，而不是`1`。
- `count`指定要返回的最大行数。



## 15、两个数组之间的距离(LC 1385)

给你两个整数数组 arr1 ， arr2 和一个整数 d ，请你返回两个数组之间的 距离值 。

「距离值」 定义为符合此距离要求的元素数目：对于元素 arr1[i] ，不存在任何元素 arr2[j] 满足 |arr1[i]-arr2[j]| <= d 。

**示例**

```
示例 1：

输入：arr1 = [4,5,8], arr2 = [10,9,1,8], d = 2
输出：2
解释：
对于 arr1[0]=4 我们有：
|4-10|=6 > d=2 
|4-9|=5 > d=2 
|4-1|=3 > d=2 
|4-8|=4 > d=2 
所以 arr1[0]=4 符合距离要求

对于 arr1[1]=5 我们有：
|5-10|=5 > d=2 
|5-9|=4 > d=2 
|5-1|=4 > d=2 
|5-8|=3 > d=2
所以 arr1[1]=5 也符合距离要求

对于 arr1[2]=8 我们有：
|8-10|=2 <= d=2
|8-9|=1 <= d=2
|8-1|=7 > d=2
|8-8|=0 <= d=2
	存在距离小于等于 2 的情况，不符合距离要求 
	故而只有 arr1[0]=4 和 arr1[1]=5 两个符合距离要求，距离值为 2
示例 2：
	输入：arr1 = [1,4,2,3], arr2 = [-4,-3,6,10,20,30], d = 3
	输出：2
示例 3：
	输入：arr1 = [2,1,100,3], arr2 = [-5,-2,10,-3,7], d = 6
	输出：1

```

**代码**

```c
int findTheDistanceValue(int* arr1, int arr1Size, int* arr2, int arr2Size, int d){
    //暴力 双层循环
    int i,j;
    int distance = 0;
    for(i = 0;i < arr1Size;i++){
        for(j = 0;j < arr2Size;j++){
            if(abs(arr1[i] - arr2[j]) <= d)
                break;
        }
        if(j == arr2Size)
            distance++;
    }
    return distance;
}
```



## 16、移除链表元素(LC 203)

给你一个链表的头节点 `head` 和一个整数 `val` ，请你删除链表中所有满足 `Node.val == val` 的节点，并返回 **新的头节点** 。

**示例**

```
示例 1：
	输入：head = [1,2,6,3,4,5,6], val = 6
	输出：[1,2,3,4,5]
示例 2：
	输入：head = [], val = 1
	输出：[]
示例 3：
	输入：head = [7,7,7,7], val = 7
	输出：[]
```

**代码**

```c
struct ListNode* removeElements(struct ListNode* head, int val){
    struct ListNode * p,*q;
    p = (struct ListNode *)malloc(sizeof(struct ListNode));
    p->next = head;
    q = p;

    while(q->next){
        if(q->next->val == val){
            q->next = q->next->next;
        } else{
            q = q->next;
        }
    }
    return p->next;
}   
```



## 17、同构字符串(LC205)

给定两个字符串 s 和 t，判断它们是否是同构的。

如果 s 中的字符可以按某种映射关系替换得到 t ，那么这两个字符串是同构的。

每个出现的字符都应当映射到另一个字符，同时不改变字符的顺序。不同字符不能映射到同一个字符上，相同字符只能映射到同一个字符上，字符可以映射到自己本身。

**示例**

```c
示例 1:
	输入：s = "egg", t = "add"
	输出：true
示例 2：
	输入：s = "foo", t = "bar"
	输出：false
示例 3：
	输入：s = "paper", t = "title"
	输出：true
```

**代码**

```c
struct HashTable {
    char key;
    char val;
    UT_hash_handle hh;
};

bool isIsomorphic(char* s, char* t) {
    struct HashTable* s2t = NULL;
    struct HashTable* t2s = NULL;
    int len = strlen(s);
    for (int i = 0; i < len; ++i) {
        char x = s[i], y = t[i];
        struct HashTable *tmp1, *tmp2;
        HASH_FIND(hh, s2t, &x, sizeof(char), tmp1);
        HASH_FIND(hh, t2s, &y, sizeof(char), tmp2);
        if (tmp1 != NULL) {
            if (tmp1->val != y) {
                return false;
            }
        } else {
            tmp1 = malloc(sizeof(struct HashTable));
            tmp1->key = x;
            tmp1->val = y;
            HASH_ADD(hh, s2t, key, sizeof(char), tmp1);
        }
        if (tmp2 != NULL) {
            if (tmp2->val != x) {
                return false;
            }
        } else {
            tmp2 = malloc(sizeof(struct HashTable));
            tmp2->key = y;
            tmp2->val = x;
            HASH_ADD(hh, t2s, key, sizeof(char), tmp2);
        }
    }
    return true;
}
```

算法正确, 超出时间限制

```c
bool isIsomorphic(char * s, char * t){
    int length = strlen(s);     //获取长度
    //使用间接数组存放对比结果 ASCII 码
    int ** form = malloc(sizeof(int *)*2);
    form[0] = malloc(sizeof(int)*length);
    form[1] = malloc(sizeof(int)*length);

    //存放映射关系
    int i = 0;
    while(i < length){
        form[0][i] = (int)*(s+i);
        form[1][i] = (int)*(t+i);
        i++;
    }

    int size = i;
    int j;
    //存放了i个映射关系,比较是否存在不对应的映射,也即1 对 5 和 1 对 7 同时存在
    for(i = 0;i < size;i++){
        for(j = 0;j < size;j++){
            if(form[0][i] == form[0][j] && form[1][i] != form[1][j])
                return false;
            if(form[0][i] != form[0][j] && form[1][i] == form[1][j])
                return false;
            //删除已经比较过的数据,降低复杂度
        }
    }
    return true;
}
```



## 18、反转链表

给你单链表的头节点 `head` ，请你反转链表，并返回反转后的链表。

**示例**

```
示例 1：
	输入：head = [1,2,3,4,5]
	输出：[5,4,3,2,1]
示例 2：
	输入：head = [1,2]
	输出：[2,1]
示例 3：
	输入：head = []
	输出：[]
```

**代码**

```c
struct ListNode* reverseList(struct ListNode* head){
    //使用辅助数组
    struct ListNode* p;
    p = head;
    int len = 0;
    while(p){
        len++;
        p = p->next;
    }

    int i = 0;
    //赋值到数组
    p = head;
    int * nums = malloc(sizeof(int)*len);
    while(p){
        nums[i] = p->val;
        p = p->next;
        i++; 
    }

    //翻转赋值到链表
    i = 0;
    p = head;
    while(p){
        p->val = nums[len-i-1];
        i++;
        p = p->next;
    }
    return head;
}
```



## 19、存在重复元素

给定一个整数数组，判断是否存在重复元素。

如果存在一值在数组中出现至少两次，函数返回 `true` 。如果数组中每个元素都不相同，则返回 `false` 。

**示例**

```
示例 1:
	输入: [1,2,3,1]
	输出: true
示例 2:
	输入: [1,2,3,4]
	输出: false
示例 3:
	输入: [1,1,1,3,3,4,3,2,4,2]
	输出: true
```

**代码**

```c
int cmp(const void* _a, const void* _b) {
    int a = *(int*)_a, b = *(int*)_b;
    return a - b;
}

bool containsDuplicate(int* nums, int numsSize) {
    qsort(nums, numsSize, sizeof(int), cmp);
    for (int i = 0; i < numsSize - 1; i++) {
        if (nums[i] == nums[i + 1]) {
            return true;
        }
    }
    return false;
}
```

算法正确, 复杂度 O(n^2) 不符合, 考虑使用排序来做

```c
bool containsDuplicate(int* nums, int numsSize){
    //暴力法
    int i,j;
    for(i = 0;i < numsSize;i++){
        for(j = 0;j < numsSize;j++){
            if(i == j)
                continue;
            if(nums[i] == nums[j])
                return true;
        }
    }
    return false;
}
```



## 20、汇总区间

给定一个无重复元素的有序整数数组 nums 。

返回 恰好覆盖数组中所有数字 的 最小有序 区间范围列表。也就是说，nums 的每个元素都恰好被某个区间范围所覆盖，并且不存在属于某个范围但不属于 nums 的数字 x 。

列表中的每个区间范围 [a,b] 应该按如下格式输出：

"a->b" ，如果 a != b
"a" ，如果 a == b

**示例**

```
示例 1：
    输入：nums = [0,1,2,4,5,7]
    输出：["0->2","4->5","7"]
    解释：区间范围是：
    [0,2] --> "0->2"
    [4,5] --> "4->5"
    [7,7] --> "7"
示例 2：
    输入：nums = [0,2,3,4,6,8,9]
    输出：["0","2->4","6","8->9"]
    解释：区间范围是：
    [0,0] --> "0"
    [2,4] --> "2->4"
    [6,6] --> "6"
    [8,9] --> "8->9"
示例 3：
    输入：nums = []
    输出：[]
示例 4：
    输入：nums = [-1]
    输出：["-1"]
示例 5：
    输入：nums = [0]
    输出：["0"]
```

**代码**

根据题意得出区间划分只有两种情况, 一种是存在连续的数字区间如: 1,2,3,4  = 1 → 4 , 一种是单独的数字 6 = 6,9 = 9,11=11。也即只需要对两种情况进行划分即可, 当存在连续数字, 取 *left* 开始 和 *end* 结束; 存在单独数字, 直接放到结果集中即可。

```c
char** summaryRanges(int* nums, int numsSize, int* returnSize) {
    char** ret = malloc(sizeof(char*) * numsSize);
    *returnSize = 0;
    int i = 0;
    while (i < numsSize) {
        int low = i;
        i++;
        while (i < numsSize && nums[i] == nums[i - 1] + 1) {
            i++;
        }
        int high = i - 1;
        char* temp = malloc(sizeof(char) * 25);
        sprintf(temp, "%d", nums[low]);
        if (low < high) {
            sprintf(temp + strlen(temp), "->");
            sprintf(temp + strlen(temp), "%d", nums[high]);
        }
        ret[(*returnSize)++] = temp;
    }
    return ret;
}
```



## 21、分数排名

编写一个 SQL 查询来实现分数排名。

如果两个分数相同，则两个分数排名（Rank）相同。请注意，平分后的下一个名次应该是下一个连续的整数值。换句话说，名次之间不应该有“间隔”。

**示例**

```
+----+-------+
| Id | Score |
+----+-------+
| 1  | 3.50  |
| 2  | 3.65  |
| 3  | 4.00  |
| 4  | 3.85  |
| 5  | 4.00  |
| 6  | 3.65  |
+----+-------+
例如，根据上述给定的 Scores 表，你的查询应该返回（按分数从高到低排列）：

+-------+------+
| Score | Rank |
+-------+------+
| 4.00  | 1    |
| 4.00  | 1    |
| 3.85  | 2    |
| 3.65  | 3    |
| 3.65  | 3    |
| 3.50  | 4    |
+-------+------+
```

**代码**

```sql
SELECT Score,
dense_rank() OVER(ORDER BY Score DESC) AS 'Rank'
FROM Scores;
```

**DENSE_RANK()**

`DENSE_RANK()`是一个[窗口函数](https://www.begtut.com/mysql/mysql-window-functions.html)，它为分区或结果集中的每一行分配排名，而排名值没有间隙。

行的等级从行前的不同等级值的数量增加1。

`DENSE_RANK()` 函数的语法如下：

```
DENSE_RANK() OVER (
    PARTITION BY <expression>[{,<expression>...}]
    ORDER BY <expression> [ASC|DESC], [{,<expression>...}]
) 
```

在这个语法中：

- 首先，`PARTITION BY`子句将`FROM`子句生成的结果集划分为分区。`DENSE_RANK()`函数应用于每个分区。
- 其次，`ORDER BY` 子句指定`DENSE_RANK()`函数操作的每个分区中的行顺序。

如果分区具有两个或更多具有相同排名值的行，则将为这些行中的每一行分配相同的排名。

**OVER**

over不能单独使用，要和分析函数：*rank*() , *dense_rank*() , *row_number*()等一起使用



## 22、丢失的数字(LC 268)

 给定一个包含 `[0, n]` 中 `n` 个数的数组 `nums` ，找出 `[0, n]` 这个范围内没有出现在数组中的那个数。 

**示例**

```
示例 1：

输入：nums = [3,0,1]
输出：2
解释：n = 3，因为有 3 个数字，所以所有的数字都在范围 [0,3] 内。2 是丢失的数字，因为它没有出现在 nums 中。
示例 2：

输入：nums = [0,1]
输出：2
解释：n = 2，因为有 2 个数字，所以所有的数字都在范围 [0,2] 内。2 是丢失的数字，因为它没有出现在 nums 中。
```

**代码**

```c
int missingNumber(int* nums, int numsSize){
    //范围在0 - numsSize
    //借用辅助空间
    int i = 0,result = 0;
    int * temp = malloc(sizeof(int) * (numsSize+1));
    //初始化 tag = 0
    for(i = 0;i <= numsSize;i++)
        temp[i] = 0;
    //记录信息 0 - numsSize
    for(i = 0;i < numsSize;i++){
        if(0 <= nums[i] && nums[i] <= numsSize){
            temp[nums[i]] = 1;    //修改标志为1,代表已经出现
        }
    }
    //遍历获取没有出现的那个数
    for(i = 0;i <= numsSize;i++){
        if(temp[i] == 0){
            result = i;
        }
    }
    return result;
}
```



## 23、Nim 游戏(LC 292)

你和你的朋友，两个人一起玩 Nim 游戏：

桌子上有一堆石头。

- 你们轮流进行自己的回合，你作为先手。
- 每一回合，轮到的人拿掉 1 - 3 块石头。
- 拿掉最后一块石头的人就是获胜者。

 假设你们每一步都是最优解。请编写一个函数，来判断你是否可以在给定石头数量为 `n` 的情况下赢得游戏。如果可以赢，返回 `true`；否则，返回 `false` 。 

**示例**

```
示例 1：
	输入：n = 4
	输出：false 
	解释：如果堆中有 4 块石头，那么你永远不会赢得比赛；
     因为无论你拿走 1 块、2 块 还是 3 块石头，最后一块石头总是会被你的朋友拿走。
示例 2：
	输入：n = 1
	输出：true
示例 3：
	输入：n = 2
	输出：true
```

**代码**

```
bool canWinNim(int n){
    return n % 4 == 0 ? false : true;
}
```



## 24、连续出现的数字(LC 180)

**示例**

```
表：Logs
+-------------+---------+
| Column Name | Type    |
+-------------+---------+
| id          | int     |
| num         | varchar |
+-------------+---------+
id 是这个表的主键。
编写一个 SQL 查询，查找所有至少连续出现三次的数字。
返回的结果表中的数据可以按 任意顺序 排列。

查询结果格式如下面的例子所示：
Logs 表：
+----+-----+
| Id | Num |
+----+-----+
| 1  | 1   |
| 2  | 1   |
| 3  | 1   |
| 4  | 2   |
| 5  | 1   |
| 6  | 2   |
| 7  | 2   |
+----+-----+

Result 表：
+-----------------+
| ConsecutiveNums |
+-----------------+
| 1               |
+-----------------+
1 是唯一连续出现至少三次的数字。
```

**代码**

```c
# Write your MySQL query statement below
SELECT DISTINCT
    log1.num as 'ConsecutiveNums'
FROM
    Logs log1,
    Logs log2,
    Logs log3
WHERE
    log1.id = log2.id -1 AND log2.id = log3.id - 1 AND
    log1.num = log2.num AND log2.num = log3.num;
```



## 25、两数相加(LC 2)

给你两个 非空 的链表，表示两个非负的整数。它们每位数字都是按照 逆序 的方式存储的，并且每个节点只能存储 一位 数字。

请你将两个数相加，并以相同形式返回一个表示和的链表。

你可以假设除了数字 0 之外，这两个数都不会以 0 开头。

**示例**

示例1: 

![image-20211026210738762](img/image-20211026210738762.png)

```
	输入：l1 = [2,4,3], l2 = [5,6,4]
	输出：[7,0,8]
	解释：342 + 465 = 807.
示例 2：
	输入：l1 = [0], l2 = [0]
	输出：[0]
示例 3：
	输入：l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
	输出：[8,9,9,9,0,0,0,1]
```

**代码**

```c
struct ListNode* addTwoNumbers(struct ListNode* l1, struct ListNode* l2){
    //使用进位的思想来计算
    //获取两个链表的长度, 用来动态生成数组
    struct ListNode * p,*q,*t;
    t = malloc(sizeof(struct ListNode));
    p = l1;
    q = l2;
    int lenA = 0;
    int lenB = 0;
    while(p){
        lenA++;
        p = p->next;
    }
    while(q){
        lenB++;
        q = q->next;
    }
    //扩宽比较短的链表长度, 与长的链表长度一致 - 可以采用
    int tag = 0;    //进位标志
    int plus = 0;   //各位相加和
    int i = 0;      //当前是第几位
    int * nums = malloc(sizeof(int)* (lenA > lenB ? lenA + 1 : lenB + 1));        //获取最大的长度加1 相加最大进一位
    while(l1 || l2){
        if(!l1){
            plus = 0 + l2->val; 
        } else if(!l2){
            plus = l1->val + 0; 
        } else if(l1 && l2){
            plus = l1->val + l2->val;
        }
        
        //不考虑进位先赋值
        nums[i] = (plus+tag) % 10;    //个位 % 10 仍然为原数

        //当前位是否有向上一级的进位
        if(plus+tag >= 10)
            tag = 1;
        else
            tag = 0;
        
        i++;
        if(l1)
            l1 = l1->next;
        if(l2)
            l2 = l2->next;
    }

    int j = 0;
    q = t;
    for(j = 0;j < i;j++){
        struct ListNode * h = malloc(sizeof(struct ListNode));
        h->val = nums[j];
        t->next = h;
        t = t->next;
    }
    //9 + 9 = 18 8 1 没有 1 位, 这里加上
    if(tag == 1){
        struct ListNode * h = malloc(sizeof(struct ListNode));
        h->val = 1;
        t->next = h;
        t = t->next;
    }
    t->next = NULL;
    return q->next;
}
```

转为整型计算再分割存入链表 - 精度比较小, 限制在 int / long 范围内

```c
struct ListNode* addTwoNumbers(struct ListNode* l1, struct ListNode* l2){
    struct ListNode * p,*q,*t;
    p = l1;
    q = l2;
    t = malloc(sizeof(struct ListNode));
    int reverseA = 0;
    int reverseB = 0;
    //转为int计算再转为链表
    int i = 0;
    while(l1){
        reverseA += l1->val * pow(10,i);
        l1 = l1->next;
        i++;
    }
    i = 0;
    while(l2){
        reverseB += l2->val * pow(10,i);
        l2 = l2->next;
        i++;
    }
    int final = reverseA + reverseB;
    p = t;
    //将结果存到链表
    //处理边界条件 两个链表都为0的情况
    if(final == 0){
        struct ListNode * h = malloc(sizeof(struct ListNode));
        h->val = 0;    //各位开始存,结果是反的
        t->next = h;
        t = t->next;
    } else{
        while(final){
            struct ListNode * h = malloc(sizeof(struct ListNode));
            h->val = final % 10;    //各位开始存,结果是反的
            t->next = h;
            t = t->next;
            final/=10;
        }
    }
    t->next = NULL;
    return p->next;
}
```



## 26、2的幂

给你一个整数 n，请你判断该整数是否是 2 的幂次方。如果是，返回 true ；否则，返回 false 。

如果存在一个整数 x 使得$n = 2^x$ ，则认为 n 是 2 的幂次方。

**示例**

```c
示例 1：
	输入：n = 1
	输出：true
	解释：20 = 1
示例 2：
	输入：n = 16
	输出：true
	解释：24 = 16
示例 3：
	输入：n = 3
	输出：false
示例 4：
	输入：n = 4
	输出：true
示例 5：
	输入：n = 5
	输出：false
```

**代码**

**进制转换思想** 利用2的幂转换为2进制一定只含有一个1来判断是否是2的幂次 1 = 1  10 = 2  100 = 4 1000 = 8 

```c
bool isPowerOfTwo(int n){
    int tag = 0;
    while(n){
        tag += n % 2;
        n /= 2;
    }
    return tag == 1 ? true : false;
}
```

**暴力法**    这里可以通过一些方法来缩减复杂度, 先获取 n 的 i * i = n 的情况, 抛去 n % 2 != 0的情况等

```c
bool isPowerOfTwo(int n){
    int i;
    for(i = 0;i < n;i++){
        if(pow(2,i) == n)
            return true;
    }
    return false;
}
```



## 27、3的幂(LC 326)

给定一个整数，写一个函数来判断它是否是 3 的幂次方。如果是，返回 true ；否则，返回 false 。

整数 n 是 3 的幂次方需满足：存在整数 x 使得 n == $3^x$

**示例**

```
示例 1：
	输入：n = 27
	输出：true
示例 2：
	输入：n = 0
	输出：false
示例 3：
	输入：n = 9
	输出：true
示例 4：
	输入：n = 45
	输出：false
```

**代码**

**进制转换思想** 利用3的幂转换为3进制一定只含有一个1来判断是否是3的幂次  1 = 1  10 = 3  100 = 9 1000 = 27 

```c
bool isPowerOfThree(int n){
    int tag = 0;
    while(n){
        tag += n % 3;
        n /= 3;
    }
    return tag == 1 ? true : false;
}
```



## 28、4的幂(LC 342)

给定一个整数，写一个函数来判断它是否是 4 的幂次方。如果是，返回 true ；否则，返回 false 。

整数 n 是 4 的幂次方需满足：存在整数 x 使得 n == $4^x$

 **示例**

```
示例 1：
	输入：n = 16
	输出：true
示例 2：
	输入：n = 5
	输出：false
示例 3：
	输入：n = 1
	输出：true
```

**代码**

**进制转换思想** 利用4的幂转换为4进制一定只含有一个1来判断是否是4的幂次  1 = 1  10 = 4  100 = 16 1000 = 64 

```c
bool isPowerOfFour(int n){
    int tag = 0;
    while(n){
        tag += n % 4;
        n /= 4;
    }
    return tag == 1 ? true : false;
}
```



## 29、各位相加(LC 258)

给定一个非负整数 num，反复将各个位上的数字相加，直到结果为一位数。

**示例**

```
输入: 38
输出: 2 
解释: 各位相加的过程为：3 + 8 = 11, 1 + 1 = 2。 由于 2 是一位数，所以返回 2。
```

**代码**

**循环分割相加直到结果<10**。 首先统计位数生成间接数组, 循环 存放分割结果循环相加直到结果 < 10。

```c
int addDigits(int num){
    //统计数字位数
    int len = 0;
    int temp = num;
    while(temp){
        len++;
        temp /= 10;
    }

    //生成间接数组
    int * nums = malloc(sizeof(int)*len);
    int result = 10;     //结果,循环终止条件
    while(result >= 10){
        //分割数组
        int i = 0;
        result = 0;
        while(num){
            nums[i] = num % 10;
            num /= 10; 
            result += nums[i];
            i++;
        }
        num = result;
    }
    return result;
}
```



## 30、汉明距离(LC 461)

两个整数之间的汉明距离数字对应二进制位不同的位置的数目。

给你两个整数 `x` 和 `y`，计算并返回它们之间的汉明距离。

**示例**

```
示例 1：
	输入：x = 1, y = 4
	输出：2
	解释：
	1   (0 0 0 1)
	4   (0 1 0 0)
  	     ↑   ↑
	上面的箭头指出了对应二进制位不同的位置。
示例 2：
	输入：x = 3, y = 1
	输出：1

```

**代码**

内置函数

```c
int hammingDistance(int x, int y) {
    return __builtin_popcount(x ^ y);
}
```

转换为二进制各位存放到数组, 挨个比较

```c
int hammingDistance(int x, int y){
    //计算长度
    int lenA = 0;
    int lenB = 0;
    int temp = x;
    while(temp){
        lenA++;
        temp /= 2;
    }
    temp = y;
    while(temp){
        lenB++;
        temp /= 2;
    }

    int * numsA = malloc(sizeof(int)*lenA);
    int * numsB = malloc(sizeof(int)*lenB);
    //二进制存储到数组中



}
```



## 31、删除链表中的节点(自删 LC 237)

请编写一个函数，使其可以删除某个链表中给定的（非末尾）节点。传入函数的唯一参数为 要被删除的节点 。

现有一个链表 -- head = [4,5,1,9]，它可以表示为:

![img](img/237_example.png)

```c
示例 1：
	输入：head = [4,5,1,9], node = 5
	输出：[4,1,9]
	解释：给定你链表中值为 5 的第二个节点，那么在调用了你的函数之后，该链表应变为 4 -> 1 -> 9.
示例 2：
	输入：head = [4,5,1,9], node = 1
	输出：[4,5,9]
	解释：给定你链表中值为 1 的第三个节点，那么在调用了你的函数之后，该链表应变为 4 -> 5 -> 9.
```

**代码**

模仿数组删除 覆盖移除尾结点

```c
void deleteNode(struct ListNode* node) {
    struct ListNode * p,* q;
    p = node;
    q = node->next;
    while(q){
        p->val = q->val;
        //赋值完毕,直接退出,不再移动结点
        if(q->next == NULL)
            break;
        p = p->next;
        q = q->next;
    }
    p->next = NULL;
}
```



## 32、比特数计数(LC 338)

给你一个整数 `n` ，对于 `0 <= i <= n` 中的每个 `i` ，计算其二进制表示中 **`1` 的个数** ，返回一个长度为 `n + 1` 的数组 `ans` 作为答案。

**示例**

```
示例 1：
	输入：n = 2
	输出：[0,1,1]
	解释：
	0 --> 0
	1 --> 1
	2 --> 10
示例 2：
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

**代码**

```c
/**
 * Note: The returned array must be malloced, assume caller calls free().
 */
int * countBits(int n, int* returnSize){
    //间接数组
    int * result = malloc(sizeof(int)*(n+1));     //存放结果
    //转换为2进制
    int i = 0;
    int tag = 0;    //计数 1 的个数
    int num = 0;    //存放转换后的结果数组
    for(i = 0;i <= n;i++){
        num = i;
        //转换为2进制
        while(num){
            int flag = num % 2;       //2进制各位
            num /= 2;
            if(flag == 1)
                tag++;
        }
        result[i] = tag;
        tag = 0;    //重置用于下次计数
    }
    *returnSize = n+1;
    return result;
}
```



## 33、两个数组的交集(LC 349)

给定两个数组，编写一个函数来计算它们的交集。

**示例**

 ```
示例 1：

输入：nums1 = [1,2,2,1], nums2 = [2,2]
输出：[2]
示例 2：

输入：nums1 = [4,9,5], nums2 = [9,4,9,8,4]
输出：[9,4]
 ```

**代码**

暴力遍历 + 去重

```c
int* intersection(int* nums1, int nums1Size, int* nums2, int nums2Size, int* returnSize){
    //暴力法
    int len = nums1Size > nums2Size ? nums2Size : nums1Size;    //返回较小的,最大结果
    int * nums = malloc(sizeof(int)*len);
    //暴力遍历
    int i,j,k,tag = 0;
    for(i = 0;i < nums1Size;i++){
        for(j = 0;j < nums2Size;j++){
            //去重
            for(k = 0;k < tag;k++)
                if(nums1[i] == nums[k])
                    break;
            if(nums1[i] == nums2[j] && k == tag)
                nums[tag++] = nums1[i];
        }
    }
    * returnSize = tag;
    return nums;
}
```



## 34、两个数组的交集(LC 350)

给定两个数组，编写一个函数来计算它们的交集。

**示例**

```c
示例 1：
	输入：nums1 = [1,2,2,1], nums2 = [2,2]
	输出：[2,2]
示例 2:
	输入：nums1 = [4,9,5], nums2 = [9,4,9,8,4]
	输出：[4,9]
```

**代码**

冒泡排序 + 双指针 先排序然后使用双指针遍历两个数组, 获取结果。

```c
int* intersect(int* nums1, int nums1Size, int* nums2, int nums2Size, int* returnSize){
    //使用排序的思想进行排序
    int i,j;
    for(i = 0;i < nums1Size-1;i++){
        for(j = 0;j < nums1Size - i - 1;j++){
            if(nums1[j] > nums1[j+1]){
                int temp = nums1[j];
                nums1[j] = nums1[j+1];
                nums1[j+1] = temp;
            }
        }
    }
    for(i = 0;i < nums2Size-1;i++){
        for(j = 0;j < nums2Size - i - 1;j++){
            if(nums2[j] > nums2[j+1]){
                int temp = nums2[j];
                nums2[j] = nums2[j+1];
                nums2[j+1] = temp;
            }
        }
    }
    //指针比较 由于是升序排列, 小的数组应该前移, 直到连个数组中某个数组比较完毕
    int a = 0,b = 0,size = 0;
    int len = nums1Size > nums2Size ? nums2Size : nums1Size;    //返回小的
    int * nums = malloc(sizeof(int)*len);
    while(a < nums1Size && b < nums2Size){
        if(nums1[a] == nums2[b]){
            nums[size++] = nums1[a];
            a++;
            b++;
        } else if(nums1[a] < nums2[b]){
            a++;
        } else{
            b++;
        }
        len--;
    }
    *returnSize = size;
    return nums;
}
```



## 35、有效的完全平方数

给定一个 正整数 num ，编写一个函数，如果 num 是一个完全平方数，则返回 true ，否则返回 false 。

进阶：不要 使用任何内置的库函数，如  sqrt 。

**示例**

```c
示例 1：
    输入：num = 16
    输出：true
示例 2：
    输入：num = 14
    输出：false
```

**代码**

使用内置的开方函数 sqrt()

```c
bool isPerfectSquare(int num){
    int a = sqrt(num);
    return pow(a,2) == num; 
}
```



## 36、猜数字大小

猜数字游戏的规则如下：

每轮游戏，我都会从 1 到 n 随机选择一个数字。 请你猜选出的是哪个数字。
如果你猜错了，我会告诉你，你猜测的数字比我选出的数字是大了还是小了。
你可以通过调用一个预先定义好的接口 int guess(int num) 来获取猜测结果，返回值一共有 3 种可能的情况（-1，1 或 0）：

-1：我选出的数字比你猜的数字小 pick < num
1：我选出的数字比你猜的数字大 pick > num
0：我选出的数字和你猜的数字一样。恭喜！你猜对了！pick == num
返回我选出的数字。

**示例**

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

**代码**

超时 在数字比较大的情况, 运算时间过长

```
int guessNumber(int n){
	//遍历挨个猜, 不使用step计数
    int i,result;
    for(i = 0;i <= n;i++){
        if(!guess(i)){
            result = i;
            break;
        }  
    }
    return result;
}
```

二分法查找

```c
int guessNumber(int n){
    //二分查找的办思想
    int left = 0,right = n,result;
    while(left <= right){
        int mid = left + (right - left) / 2;
        if(!guess(mid)){
            result = mid;
            break;
        }
        else if(guess(mid) < 0)
            right = mid - 1;
        else if(guess(mid) > 0)
            left = mid + 1;
    }
    return result;
}
```



## 37、赎金信(LC 383)

给定一个赎金信 (ransom) 字符串和一个杂志(magazine)字符串，判断第一个字符串 ransom 能不能由第二个字符串 magazines 里面的字符构成。如果可以构成，返回 true ；否则返回 false。

(题目说明：为了不暴露赎金信字迹，要从杂志上搜索各个需要的字母，组成单词来表达意思。杂志字符串中的每个字符只能在赎金信字符串中使用一次。)

**示例**

 ```
示例 1：
	输入：ransomNote = "a", magazine = "b"
	输出：false
示例 2：
	输入：ransomNote = "aa", magazine = "ab"
	输出：false
示例 3：
	输入：ransomNote = "aa", magazine = "aab"
	输出：true
 ```

**代码**

间接数组记录字符出现次数, magazine中有足够构成ransomNote的字符个数即可

```c
bool canConstruct(char * ransomNote, char * magazine){
    //magazine中有足够构成ransomNote的字符个数即可
    //只含有小写字母 26 个使用 ASCII 判断
    int * nums1 = malloc(sizeof(int) * 26);
    int * nums2 = malloc(sizeof(int) * 26);
    //初始化每个位置为0
    memset(nums1,0,26);
    memset(nums2,0,26);
    while(*ransomNote){
        nums1[(int)*ransomNote - 97]++;   //存放到对应位置
        ransomNote++;
    }
    while(*magazine){
        nums2[(int)*magazine - 97]++;   //存放到对应位置
        magazine++;
    }
    int i;
    for(i = 0;i < 26;i++){
        if(nums1[i] == 0)
            continue;
        if(nums1[i] > nums2[i])
            break;
    }
    return i == 26 ? true : false;
}
```



## 38、字符串中的第一个唯一字符

给定一个字符串，找到它的第一个不重复的字符，并返回它的索引。如果不存在，则返回 -1。

**示例**

```
s = "leetcode"
返回 0

s = "loveleetcode"
返回 2
```

**代码**

数组存放字符出现次数, 再从头遍历字符串找到第一个出现次数为1的下标位置。

```c
int firstUniqChar(char * s){
    //使用之前使用过的 间接数组记录出现次数,然后对比
    int nums[26] = {0};
    char * temp;
    temp = s;
    int index = -1;      //结果 记录下标
    //遍历记录出现次数
    while(*temp){
        nums[(int)*temp - 97]++;
        temp++;
    }
    //从s头部开始依次遍历得到第一个 nums[i] = 1 的字符下标
    temp = s;
    int tag = 0;
    while(*temp){
        if(nums[(int)*temp - 97] == 1){
            index = tag;
            break;
        }     
        temp++;
        tag++;
    }
    return index;
}
```

思路一样, 使用数组操作的方式进行遍历

```c
int firstUniqChar(char * s){
    int a[26] = {0};
    int len = strlen(s);
    int i;

    for (i = 0; i < len; i++)
        a[s[i] - 'a']++;

    for (i = 0; i < len; i++) {
        if (a[s[i] - 'a'] == 1)
            return i;
    }

    return -1;
}
```

暴力法 超出时间限制。 使用

```c
int firstUniqChar(char * s){
    //暴力法
    char * m,* n;
    m = n = s;
    int tag = 0;		 //记录比较到的下标位置
    int index = -1;      //保存获取的下标
    while(*n){
        m = s;
        int flag = 0;       //判断是否出现了重复 0 代表不重复
        while(*m){
            //跳过n指向的位置
            if(m == n){
                m++;
                continue;
            }
            //记录 n 对应的字符出现了机次
            if(*n == *m)
                flag++;
            m++;
        }
        //flag = 0 代表一次都没有出现
        if(flag == 0){
            index = tag;
            break;
        }
        n++;
        tag++;
    }
    return index;
}
```



## 39、找不同(LC 389)

给定两个字符串 s 和 t，它们只包含小写字母。

字符串 t 由字符串 s 随机重排，然后在随机位置添加一个字母。

请找出在 t 中被添加的字母。

 **示例**

```
示例 1：
    输入：s = "abcd", t = "abcde"
    输出："e"
    解释：'e' 是那个被添加的字母。
示例 2：
    输入：s = "", t = "y"
    输出："y"
示例 3：
    输入：s = "a", t = "aa"
    输出："a"
示例 4：
    输入：s = "ae", t = "aea"
    输出："a"
```

**代码**

间接数组计数 得出str1中出现次数小于str2中出现次数的字符即为所求

```c
char findTheDifference(char * s, char * t){
    int nums1[26] = {0};
    int nums2[26] = {0};
    int i,lenA = strlen(s);
    //计算出现次数到数组中
    for(i = 0;i < lenA;i++)
        nums1[s[i] - 'a']++;
    for(i = 0;i < lenA+1;i++)
        nums2[t[i] - 'a']++;
    //遍历数组 对比nums1中次数=0,但nums2次数=1的即为所求
    for(i = 0;i <26;i++){
        if(nums1[i] < nums2[i])
            break;
    }
    return (char)i+97;
}
```



## 40、翻转字符串中的元音字母

给你一个字符串 s ，仅反转字符串中的所有元音字母，并返回结果字符串。

元音字母包括 'a'、'e'、'i'、'o'、'u'，且可能以大小写两种形式出现。

字符串内可能包含所有 ASCII 码字符, 大小写

**示例**

 ```
 示例 1：
 	输入：s = "hello"
 	输出："holle"
 示例 2：
 	输入：s = "leetcode"
 	输出："leotcede"
 ```

**代码**

暴力遍历 - 这个代码长度很高, 可以使用数组来存放对应结构。

```c
char * reverseVowels(char * s){
    //使用间接数组存放结果
    int len = strlen(s);
    int * nums = malloc(sizeof(int)*len);
    int * reverse = malloc(sizeof(int)*len);
    int i = 0;
    //记录结果
    int tag = 0;
    for(i = 0;i < len;i++){
        switch(s[i]){
            case 'a':
                nums[i] = 1;
                break;
            case 'e':
                nums[i] = 2;
                break;
            case 'i':
                nums[i] = 3;
                break;
            case 'o':
                nums[i] = 4;
                break;
            case 'u':
                nums[i] = 5;
                break;
            case 'A':
                nums[i] = 6;
                break;
            case 'E':
                nums[i] = 7;
                break;
            case 'I':
                nums[i] = 8;
                break;
            case 'O':
                nums[i] = 9;
                break;
            case 'U':
                nums[i] = 10;
                break;
            default:
                nums[i] = 0;
                break;
        }
        if(nums[i] != 0)
            reverse[tag++] = nums[i];
    }
    //整个转置
    for(i = 0;i < tag/2;i++){
        int temp = reverse[i];
        reverse[i] = reverse[tag-i-1];
        reverse[tag-i-1] = temp;
    }
    //根据reverse数组内翻转后的情况进行赋值
    tag = 0;
    for(i = 0;i < len;i++){
        if(nums[i] != 0){
            switch(reverse[tag++]){
                case 1:
                    s[i] = 'a';
                    break;
                case 2:
                    s[i] = 'e';
                    break;
                case 3:
                    s[i] = 'i';
                    break;
                case 4:
                    s[i] = 'o';
                    break;
                case 5:
                    s[i] = 'u';
                    break;
                case 6:
                    s[i] = 'A';
                    break;
                case 7:
                    s[i] = 'E';
                    break;
                case 8:
                    s[i] = 'I';
                    break;
                case 9:
                    s[i] = 'O';
                    break;
                case 10:
                    s[i] = 'U';
                    break;
            }
        }
    }
    return s;
}
```

使用间接数组 - 修改后

```c
char * reverseVowels(char * s){
    //使用间接数组存放结果
    int len = strlen(s);
    int * nums = malloc(sizeof(int)*len);
    int * reverse = malloc(sizeof(int)*len);
    int str[10] = {'a','e','i','o','u','A','E','I','O','U'};
    int i = 0,j = 0;
    //记录结果
    int tag = 0;
    for(i = 0;i < len;i++){
        for(j = 0;j < 10;j++)
            if(s[i] == str[j]){
                nums[i] = j+1;
                break;
            } 
        if(j == 10)
            nums[i] = 0;
        if(nums[i] != 0)
            reverse[tag++] = nums[i];
    }

    //整个转置
    for(i = 0;i < tag/2;i++){
        int temp = reverse[i];
        reverse[i] = reverse[tag-i-1];
        reverse[tag-i-1] = temp;
    }


    //根据reverse数组内翻转后的情况进行赋值
    tag = 0;
    for(i = 0;i < len;i++){
        if(nums[i] != 0){
           for(j = 0;j < 10;j++){
                if(reverse[tag] == j+1){
                    s[i] = str[j];
                    tag++;
                    break;
                }   
           }
        }
    }
    return s;
}
```



## 41、数字转为十六进制数(LC 405)  查看移位 & | >> <<操作符学习

给定一个整数，编写一个算法将这个数转换为十六进制数。对于负整数，我们通常使用 **补码运算** 方法。

> 注意:
>
> 十六进制中所有字母(a-f)都必须是小写。
> 十六进制字符串中不能包含多余的前导零。如果要转化的数为0，那么以单个字符'0'来表示；对于其他情况，十六进制字符串中的第一个字符将不会是0字符。 
> 给定的数确保在32位有符号整数范围内。
> 不能使用任何由库提供的将数字直接转换或格式化为十六进制的方法。

**示例**

```
示例 1：
    输入:
    26
    输出:
    "1a"
示例 2：
    输入:
    -1
    输出:
    "ffffffff"
```

**代码**

```c
char * toHex(int num){
    //16进制对应的字符
    char str[16]={'0','1','2','3','4','5','6','7','8','9','a','b','c','d','e','f'};
    char * reverse; //结果数组
    //分配空间 - 足底啊32位整型,16进制则为9位
    reverse = (char *)malloc(sizeof(char) * 9);    
    int i = 0;
    //倒序存放
    for(i = 7 ;i >= 0;i--){
        reverse[i] = str[num & 0xF];      //每位16进制
        num = num>>4;
    }
    //在最后加上终止字符, 防止识别不到终止, 长度越界
    reverse[8]='\0';
    //不满8位时存在前缀0, 去除前缀0
    while(reverse[0]=='0' && *(reverse+1)!='\0')    reverse++;
    return reverse;
}
```



## 42、最长回文串(LC 409)

给定一个包含大写字母和小写字母的字符串，找到通过这些字母构造成的最长的回文串。

在构造过程中，请注意区分大小写。比如 "Aa" 不能当做一个回文字符串。

注意:
假设字符串的长度不会超过 1010。

**示例**

```
示例 1:
	输入:
	"abccccdd"
	输出:
	7
	解释:
	我们可以构造的最长的回文串是"dccaccd", 它的长度是 7。
```

**代码**

```c
int longestPalindrome(char * s){
    //间接数组存放出现次数
    int nums[52] = {0};  //区分大小写
    //统计出现次数
    char * temp = s;
    int tag = 0;
    while(*temp){
        if(*temp >= 'A' && *temp <= 'Z'){
            nums[*temp++ - 'A']++;      //0 - 26 27 - 52个
        } else if(*temp >= 'a' && *temp <= 'z'){
            nums[*temp++ - 'a' + 26]++;      //0 - 26 27 - 52个
        }
    }
        
    //拿到了次数,进行构造
    //奇数次放中间, 偶数次放两边
    int i = 0;
    int resLen = 0;
    int max = 0;
    int index = 0;
    for(i = 0;i < 52;i++){
        //奇数时, 出现次数为奇数中最大的
        if(nums[i] % 2 != 0){
            if(max < nums[i]){
                max = nums[i];
                index = i;
            }
            resLen += nums[i] -1;       //去掉1位就可以构造
        }
        if(nums[i] % 2 == 0){
            resLen += nums[i];
        }
    }
    if(max != 0)
        resLen -= nums[index] - 1;
    return resLen + max;
}
```



## 43、Fizz Buzz(LC 412)

给你一个整数 n ，找出从 1 到 n 各个整数的 Fizz Buzz 表示，并用字符串数组 answer（下标从 1 开始）返回结果，其中：

answer[i] == "FizzBuzz" 如果 i 同时是 3 和 5 的倍数。
answer[i] == "Fizz" 如果 i 是 3 的倍数。
answer[i] == "Buzz" 如果 i 是 5 的倍数。
answer[i] == i 如果上述条件全不满足。

**示例**

```
示例 1：
	输入：n = 3
	输出：["1","2","Fizz"]
示例 2：
	输入：n = 5
	输出：["1","2","Fizz","4","Buzz"]
示例 3：
	输入：n = 15
	输出：			["1","2","Fizz","4","Buzz","Fizz","7","8","Fizz","Buzz","11","Fizz","13","14","FizzBuzz"]
```

**代码**

```c
//如果直接用 strcpy会出现 *** buffer overflow detected ***: terminated错误
char *g1 = "FizzBuzz";
char *g2 = "Fizz";
char *g3 = "Buzz";

char ** fizzBuzz(int n, int* returnSize){
    char ** str = (char **)malloc(sizeof(char *) * n);
    int i;
    for(i = 1;i <= n;i++){
        str[i - 1] = (char *)malloc(sizeof(char) * 8);
        if(i % 3 == 0 && i % 5 == 0){
            str[i-1] = g1;
        } else if(i % 3 == 0){
            str[i-1] = g2;
        } else if(i % 5 == 0){
            str[i-1] = g3;
        } else{
            sprintf(str[i-1],"%d",i);
        }
    }
    *returnSize = n;
    return str;
}
```



## 44、第三大的数(LC 414)

给你一个非空数组，返回此数组中 第三大的数 。如果不存在，则返回数组中最大的数。

 **示例**

```
示例 1：
    输入：[3, 2, 1]
    输出：1
    解释：第三大的数是 1 。
示例 2：
    输入：[1, 2]
    输出：2
    解释：第三大的数不存在, 所以返回最大的数 2 。
示例 3：
    输入：[2, 2, 3, 1]
    输出：1
    解释：注意，要求返回第三大的数，是指在所有不同数字中排第三大的数。
    此例中存在两个值为 2 的数，它们都排第二。在所有不同数字中排第三大的数为 1 。
```

**代码**

```c
int thirdMax(int* nums, int numsSize){
    int result[3] = {0};
    int i,j;
    //冒泡排序排3次 降序
    for(i = 0;i < numsSize-1;i++){
        for(j = 0;j <numsSize-i-1;j++){
            if(nums[j] < nums[j+1]){
                int temp = nums[j];
                nums[j] = nums[j+1];
                nums[j+1] = temp;
            }
        }
    }
    //赋值到结果数组
    int flag = 0;
    int tag = 0;
    for(j = 0;j < numsSize;j++){
        if(tag == 3)    break;
        result[tag] = nums[j];
        while(result[tag] == nums[j+1 >= numsSize ? j : j+1]){
            if(j+1 == numsSize)
                break;
            j++;
        }
        printf("%d ",result[tag]);
        tag++;
    }
        
    return tag == 3 ? result[2] : result[0];
}
```



## 45、字符串相加

给定两个字符串形式的非负整数 num1 和num2 ，计算它们的和并同样以字符串形式返回。

你不能使用任何內建的用于处理大整数的库（比如 BigInteger）， 也不能直接将输入的字符串转换为整数形式。

**示例**

 ```
 示例 1：
 	输入：num1 = "11", num2 = "123"
 	输出："134"
 示例 2：
 	输入：num1 = "456", num2 = "77"
 	输出："533"
 示例 3：
 	输入：num1 = "0", num2 = "0"
 	输出："0"
 ```

**代码**

暴力法  字符串->数组->相加(考虑进位的实现)->字符串->考虑边界条件(2个两位数字相加构成3位的情况)->返回结果

```c
char * addStrings(char * num1, char * num2){
    int i = 0;
    int len1 = strlen(num1);
    int len2 = strlen(num2);
    int maxLen = len1 > len2 ? len1 : len2;
    //生成间接数组,存放各位
    int * nums1 = malloc(sizeof(int) * maxLen);
    int * nums2 = malloc(sizeof(int) * maxLen);
    for(i = 0;i < maxLen;i++){
        nums1[i] = nums2[i] = 0;
    }
    //取各位
    int tag = maxLen - 1;   //从末尾开始赋值,长度不够前面都为0
    for(i = len1 - 1;i >= 0;i--){
        nums1[tag--] = num1[i] - '0';
    }
    tag = maxLen - 1;
    for(i = len2-1;i >= 0;i--){
        nums2[tag--] = num2[i]  - '0';;
    }

    //赋值完毕开始相加
    int * result = malloc(sizeof(int)*(maxLen+1));  //生成结果数组
    for(i = 0;i < maxLen;i++){
        result[i]  = 0;
    }
    tag = 0;        //进位符号
    for(i = maxLen - 1;i >= 0;i--){
        if(tag == 1){
            result[i] += tag;   //进位
            tag = 0;
        }  
        result[i] += nums1[i] + nums2[i];
        if(result[i] >= 10){
            tag = 1;
            result[i] %= 10;
        } 
    }

    //转换为字符串
    char * str = malloc(sizeof(char) * (maxLen+1));
    for(i = 0;i < maxLen;i++){
        str[i] = result[i] + '0';
    }
    str[maxLen] = '\0';
    //没有进位. 这里需要处理进位的情况 19 + 91 = 110 结果为 10  -> 
    char * final = malloc(sizeof(char) * (maxLen+2));
    final[0] = '1';
    for(i = 0;i < maxLen;i++){
        final[i+1] = str[i];
    }
    final[maxLen+1] = '\0';
    return tag == 0 ? str : final;
}
```



## 46、字符串中的单词数

统计字符串中的单词个数，这里的单词指的是连续的不是空格的字符。

请注意，你可以假定字符串里不包括任何不可打印的字符。

**示例**

```
输入: "Hello, my name is John"
输出: 5
解释: 这里的单词是指连续的不是空格的字符，所以 "Hello," 算作 1 个单词。
```

**代码**

主要讲究理解题意 懂了就很简单

```c
int countSegments(char * s){
    int size = 0;
    char pre = ' ';
    //上一个是空格,下一个不是空格就是一个单词
    //' m' ' ,' 这里是从头部进行判断是否是一个单词
    while(*s){
        if(pre == ' ' && *s !=  ' ')
            size++;
        pre = *s;
        s++;
    }
    return size;
}
```



## 47、找到数组中消失的数(LC 448)

给你一个含 n 个整数的数组 nums ，其中 nums[i] 在区间 [1, n] 内。请你找出所有在 [1, n] 范围内但没有出现在 nums 中的数字，并以数组的形式返回结果。

 **示例**

```
示例 1：
    输入：nums = [4,3,2,7,8,2,3,1]
    输出：[5,6]
示例 2：
    输入：nums = [1,1]
    输出：[2]
```

**代码**

**间接空间** 借用 MAP 表存储出现次数复杂度为 $O(n)$

实质上也可以使用一个数组存放出现的数, 如 {1,2,3,4,5,5,6,7} 8个长度, 生成一个长度为8的数组空间, 初始化为0 。 计数 - 当出现该数就在对应的位置次数加1,最后依旧打印次数为0的数组即可。

```c
typedef struct Hash{
    int value;
    int times;
}Hash;

int* findDisappearedNumbers(int* nums, int numsSize, int* returnSize){
    //使用Hash表
    Hash * hash = malloc(sizeof(Hash) * numsSize);
    //初始化次数
    int i;
    for(i = 0;i < numsSize;i++){
        hash[i].times = 0;
    }
    //计数
    for(i = 0;i < numsSize;i++){
        hash[nums[i]-1].value = nums[i];
        hash[nums[i]-1].times++;
    }
    //查找为0的数
    int  tag = 0;
    int * result = malloc(sizeof(int)*numsSize);
    for(i = 0;i < numsSize;i++){
        if(hash[i].times == 0){
            result[tag++] = i+1;
        }
    }
    *returnSize = tag;
    return result;
}
```



## 48、排列硬币(LC 441)

你总共有 n 枚硬币，并计划将它们按阶梯状排列。对于一个由 k 行组成的阶梯，其第 i 行必须正好有 i 枚硬币。阶梯的最后一行 可能 是不完整的。

给你一个数字 n ，计算并返回可形成 完整阶梯行 的总行数。

 **示例**

![image-20211102200138525](img/image-20211102200138525.png)

```
输入：n = 5
输出：2
解释：因为第三行不完整，所以返回 2 。

输入：n = 8
输出：3
解释：因为第四行不完整，所以返回 3 。
```

**代码**

暴力法 使用long存放数据满足数据上限, 但是做了许多无效比较, 效率不高, 可以使用二分查找优化

```c
int arrangeCoins(int n){
    long  i = 0;
    //等差数列公式  n(n+1)/2
    while(i*(i+1)/2 <= n) {
        i++;
    }
    return i-1;
}
```



## 49、最小操作次数使数组元素相等

给你一个长度为 n 的整数数组，每次操作将会使 n - 1 个元素增加 1 。返回让数组所有元素相等的最小操作次数。

 **示例**

```
示例 1：
	输入：nums = [1,2,3]
	输出：3
	解释：
	只需要3次操作（注意每次操作会增加两个元素的值）：
	[1,2,3]  =>  [2,3,3]  =>  [3,4,3]  =>  [4,4,4]
示例 2：
	输入：nums = [1,1,1]
	输出：0
```

**代码**

```c
// 思路一
// sum + m * (n - 1) = x * n  
// sum 为数组当前和, m 为待求的move次数, x 为相加完成后的元素值, n 为数组大小
// 假设当前数组最小元素为 min 那么有 m = x - min (这里因为最小的元素一定是相加次数最多的且恰好等于 m)
// 故 x = m + min 那么 原方程变为 sum + m * (n - 1) = (m + min) * n  => m = sum - min * n

// 思路二 反向思维
// 每次使 n - 1 个元素 +1 增加到 所有元素相等的问题 等价于
// 每次使 1 个元素 -1 减小到 所有元素等于最小值

int compare(const void * a, const void * b)
{
   return ( *(int*)a - *(int*)b );
}

int minMoves(int* nums, int numsSize){
    //排序获得最小的值
    qsort(nums,numsSize,sizeof(int),compare);
    int min = nums[0];
    int ans = 0,i;
    for(i = 0; i < numsSize; i++){
        ans += nums[i] - min;
    }
    return ans;
}
```



## 50、重复的子字符串(LC 459)

给定一个非空的字符串，判断它是否可以由它的一个子串重复多次构成。给定的字符串只含有小写英文字母，并且长度不超过10000。

**示例**

```
示例 1:
	输入: "abab"
	输出: True
	解释: 可由子字符串 "ab" 重复两次构成。
示例 2:
	输入: "aba"
	输出: False
示例 3:
	输入: "abcabcabcabc"
	输出: True
	解释: 可由子字符串 "abc" 重复四次构成。 (或者子字符串 "abcabc" 重复两次构成。)
```

**代码**

```c
// 该题的思路在于, 给出的串s 一定是一个重复串
// 且该串的最多由其串长一般的子串构成  abcabc 由 abc 组成(而不可能是 abcd 组成)  ->  i <= len / 2
// 而且由于是重复构成那么,子串长度是父串长度的因数  ->   lenof(s) % lenof(subS) == 0    
// 枚举即可 
bool repeatedSubstringPattern(char * s){
    int len = strlen(s);        //字符串长度
    int match = 0,i;
    for(i = 1;i *2 <= len;i++){
        if(len % i == 0){
            //分割串
            int j;  
            for (j = i; j < len; j++) {
                if (s[j] == s[j - i]) {
                    match = 1;
                } else {
                    match = 0;
                    break;
                }
            }
            if (match == 1) {
                return true;
            }
        }
    }
    return false;
}
```



## 51、岛屿的周长(LC 463)

给定一个 row x col 的二维网格地图 grid ，其中：grid[i][j] = 1 表示陆地， grid[i][j] = 0 表示水域。

网格中的格子 水平和垂直 方向相连（对角线方向不相连）。整个网格被水完全包围，但其中恰好有一个岛屿（或者说，一个或多个表示陆地的格子相连组成的岛屿）。

岛屿中没有“湖”（“湖” 指水域在岛屿内部且不和岛屿周围的水相连）。格子是边长为 1 的正方形。网格为长方形，且宽度和高度均不超过 100 。计算这个岛屿的周长。

**示例**

![image-20211103155312779](img/image-20211103155312779.png)

```c
示例 1：
	输入：grid = [[0,1,0,0],[1,1,1,0],[0,1,0,0],[1,1,0,0]]
	输出：16
	解释：它的周长是上面图片中的 16 个黄色的边
示例 2：
	输入：grid = [[1]]
	输出：4
示例 3：
	输入：grid = [[1,0]]
	输出：4
```

**代码**

暴力迭代 - 计算所有1, 减去重复边, 即得结果

```c
int islandPerimeter(int** grid, int gridSize, int* gridColSize){
    //总的周长 4 * 16 = 64 
    //1所对应格子的边长,有重复 4 * 7 = 28
    //对于一个格子 有几个相邻的 1 就减去多少重复计算的边  最后即为结果

    int i,j;
    int totalSize = 0;
    //减去 0 对应的边长 - 现在得到的是带重复边的边长
    for(i = 0;i < gridSize;i++){
        for(j = 0;j < gridColSize[i];j++){
            if(grid[i][j] == 1)
                totalSize += 4;
        }
    }
    //考虑1之间的关系 这里使用间接数组, 给它周围补一圈 0  
    //避免复杂的边界判断,空间可以尽可能大一点
    //生成间接数组 
    int ** temp = malloc(sizeof(int *) * (gridSize+2));     //行数+2
    //找到最大列数, 防止空间不足
    int max = 0;
    for(i = 0;i < gridSize;i++)
        max = fmax(max,gridColSize[i]);
    //分配空间
    for(i = 0;i < gridSize+2;i++){
        temp[i] = malloc(sizeof(int)*(max+2));
    }
    //初始化赋值为0
    for(i = 0;i < gridSize+2;i++)
        for(j = 0;j < max+2;j++)
            temp[i][j] = 0;
    //为间接数组赋值陆地的情况
    for(i = 1;i < gridSize+1;i++)
        for(j = 1;j < max+1;j++)
            temp[i][j] = grid[i-1][j-1]; 
    
    //构建完毕开始比较
    for(i = 1;i < gridSize+1;i++){
        for(j = 1;j < max+1;j++){
            if(temp[i][j] == 1){
                //上为 1
                if(temp[i-1][j] == 1)
                    totalSize--;
                //下为 1
                if(temp[i+1][j] == 1)
                    totalSize--;
                //左为 1
                if(temp[i][j-1] == 1)
                    totalSize--;
                //右为 1
                if(temp[i][j+1] == 1)
                    totalSize--;
            }
        }
    }
    return totalSize;
}
```



## 52、数字的补数(LC 476)

对整数的二进制表示取反（0 变 1 ，1 变 0）后，再转换为十进制表示，可以得到这个整数的补数。

例如，整数 5 的二进制表示是 "101" ，取反后得到 "010" ，再转回十进制表示得到补数 2 。
给你一个整数 num ，输出它的补数。

 **示例**

```c
示例 1：
	输入：num = 5
	输出：2
	解释：5 的二进制表示为 101（没有前导零位），其补数为 010。所以你需要输出 2 。
示例 2：
	输入：num = 1
	输出：0
	解释：1 的二进制表示为 1（没有前导零位），其补数为 0。所以你需要输出 0 。
```

**代码**

暴力转换 - 转换为二进制保存到数组再依次取反, 然后转换为10进制保存。

```c
int findComplement(int num){
    //计算长度
    int temp = num;
    int len = 0;
    while(temp){
        temp /= 2;
        len++;
    }
    //转换为2进制, 保存到数组
    int * nums= malloc(sizeof(int) * len);
    int tag = 0,i;
    while(num){
        nums[tag++] = num % 2;
        num /= 2;
    }
    //按位取反
    for(i = 0;i < tag;i++)
        nums[i] = nums[i] == 0 ? 1 : 0;
    //转换为数字
    int result = 0;
    for(i = 0;i < tag;i++)
        result += nums[i] * pow(2,i);
    return result;
}
```



## 53、最大连续1个个数(LC 485)

给定一个二进制数组， 计算其中最大连续 1 的个数。

**示例**

```
输入：[1,1,0,1,1,1]
输出：3
解释：开头的两位和最后的三位都是连续 1 ，所以最大连续 1 的个数是 3.
```

**代码**

简单题 - 依次遍历即可

```c
int findMaxConsecutiveOnes(int* nums, int numsSize){
    int tag = 0,i,max = 0;
    for(i = 0;i < numsSize;i++){
        if(nums[i] == 0) 
            tag = 0;
        else
            tag++;
        max = fmax(tag,max);
    }
    return max;
}
```



## 54、构造矩形(LC 492)

作为一位web开发者， 懂得怎样去规划一个页面的尺寸是很重要的。 现给定一个具体的矩形页面面积，你的任务是设计一个长度为 L 和宽度为 W 且满足以下要求的矩形的页面。要求：

1. 你设计的矩形页面必须等于给定的目标面积。

2. 宽度 W 不应大于长度 L，换言之，要求 L >= W 。

3. 长度 L 和宽度 W 之间的差距应当尽可能小。
你需要按顺序输出你设计的页面的长度 L 和宽度 W。

**示例**

```
输入: 4
输出: [2, 2]
解释: 目标面积是 4， 所有可能的构造方案有 [1,4], [2,2], [4,1]。
但是根据要求2，[1,4] 不符合要求; 根据要求3，[2,2] 比 [4,1] 更能符合要求. 所以输出长度 L 为 2， 宽度 W 为 2。
```

**代码**

暴力法 遍历即可, 这里巧妙的点在于从 sqrt(area) 的点开始, 减少了一半的无效遍历

```
int* constructRectangle(int area, int* returnSize){
    //找area的公因数 然后根据规则划分即可 最优方案是 sqrt(area)
    //因此遍历时 边长初始为 sqrt(area) 然后依次遍历找到第一个符合的值即为次优方案
    int * result = malloc(sizeof(int) * 2);
    *returnSize = 2;
    int num = sqrt(area);
    if(pow(num,2) == area)
        result[0] = result[1] = sqrt(area);
    else{
        int i = 0,j;
        for(i = num;i <= area;i++){
            for(j = 1;i * j <= area;j++){
                if(i * j == area && i > j){
                    result[0] = i;
                    result[1] = j;
                    return result;
                }
            }
        }
    }
    
    return result;
}
```



## 55、提莫攻击(LC 495)

在《英雄联盟》的世界中，有一个叫 “提莫” 的英雄，他的攻击可以让敌方英雄艾希（编者注：寒冰射手）进入中毒状态。现在，给出提莫对艾希的攻击时间序列和提莫攻击的中毒持续时间，你需要输出艾希的中毒状态总时长。

你可以认为提莫在给定的时间点进行攻击，并立即使艾希处于中毒状态。

 **示例**

```c
示例1:
    输入: [1,4], 2
    输出: 4
    原因: 第 1 秒初，提莫开始对艾希进行攻击并使其立即中毒。中毒状态会维持 2 秒钟，直到第 2 秒末结束。
    第 4 秒初，提莫再次攻击艾希，使得艾希获得另外 2 秒中毒时间。
    所以最终输出 4 秒。
示例2:
    输入: [1,2], 2
    输出: 3
    原因: 第 1 秒初，提莫开始对艾希进行攻击并使其立即中毒。中毒状态会维持 2 秒钟，直到第 2 秒末结束。
    但是第 2 秒初，提莫再次攻击了已经处于中毒状态的艾希。
    由于中毒状态不可叠加，提莫在第 2 秒初的这次攻击会在第 3 秒末结束。
    所以最终输出 3 。
```

**代码**

暴力法 - 迭代判断即可

```
int findPoisonedDuration(int* timeSeries, int timeSeriesSize, int duration){
    //根据两个时序序列的差值来判断中毒时间
    int i = 0;
    //由于判断是否重复中毒只判断 timeSeriesSize - 1次, 因此少了依次 duration 累加的步骤, 这里进行添加
    int seconds = duration;         
    //去掉时间间隔
    for(i = 0;i < timeSeriesSize - 1;i++){
        seconds += duration;
        //减去时间间隔内的重复中毒时间
        if(timeSeries[i+1] - timeSeries[i] <= duration)
            seconds -= duration - (timeSeries[i+1] - timeSeries[i]);
    }
    return seconds;
}
```



## 56、下一个更大元素 i(LC 496)

给你两个 没有重复元素 的数组 nums1 和 nums2 ，其中nums1 是 nums2 的子集。

请你找出 nums1 中每个元素在 nums2 中的下一个比其大的值。

nums1 中数字 x 的下一个更大元素是指 x 在 nums2 中对应位置的右边的第一个比 x 大的元素。如果不存在，对应位置输出 -1 。

**示例**

```
示例 1:
    输入: nums1 = [4,1,2], nums2 = [1,3,4,2].
    输出: [-1,3,-1]
    解释:
        对于 num1 中的数字 4 ，你无法在第二个数组中找到下一个更大的数字，因此输出 -1 。
        对于 num1 中的数字 1 ，第二个数组中数字1右边的下一个较大数字是 3 。
        对于 num1 中的数字 2 ，第二个数组中没有下一个更大的数字，因此输出 -1 。
示例 2:
    输入: nums1 = [2,4], nums2 = [1,2,3,4].
    输出: [3,-1]
    解释:
        对于 num1 中的数字 2 ，第二个数组中的下一个较大数字是 3 。
        对于 num1 中的数字 4 ，第二个数组中没有下一个更大的数字，因此输出 -1 。
```

**代码**

暴力法 - 遍历

```c
int* nextGreaterElement(int* nums1, int nums1Size, int* nums2, int nums2Size, int* returnSize){
    //暴力遍历
    int i = 0,j;
    int * nums = malloc(sizeof(int) * nums1Size);
    *returnSize = nums1Size;
    int tag;        //是否查找到nums1元素在nums2中的位置 1 查找到
    for(i = 0;i <nums1Size;i++){
        tag = 0;
        for(j = 0;j < nums2Size;j++){
            if(nums1[i] == nums2[j]) tag = 1;
            if(nums1[i] < nums2[j] && tag == 1){
                nums[i] = nums2[j];
                break;
            }
        }
        if(j == nums2Size)
            nums[i] = -1;
    }
    return nums;
}
```



## 57、键盘行(LC 500)

给你一个字符串数组 words ，只返回可以使用在 美式键盘 同一行的字母打印出来的单词。键盘如下图所示。

美式键盘 中：

第一行由字符 "qwertyuiop" 组成。
第二行由字符 "asdfghjkl" 组成。
第三行由字符 "zxcvbnm" 组成。

**示例**

![image-20211103182749987](img/image-20211103182749987.png)

```
示例 1：
	输入：words = ["Hello","Alaska","Dad","Peace"]
	输出：["Alaska","Dad"]
示例 2：
	输入：words = ["omk"]
	输出：[]
示例 3：
	输入：words = ["adsdf","sfd"]
	输出：["adsdf","sfd"]
```

**代码**

```c
char ** findWords(char ** words, int wordsSize, int* returnSize){
    //暴力 判断是否属于3个子串即可
    char * str = "12210111011122000010020202";
    int i,j,tag=0;
    int * result = malloc(sizeof(int) * wordsSize);
    for(i = 0;i < wordsSize;i++){
        char * temp = words[i];
        int cur = str[*temp < 'a' ? *temp + ' ' - 'a' : *temp - 'a'];     //记录首个字符属于哪一类
        while(*temp){
            //大写转小写
            if(str[*temp < 'a' ? *temp + ' ' - 'a' : *temp - 'a'] != cur)
                break;
            temp++;
        }
        if(*temp == '\0'){
            result[i] = 1;
            tag++;
        }      
    }


    //分配空间
    char ** reWords = malloc(sizeof(char *) * tag);
    int cur = 0;
    for(i = 0;i < wordsSize;i++){
        if(result[i] == 1){
            reWords[cur] = malloc(sizeof(char) * (strlen(words[i])+1));
            strcpy(reWords[cur],words[i]);
            cur++;
        }
    }   
    * returnSize = tag;
    return reWords;
}
```



## 58、七进制数(LC 504)

给定一个整数 num，将其转化为 7 进制，并以字符串形式输出。

 **示例**

```
示例 1:
	输入: num = 100
	输出: "202"
示例 2:
	输入: num = -7
	输出: "-10"
```

**代码**

借用了一些自己定义的API - 数字转7进制数组  -> 数组翻转 -> 整型数组转字符数组

(正负的区分是通过 abs取绝对值然后加负号实现的)

```c
/*
 * 输入: 数组 可返回的长度
 * 输出: 转换后的二进制的数组  数组长度参数
 * 说明: 该数组返回的数组结果从小端的 从个位开始
*/
int * tenToSeven(int num,int * size){
    //计算长度
    int temp = abs(num);
    int len = 0;
    while(temp){
        temp /= 7;
        len++;
    }
    *size = len;
    //转换为2进制, 保存到数组
    int * nums= malloc(sizeof(int) * len);
    int tag = 0,i;
    num = abs(num);
    while(num){
        nums[tag++] = num % 7;
        num /= 7;
    }
    return nums;
}

/*
 * 输入: 数组 长度
 * 输出: 翻转后的数组
*/
int * reverse(int * nums,int size){
    int i,j;
    for(i = 0;i < size/2;i++){
        int temp = nums[i];
        nums[i] = nums[size-i-1];
        nums[size-i-1] = temp;
    }
    return nums;
}

char * convertToBase7(int num){
    if(num == 0){
        char * str = malloc(sizeof(char) * (2));
        str[0] = '0';
        str[1] = '\0';
        return str;
    }

    int size;
    int * nums = tenToSeven(num,&size);
    int i;
    reverse(nums,size);
    //分配空间
    char * str = malloc(sizeof(char) * (size+2));
    int tag = 0;        //判断是否是负数
    //如果是负数加上负号
    if(num < 0){
        str[0] = '-';
        tag = 1;
    }
  
    for(i = 0;i < size;i++){
        str[i+tag] = nums[i] + '0';
    }
    str[i+tag] = '\0';
    return str;
}
```



## 59、相对名次(LC 506)

给出 N 名运动员的成绩，找出他们的相对名次并授予前三名对应的奖牌。前三名运动员将会被分别授予 “金牌”，“银牌” 和“ 铜牌”（"Gold Medal", "Silver Medal", "Bronze Medal"）。

(注：分数越高的选手，排名越靠前。)

**示例**

```
示例 1:
    输入: [5, 4, 3, 2, 1]
    输出: ["Gold Medal", "Silver Medal", "Bronze Medal", "4", "5"]
    解释: 前三名运动员的成绩为前三高的，因此将会分别被授予 “金牌”，“银牌”和“铜牌” ("Gold Medal", 
    "Silver Medal" and "Bronze Medal").
    余下的两名运动员，我们只需要通过他们的成绩计算将其相对名次即可。
```

**代码**

**排序** 使用间接数组存放排序后的下标, 根据位于前3名的下标修改对应的字符串。

这里二维数组不能定义, 必须malloc。 因此字符串必须要作为常量空间进行赋值, 同时使用sprintf 函数转换int为字符型。

```c
/**
 * Note: The returned array must be malloced, assume caller calls free().
 */
char ** findRelativeRanks(int* score, int scoreSize, int* returnSize){
    int i,j;
    int * nums = malloc(sizeof(int) * scoreSize);
    //初始化nums数组
    for(i = 0;i < scoreSize;i++)    nums[i] = i;
    //冒泡排序
    for(i = 0;i < scoreSize - 1;i++){
        for(j = 0;j < scoreSize - i - 1;j++){
            if(score[j] < score[j+1]){
                //交换数值
                int temp = score[j];
                score[j] = score[j+1];
                score[j+1] = temp;
                //交换下标
                temp = nums[j];
                nums[j] = nums[j+1];
                nums[j+1] = temp;
            }
        }
    }


    //生成结果字符串
    char ** result = malloc(sizeof(char *) * scoreSize);
    
    //存放结果
    for(i = 0;i < scoreSize;i++) {
        if(i == 0)
            result[nums[i]] = "Gold Medal";
        else if(i == 1)
            result[nums[i]] = "Silver Medal";
        else if(i == 2)
            result[nums[i]] = "Bronze Medal";
        else{
            result[nums[i]] = malloc(sizeof(char) * 6);
            sprintf(result[nums[i]],"%d",i+1);
        }
    }
    * returnSize = scoreSize;
    return result;
}
```



## 60、完美数

对于一个 正整数，如果它和除了它自身以外的所有 正因子 之和相等，我们称它为 「完美数」。

给定一个 整数 n， 如果是完美数，返回 true，否则返回 false

**示例**

```
示例 1：
	输入：28
	输出：True
	解释：28 = 1 + 2 + 4 + 7 + 14
	1, 2, 4, 7, 和 14 是 28 的所有正因子。
示例 2：
	输入：num = 6
	输出：true
示例 3：
	输入：num = 496
	输出：true
示例 4：
	输入：num = 8128
	输出：true
示例 5：
	输入：num = 2
	输出：false
```

**代码**

暴力迭代

```
bool checkPerfectNumber(int num){
    //获取所有的因子
    int i,tag=0;
    int * result = malloc(sizeof(int) * (num/2));   //因子数不可能超过 num / 2个
    //这里取开方缩减执行时间, 在开方数之下我们就可以获取到所有的因子
    for(i = 1;i < sqrt(num);i++){
        if(num % i == 0){
            result[tag++] = i;
            //避免计算到 num 本身
            if(num / i  != num)
                result[tag++] = num / i;
        }
    }
    int sum = 0;
    for(i = 0;i < tag;i++){
        sum += result[i];
    }
    if(sum == num)
        return true;
    return false;
}
```



## 61、斐波那契数(LC 509)

斐波那契数，通常用 F(n) 表示，形成的序列称为 斐波那契数列 。该数列由 0 和 1 开始，后面的每一项数字都是前面两项数字的和。也就是：

F(0) = 0，F(1) = 1
F(n) = F(n - 1) + F(n - 2)，其中 n > 1
给你 n ，请计算 F(n) 。

 **示例**

```
示例 1：
	输入：2
	输出：1
	解释：F(2) = F(1) + F(0) = 1 + 0 = 1
示例 2：
	输入：3
	输出：2
	解释：F(3) = F(2) + F(1) = 1 + 1 = 2
示例 3：
	输入：4
	输出：3
	解释：F(4) = F(3) + F(2) = 2 + 1 = 3
```

**代码**

递归

```
int fib(int n){
    if(n == 0)
        return 0;
    if(n == 1)
        return 1;
    return fib(n-1) + fib(n-2);
}
```



## 62、检测大写字母(LC 520)

给定一个单词，你需要判断单词的大写使用是否正确。

我们定义，在以下情况时，单词的大写用法是正确的：

全部字母都是大写，比如"USA"。
单词中所有字母都不是大写，比如"leetcode"。
如果单词不只含有一个字母，只有首字母大写， 比如 "Google"。
否则，我们定义这个单词没有正确使用大写字母。

**示例**

```
示例 1:
	输入: "USA"
	输出: True
示例 2:
	输入: "FlaG"
	输出: False
注意: 输入是由大写和小写拉丁字母组成的非空单词。
```

**代码**

判断错误条件 判决器

```c
bool detectCapitalUse(char * word){
    int len = strlen(word); //字符串长度
    int flag1 = 0,flag2 = 0;    //flag1 判断是否有小写字母 flag2 判断是否有大写字母
    char * temp = word;
    temp++;     //不比较第1位
    while(*temp){
        if(*temp - 'a' >= 0)
            flag1 = 1;
        if(*temp - 'a' < 0)
            flag2 = 1;
        temp++;
    }

    //判断  "Flag"     "mL" 两种情形, 其余都是对的   
    return (flag1 == 1 && flag2 == 1) || (*word - 'a' >= 0 && flag2 == 1)? false : true;
}
```



## 63、最长特殊序列 I (LC 521)

给你两个字符串，请你从这两个字符串中找出最长的特殊序列。

「最长特殊序列」定义如下：该序列为某字符串独有的最长子序列（即不能是其他字符串的子序列）。

子序列 可以通过删去字符串中的某些字符实现，但不能改变剩余字符的相对顺序。空序列为所有字符串的子序列，任何字符串为其自身的子序列。

输入为两个字符串，输出最长特殊序列的长度。如果不存在，则返回 -1。

 **示例**

```
示例 1：
	输入: "aba", "cdc"
	输出: 3
	解释: 最长特殊序列可为 "aba" (或 "cdc")，两者均为自身的子序列且不是对方的子序列。
示例 2：
	输入：a = "aaa", b = "bbb"
	输出：3
示例 3：
	输入：a = "aaa", b = "aaa"
	输出：-1
```

**代码**

官方解法 取了所有情形思考,  判决所有情形即可, 不再附其它方法。

![image-20211104154821773](img/image-20211104154821773.png)

```
int findLUSlength(char * a, char * b){
    return !strcmp(a,b) ? -1 : fmax(strlen(a),strlen(b));
}
```



## 64、学生出勤记录I(LC 551)

给你一个字符串 s 表示一个学生的出勤记录，其中的每个字符用来标记当天的出勤情况（缺勤、迟到、到场）。记录中只含下面三种字符：

'A'：Absent，缺勤
'L'：Late，迟到
'P'：Present，到场
如果学生能够 同时 满足下面两个条件，则可以获得出勤奖励：

按 总出勤 计，学生缺勤（'A'）严格 少于两天。
学生 不会 存在 连续 3 天或 连续 3 天以上的迟到（'L'）记录。
如果学生可以获得出勤奖励，返回 true ；否则，返回 false 。

 **示例**

```
示例 1：
	输入：s = "PPALLP"
	输出：true
	解释：学生缺勤次数少于 2 次，且不存在 3 天或以上的连续迟到记录。
示例 2：
	输入：s = "PPALLL"
	输出：false
	解释：学生最后三天连续迟到，所以不满足出勤奖励的条件。
```

**代码**

```c
bool checkRecord(char * s){
    int countA = 0,countL = 0;
    //显然如题意所述, countA < 2 countL < 3
    //当然countL 是需要连续的 3 个 L 才可计数, 我们可以对其每一次比较
    //自动 - 1, 直到减为0 。 这里借用的是投票的思想 
    while(*s){
        if(*s == 'L')
            countL++;  
        if(*s == 'A')
            countA++;
        //如果不是 L 重置countL
        if(*s != 'L')
            countL = 0;
        s++;
        //终止条件
        if(countL == 3 || countA == 2)
            return false;
    }
    return true;
}
```



## 65、数组拆分I(LC 561)

给定长度为 2n 的整数数组 nums ，你的任务是将这些数分成 n 对, 例如 (a1, b1), (a2, b2), ..., (an, bn) ，使得从 1 到 n 的 min(ai, bi) 总和最大。

返回该 最大总和 。

 **示例**

```
示例 1：
	输入：nums = [1,4,3,2]
	输出：4
	解释：所有可能的分法（忽略元素顺序）为：
	1. (1, 4), (2, 3) -> min(1, 4) + min(2, 3) = 1 + 2 = 3
	2. (1, 3), (2, 4) -> min(1, 3) + min(2, 4) = 1 + 2 = 3
	3. (1, 2), (3, 4) -> min(1, 2) + min(3, 4) = 1 + 3 = 4
   所以最大总和为 4
示例 2：
	输入：nums = [6,2,6,5,1,2]
	输出：9
	解释：最优的分法为 (2, 1), (2, 5), (6, 6). min(2, 1) + min(2, 5) + min(6, 6) = 
	1 + 2 + 6 = 9
```

**代码**

思考题 - 对排序后数组的低位进行相加 

```
int compare(const void * a, const void * b)
{
   return ( *(int*)a - *(int*)b );
}

//这里实质上就是对排序后数组的低位进行相加
//比如 1 2 2 5 6 6  我们能得到的最大解的情况一定是, 将其邻近的两个数值进行配对
//保留了对应的最大值, 因此我们只需要取排序结果的 左侧值(奇数值即可)
int arrayPairSum(int* nums, int numsSize){
    qsort(nums,numsSize,sizeof(int),compare);
    int result = 0,i;
    for(i = 0;i <numsSize;i+=2){
        result += nums[i];
    }
    return result;
}
```



## 66、分糖果(LC 575)

Alice 有 n 枚糖，其中第 i 枚糖的类型为 candyType[i] 。Alice 注意到她的体重正在增长，所以前去拜访了一位医生。

医生建议 Alice 要少摄入糖分，只吃掉她所有糖的 n / 2 即可（n 是一个偶数）。Alice 非常喜欢这些糖，她想要在遵循医生建议的情况下，尽可能吃到最多不同种类的糖。

给你一个长度为 n 的整数数组 candyType ，返回： Alice 在仅吃掉 n / 2 枚糖的情况下，可以吃到糖的最多种类数。

**示例**

```
示例 1：
	输入：candyType = [1,1,2,2,3,3]
	输出：3
	解释：Alice 只能吃 6 / 2 = 3 枚糖，由于只有 3 种糖，她可以每种吃一枚。
示例 2：
	输入：candyType = [1,1,2,3]
	输出：2
	解释：Alice 只能吃 4 / 2 = 2 枚糖，不管她选择吃的种类是 [1,2]、[1,3] 还是 [2,3]，她	
	只能吃到两种不同类的糖。
示例 3：
	输入：candyType = [6,6,6,6]
	输出：1
	解释：Alice 只能吃 4 / 2 = 2 枚糖，尽管她能吃 2 枚，但只能吃到 1 种糖。
```

**代码**

迭代法 - 使用 快速排序 进行排序, 然后根据排序结果去重记录糖果种类, 比较得出结果

```c
int compare(const void * a, const void * b)
{
   return ( *(int*)a - *(int*)b );
}
//使用 快速排序 进行排序, 然后根据排序结果去重记录糖果种类, 比较得出结果
int distributeCandies(int* candyType, int candyTypeSize){
    //计算最大能吃到多少糖
    int maxEat = candyTypeSize / 2;
    qsort(candyType,candyTypeSize,sizeof(int),compare);
    //获取有多少种不同的糖果
    int i,tag = candyType[0],type = 1;
    for(i = 1;i <candyTypeSize;i++){
        if(tag != candyType[i])
            type++;
        tag = candyType[i];
    }
    //printf("%d ",type);
    return type < maxEat ? type : maxEat;
}
```



## 67、范围求和II(LC 598)

给定一个初始元素全部为 0，大小为 m*n 的矩阵 M 以及在 M 上的一系列更新操作。

操作用二维数组表示，其中的每个操作用一个含有两个正整数 a 和 b 的数组表示，含义是将所有符合 0 <= i < a 以及 0 <= j < b 的元素 M[i][j] 的值都增加 1。

在执行给定的一系列操作后，你需要返回矩阵中含有最大整数的元素个数。

**示例**

```c
示例 1:

输入: 
m = 3, n = 3
operations = [[2,2],[3,3]]
输出: 4
解释: 
初始状态, M = 
[[0, 0, 0],
 [0, 0, 0],
 [0, 0, 0]]

执行完操作 [2,2] 后, M = 
[[1, 1, 0],
 [1, 1, 0],
 [0, 0, 0]]

执行完操作 [3,3] 后, M = 
[[2, 2, 1],
 [2, 2, 1],
 [1, 1, 1]]

M 中最大的整数是 2, 而且 M 中有4个值为2的元素。因此返回 4。
```

**代码**

思考题 - 由于每次操作都是从[0,0] -> [a,b] 所以只需要求最小的覆盖面积即可, 也即求最小的 a 和 b。

这里的覆盖 [2,1] 取 [0,0] [1,0]   ;  [1,2] 取 [0,1]  也即题示  0 <= i < a 以及 0 <= j < b  

```c
int maxCount(int m, int n, int** ops, int opsSize, int* opsColSize){
    //边界条件 [0,0]
    if(!opsSize)
        return m * n;
    //找最小的 a 和 最小的 b 考虑为0的情况
    int i,j,mina = ((unsigned)(-1))>>1,minb = ((unsigned)(-1))>>1;
    for(i = 0;i < opsSize;i++){
        mina = fmin(mina,ops[i][0]);
        minb = fmin(minb,ops[i][1]);
    }
    return mina == 0 ? minb : mina * minb;
}   
```



## 68、自除数

自除数 是指可以被它包含的每一位数除尽的数。

例如，128 是一个自除数，因为 128 % 1 == 0，128 % 2 == 0，128 % 8 == 0。

还有，自除数不允许包含 0 。

给定上边界和下边界数字，输出一个列表，列表的元素是边界（含边界）内所有的自除数。

**示例**

```
示例 1：
	输入： 
	上边界left = 1, 下边界right = 22
	输出： [1, 2, 3, 4, 5, 6, 7, 8, 9, 11, 12, 15, 22]
```

**代码**

暴力法 迭代即可

```c
/**
 * Note: The returned array must be malloced, assume caller calls free().
 */
int* selfDividingNumbers(int left, int right, int* returnSize){
    int i,j,tag = 0;
    int * nums = malloc(sizeof(int) * (right-left));
    for(i = left;i <= right;i++){
        //判断长度
        int temp = i,size = 0;   
        while(temp){
            temp /= 10;
            size++;
        }
        
        //取各位
        temp = i;
        int * temps = malloc(sizeof(int) * size);
        for(j = 0;j < size;j++){
            temps[j] = temp % 10;
            temp/=10;
        }

        //判断是否可以除尽
        for(j = 0;j < size;j++){
            //抛去为0的情况 必然不成立
            if(temps[j] == 0)
                break;
            if(i % temps[j] != 0)
                break;
        }
        if(j == size)
            nums[tag++] = i;
    }
    *returnSize = tag;
    return nums;
}
```



## 69、二进制求和(LC 67)

给你两个二进制字符串，返回它们的和（用二进制表示）。

输入为 非空 字符串且只包含数字 1 和 0。

 **示例**

```
示例 1:
	输入: a = "11", b = "1"
	输出: "100"
示例 2:
	输入: a = "1010", b = "1011"
	输出: "10101"
```

**代码**

字符串翻转后从个位考虑进位逐级相加,处理可能的最高位,再对结果进行翻转。

```c
/*
 * 输入: 字符数组 长度
 * 输出: 翻转后的数组
*/
char * reverseChar(char * str,int size){
    int i,j;
    for(i = 0;i < size/2;i++){
        int temp = str[i];
        str[i] = str[size-i-1];
        str[size-i-1] = temp;
    }
    return str;
}

/**
* 输入: 相加的二进制字符串 a b
* 输出: 相加后的结果字符串
* 思路: 字符串翻转后从个位考虑进位逐级相加,处理可能的最高位,再对结果进行翻转。
*/
char * plusBinary(char * a, char * b){
    int sizeA = strlen(a);
    int sizeB = strlen(b);
    reverseChar(a,sizeA);
    reverseChar(b,sizeB);
    int i = 0;
    int maxSize = fmax(sizeA,sizeB);
    //生成结果数组
    char * result = malloc(sizeof(char) * (maxSize+2));
    int tag = 0;        //实际否需要进位 1 需要 0 不需要
    for(i = 0;i < maxSize;i++){
        int plus = 0;
        if(sizeA > i && sizeB > i){
            plus = a[i] - '0' + b[i] - '0' + tag;
        } else if(sizeA <= i){
            plus = 0 + b[i] - '0' + tag;
        } else if(sizeB <= i){
            plus = a[i] - '0' + 0 + tag;
        }

        //考虑进位
        if(plus >= 2)
            tag = 1;
        else
            tag = 0;
        result[i] = plus % 2 + '0';
    }
    if(tag == 1){
        result[i] = tag + '0';
        result[i+1] = '\0';
    } else
        result[i] = '\0';
    reverseChar(result,strlen(result));
    return result;
}
```



## 70、有序数组转换为二叉搜索树(LC 108)

给你一个整数数组 nums ，其中元素已经按 升序 排列，请你将其转换为一棵 高度平衡 二叉搜索树。

高度平衡 二叉树是一棵满足「每个节点的左右两个子树的高度差的绝对值不超过 1 」的二叉树。

**示例**

![img](img/btree1.jpg)

![img](img/btree2.jpg)

![img](img/btree.jpg)

```
输入：nums = [-10,-3,0,5,9]
输出：[0,-3,9,-10,null,5]
解释：[0,-10,5,null,-3,null,9] 也将被视为正确答案：

输入：nums = [1,3]
输出：[3,1]
解释：[1,3] 和 [3,1] 都是高度平衡二叉搜索树。
```

**代码**

递归  每次选取最中间左侧的结点作为根节点进行划分重组

```c
//以升序数组的中间结点作为根节点, 左小右大的方式进行排列
struct TreeNode * helper(int* nums, int left, int right) {
    if (left > right) {
        return NULL;
    }

    // 总是选择中间位置左边的数字作为根节点
    int mid = (left + right) / 2;

    struct TreeNode* root = (struct TreeNode*)malloc(sizeof(struct TreeNode));
    root->val = nums[mid];
    root->left = helper(nums, left, mid - 1);
    root->right = helper(nums, mid + 1, right);
    return root;
}

struct TreeNode* sortedArrayToBST(int* nums, int numsSize) {
    return helper(nums, 0, numsSize - 1);
}
```



## 71、二叉树的最小深度(LC 111)

给定一个二叉树，找出其最小深度。

最小深度是从根节点到最近叶子节点的最短路径上的节点数量。

**说明：**叶子节点是指没有子节点的节点。

 **示例**

![img](img/ex_depth.jpg)

```
示例 1：
	输入：root = [3,9,20,null,null,15,7]
	输出：2
示例 2：
	输入：root = [2,null,3,null,4,null,5,null,6]
	输出：5
```

**代码**

**解法一 官方解法**

注意题目要求计算从根节点到叶子结点的最小深度, 因此只有一个根节点的情况是不符合要求的, 因此要忽略最坏情况,即树成为一个链表的情形, 即形成直线, 这时需要返回最大值而不是1。

```
int minDepth(struct TreeNode *root) {
    if (root == NULL) {
        return 0;
    }

    if (root->left == NULL && root->right == NULL) {
        return 1;
    }

    int min_depth = INT_MAX;
    if (root->left != NULL) {
        min_depth = fmin(minDepth(root->left), min_depth);
    }
    if (root->right != NULL) {
        min_depth = fmin(minDepth(root->right), min_depth);
    }

    return min_depth + 1;
}
```

**解法二**

 这里加一个判定即可, 也即只需要对最坏情况做处理即可

```c
int minDepth(struct TreeNode* root){
    if(!root)
        return 0;
    int len;
    if(root->left == NULL || root->right == NULL)
        len = fmax(minDepth(root->left),minDepth(root->right)) + 1;
    else
        len = fmin(minDepth(root->left),minDepth(root->right)) + 1;
    return len;
}
```



## 72、杨辉三角(LC 118)

给定一个非负整数 *`numRows`，*生成「杨辉三角」的前 *`numRows`* 行。

在「杨辉三角」中，每个数是它左上方和右上方的数的和。

![img](https://pic.leetcode-cn.com/1626927345-DZmfxB-PascalTriangleAnimated2.gif)

**示例**

```
示例 1:
	输入: numRows = 5
	输出: [[1],[1,1],[1,2,1],[1,3,3,1],[1,4,6,4,1]]
示例 2:
	输入: numRows = 1
	输出: [[1]]
```

**代码**

逻辑简单, 繁琐的点在于返回结果时, 必须 malloc 和 free 导致很多位置的 下标越界、指针访问错误的问题, 调 BUG 时间 巨长。

- 可返回的数组空间,以该写法为标准 

  ```
  (int**)malloc(sizeof(int*) * numRows   而不是
  	   malloc(sizeof(int*) * numRows)
  	   
  int ** nums = (int**)malloc(sizeof(int*) * numRows);
  *returnColumnSizes = (int*)malloc(numRows*sizeof(int));
  ```

- 尽量不要额外生成数组空间

  这里对 temp 数组的赋值, 出现 `addresssanitizer:DEAD` 类型错误

  ```
      //生成
      int * temp = (int)malloc(sizeof(int)*(numRows));
      for(i = 0;i < numRows-1;i++){
          //生成填充数据
          for(j = 0;j < i;j++){
              nums[i+1][j+1] = nums[i][j] + nums[i][j+1];
          }
      }
  ```

```c
int** generate(int numRows, int* returnSize, int** returnColumnSizes){
    //定义数组
    int ** nums = (int**)malloc(sizeof(int*) * numRows);
    *returnColumnSizes = (int*)malloc(numRows*sizeof(int));
    * returnSize = numRows;
    //分配空间
    int i = 0,j = 0;
    for(i = 0;i < numRows;i++){
        nums[i] = (int*)malloc(sizeof(int) * (i+1));
        (*returnColumnSizes)[i] = i+1;
    }
    //初始化边界
    for(i = 0;i < numRows;i++){
        nums[i][0] = 1;
        nums[i][i] = 1;
    }
    //生成
    int * temp = (int)malloc(sizeof(int)*(numRows));
    for(i = 0;i < numRows-1;i++){
        //生成填充数据
        for(j = 0;j < i;j++){
            nums[i+1][j+1] = nums[i][j] + nums[i][j+1];
        }
    }
    return nums;
}
```



## 73、杨辉三角 **II**(LC 119)

**示例**

给定一个非负索引 `rowIndex`，返回「杨辉三角」的第 `rowIndex` 行。

在「杨辉三角」中，每个数是它左上方和右上方的数的和。

```
示例 1:
	输入: rowIndex = 3
	输出: [1,3,3,1]
示例 2:
	输入: rowIndex = 0
	输出: [1]
示例 3:
	输入: rowIndex = 1
	输出: [1,1]
```

**代码**

```c
/**
 * Note: The returned array must be malloced, assume caller calls free().
 */
int** generate(int numRows, int* returnSize, int** returnColumnSizes){
    //定义数组
    int ** nums = (int**)malloc(sizeof(int*) * numRows);
    *returnColumnSizes = (int*)malloc(numRows*sizeof(int));
    * returnSize = numRows;
    //分配空间
    int i = 0,j = 0;
    for(i = 0;i < numRows;i++){
        nums[i] = (int*)malloc(sizeof(int) * (i+1));
        (*returnColumnSizes)[i] = i+1;
    }
    //初始化边界
    for(i = 0;i < numRows;i++){
        nums[i][0] = 1;
        nums[i][i] = 1;
    }
    //生成
    int * temp = (int)malloc(sizeof(int)*(numRows));
    for(i = 0;i < numRows-1;i++){
        //生成填充数据
        for(j = 0;j < i;j++){
            nums[i+1][j+1] = nums[i][j] + nums[i][j+1];
        }
    }
    return nums;
}

int * getRow(int rowIndex, int* returnSize){
    int * size;
    int ** returnColumnSizes = (int**)malloc(sizeof(int*) * 1);
    int ** result = generate(rowIndex+1,returnSize,returnColumnSizes);
    *returnSize = rowIndex+1;
    return result[rowIndex];
}
```



## 74、买卖股票的最佳时机(LC 121)

给定一个数组 prices ，它的第 i 个元素 prices[i] 表示一支给定股票第 i 天的价格。

你只能选择 某一天 买入这只股票，并选择在 未来的某一个不同的日子 卖出该股票。设计一个算法来计算你所能获取的最大利润。

返回你可以从这笔交易中获取的最大利润。如果你不能获取任何利润，返回 0 。

**示例**

```
示例 1：
    输入：[7,1,5,3,6,4]
    输出：5
    解释：在第 2 天（股票价格 = 1）的时候买入，在第 5 天（股票价格 = 6）的时候卖出，最大利润 = 6-1 = 5 。
         注意利润不能是 7-1 = 6, 因为卖出价格需要大于买入价格；同时，你不能在买入前卖出股票。
示例 2：
    输入：prices = [7,6,4,3,1]
    输出：0
    解释：在这种情况下, 没有交易完成, 所以最大利润为 0。
```

**代码**

暴力法 可以再优化一下  $O(n^2)$ 复杂度

```c
int maxProfit(int* prices, int pricesSize){
    //思路: 根本逻辑为低买高卖, 因此顺序取相差最大的两个数的差即可
    //      如果没有, 那么利润为0  借用冒泡排序的思想
    int i,j,salary = 0;
    for(i = pricesSize - 1;i > 0;i--){
        for(j = i-1;j >= 0;j--){
            salary = fmax(salary,prices[i] - prices[j]);
        }
    }
    return salary > 0 ? salary : 0;
}
```

**动态规划**

```
1. 记录【今天之前买入的最小值】
2. 计算【今天之前最小值买入，今天卖出的获利】，也即【今天卖出的最大获利】
3. 比较【每天的最大获利】，取最大值即可
```

```c
int maxProfit(int* prices, int pricesSize){
    //思路: 根本逻辑为低买高卖, 因此顺序取相差最大的两个数的差即可
    //      如果没有, 那么利润为0  借用冒泡排序的思想
    if(pricesSize <= 1)
        return 0;
    int min = prices[0], max = 0;
    int i;
    for(i = 1; i < pricesSize; i++) {
        max = fmax(max, prices[i] - min);
        min = fmin(min, prices[i]);
    }
    return max;
}
```



## 75、EXCEL 表列序号(LC 171)

给你一个字符串 columnTitle ，表示 Excel 表格中的列名称。返回该列名称对应的列序号。

例如，

    A -> 1
    B -> 2
    C -> 3
    ...
    Z -> 26
    AA -> 27
    AB -> 28 
    ...
    示例 1:
        输入: columnTitle = "A"
        输出: 1
    示例 2:
        输入: columnTitle = "AB"
        输出: 28
    示例 3:
        输入: columnTitle = "ZY"
        输出: 701
    示例 4:
        输入: columnTitle = "FXSHRXW"
        输出: 2147483647

**代码**

进制转换思想  字符串转 26 进制数

```c
/*
 * 输入: 字符数组 长度
 * 输出: 翻转后的数组
*/
char * reverseChar(char * str,int size){
    int i,j;
    for(i = 0;i < size/2;i++){
        int temp = str[i];
        str[i] = str[size-i-1];
        str[size-i-1] = temp;
    }
    return str;
}

//思路: 实质上就是进制转换(26进制)
int titleToNumber(char * columnTitle){
    //翻转数组, 从个位开始计数
    reverseChar(columnTitle,strlen(columnTitle));
    long result = 0;
    int tag = 0;
    while(*columnTitle){
        result += (*columnTitle - 'A' + 1) *  pow(26,tag);
        tag++;
        columnTitle++;
    } 
    return result;
}
```



## 76、存在重复元素II(LC 219)

给定一个整数数组和一个整数 k，判断数组中是否存在两个不同的索引 i 和 j，使得 nums [i] = nums [j]，并且 i 和 j 的差的 绝对值 至多为 k。

 **示例**

```
示例 1:
	输入: nums = [1,2,3,1], k = 3
	输出: true
示例 2:
	输入: nums = [1,0,1,1], k = 1
	输出: true
示例 3:
	输入: nums = [1,2,3,1,2,3], k = 2
	输出: false
```

**代码**

解法一 

超时代码, 复杂度为 $O(kn)$ 受 k 的取值影响

```c
bool containsNearbyDuplicate(int* nums, int numsSize, int k){
    //双指针, 慢指针指向前边, 快指针指向后面
    //出现数据慢指针移动到和快指针相同的位置, 然后快指针根据 k 大小开始滑动,直到找到解
    int slow,fast,i,flag = 0;
    slow = 0;
    fast = 1;
    //边界条件
    while(1){
        //越界判定
        if(fast > numsSize - 1)
            return false;

        int tag = k;
        while(tag){
            //printf("%d %d ",nums[slow],nums[fast]);
            if(nums[slow] == nums[fast]){
                flag = 1;
                break;
            }
                
            fast++;
            tag--;
            //越界判定
            if(fast > numsSize - 1)
                break;
        }
        //printf("\n");
        if(flag == 1)
            return true;
        slow++;
        fast = slow+1;
    }
    return false;
}
```

解法二 

Hash 表, 思路在于通过向Hash 表中存放数据, 当存放两个相同的数据时, 根据映射关系, 他们一定会存放在同一个位置上, 这时就出现了 Hash 冲突。 那么我们就根据这两个值 下标 的差值 < k 与否来判断是否满足题意。

```c
typedef struct hash{
    int key;  // 键
    int index;  // 索引值
    UT_hash_handle hh; // 让结构体哈希柄
} *hash_ptr;

bool containsNearbyDuplicate(int* nums, int numsSize, int k){
    hash_ptr p=NULL, tables=NULL;
    for(int i=0;i<numsSize;i++){
        if(tables) HASH_FIND_INT(tables, &(nums[i]), p);
        if(p&&(i-p->index)<=k) return true;
        p=(hash_ptr)malloc(sizeof(*p));
        p->key=nums[i];
        p->index=i;
        HASH_ADD_INT(tables, key, p);
    }
    return false;
}
```



## 77、回文链表(LC 234)

给你一个单链表的头节点 `head` ，请你判断该链表是否为回文链表。如果是，返回 `true` ；否则，返回 `false` 。

**示例 1：**

![img](img/pal1linked-list.jpg)

```
输入：head = [1,2,2,1]
输出：true
```

**示例 2：**

![img](img/pal2linked-list.jpg)

```
输入：head = [1,2]
输出：false
```

 **代码**

间接数组 对数组进行首尾比较即可

```c
bool isPalindrome(struct ListNode* head){
    struct ListNode* p = head;
    int size = 0;
    //计算链表长度
    while(p){
        p = p->next;
        size++;
    }
    //间接数组
    int * nums = malloc(sizeof(int) * size);
    //存放数据
    int i = 0;
    p = head;
    while(p){
        nums[i++] = p->val;
        p = p->next;
    }
    
    for(i = 0;i < size/ 2;i++){
        if(nums[i] != nums[size - i - 1])
            break;
    }
    return i == size/2 ? true : false;
}
```



## 78、丑数

给你一个整数 n ，请你判断 n 是否为 丑数 。如果是，返回 true ；否则，返回 false 。

丑数 就是只包含质因数 2、3 和/或 5 的正整数。

 **示例**

```
示例 1：
    输入：n = 6
    输出：true
    解释：6 = 2 × 3
示例 2：
    输入：n = 8
    输出：true
    解释：8 = 2 × 2 × 2
示例 3：
    输入：n = 14
    输出：false
    解释：14 不是丑数，因为它包含了另外一个质因数 7 。
示例 4：
    输入：n = 1
    输出：true
    解释：1 通常被视为丑数。
```

**代码**

对质因数进行遍历, 判断数能否仅通过 2/3/5 的多次组合而构成

```c
bool isUgly(int n) {
    if (n <= 0) {
        return false;
    }
    int factors[] = {2, 3, 5};
    for (int i = 0; i < 3; i++) {
        while (n % factors[i] == 0) {
            n /= factors[i];
        }
    }
    return n == 1;
}
```



## 79、单词规律(LC 290)

给定一种规律 pattern 和一个字符串 str ，判断 str 是否遵循相同的规律。

这里的 遵循 指完全匹配，例如， pattern 里的每个字母和字符串 str 中的每个非空单词之间存在着双向连接的对应规律。

**示例**

```
示例1:
    输入: pattern = "abba", str = "dog cat cat dog"
    输出: true
示例 2:
    输入:pattern = "abba", str = "dog cat cat fish"
    输出: false
示例 3:
    输入: pattern = "aaaa", str = "dog cat cat dog"
    输出: false
示例 4:
    输入: pattern = "abba", str = "dog dog dog dog"
    输出: false
```

**代码**

```c
int* preProcess(char *s, int *len)
{
    int size = 1;
    int i;
    for(i = 0; s[i]; i++)
        if(s[i] == ' ')
            size++;
    int *nums = (int *)malloc(sizeof(int)*(size));
    size = 0;
    nums[size++] = 0;
    for(i = 0; s[i]; i++)
        if(s[i] == ' ')
        {
            s[i] = '\0';
            nums[size++] = i+1;
        }
    *len = size;
    return nums;
}

bool wordPattern(char * pattern, char * s)
{
    int size;
    int *index = preProcess(s, &size);
    int len = strlen(pattern);
    if( len != size)
        return false;
    for(int i = 0 ; i < len; i++)
        for(int j = i + 1; j < len; j++)
        {
            int re = strcmp(&s[index[i]], &s[index[j]]);
            if((pattern[i] == pattern[j] && re != 0) || 
                (pattern[i] != pattern[j] && re == 0)
            )
                return false;
        }
    free(index);
    return true;
}
```



## 80、唯一摩斯密码相同(LC 804)

国际摩尔斯密码定义一种标准编码方式，将每个字母对应于一个由一系列点和短线组成的字符串， 比如:

'a' 对应 ".-" ，
'b' 对应 "-..." ，
'c' 对应 "-.-." ，以此类推。
为了方便，所有 26 个英文字母的摩尔斯密码表如下：

[".-","-...","-.-.","-..",".","..-.","--.","....","..",".---","-.-",".-..","--","-.","---",".--.","--.-",".-.","...","-","..-","...-",".--","-..-","-.--","--.."]
给你一个字符串数组 words ，每个单词可以写成每个字母对应摩尔斯密码的组合。

例如，"cab" 可以写成 "-.-..--..." ，(即 "-.-." + ".-" + "-..." 字符串的结合)。我们将这样一个连接过程称作 单词翻译 。
对 words 中所有单词进行单词翻译，返回不同 单词翻译 的数量。

 **示例**

```
示例 1：
    输入: words = ["gin", "zen", "gig", "msg"]
    输出: 2
    解释: 
    各单词翻译如下:
    "gin" -> "--...-."
    "zen" -> "--...-."
    "gig" -> "--...--."
    "msg" -> "--...--."
    共有 2 种不同翻译, "--...-." 和 "--...--.".
示例 2：
    输入：words = ["a"]
    输出：1
```

**代码**

迭代 根据字符判定分属于哪一个摩斯密码再进行合并, 最终得到转换后的字符集, 再在字符集内遍历去重即为结果。

```c
int uniqueMorseRepresentations(char ** words, int wordsSize){
    char str[26][8] = {".-","-...","-.-.","-..",".","..-.","--.","....","..",".---","-.-",".-..","--","-.","---",".--.","--.-",".-.","...","-","..-","...-",".--","-..-","-.--","--.."};
    int i = 0,j = 0;
    char result[wordsSize][100];
    for(i = 0;i < wordsSize;i++){
        char temp[100] = "";
        for(j = 0;j < strlen(words[i]);j++){
            strcat(temp,str[words[i][j] - 'a']);
        }
        strcpy(result[i],temp);
    }

    int count = 0;  //重复的个数
    for(i = 0;i < wordsSize;i++){
        //printf("%s\n",result[i]);
        for(j = i+1;j < wordsSize;j++){
            if(!strcmp(result[j],"-1"))
                continue;
            if(!strcmp(result[i],result[j])){
                count++; 
                strcpy(result[j],"-1");     //设置该字符为已比较完毕标志,后续不再比较
            }       
        }
    }
    return wordsSize == 1 ? 1 : wordsSize - count;
}
```



## 81、翻转图像(LC 832)

给定一个二进制矩阵 A，我们想先水平翻转图像，然后反转图像并返回结果。

水平翻转图片就是将图片的每一行都进行翻转，即逆序。例如，水平翻转 [1, 1, 0] 的结果是 [0, 1, 1]。

反转图片的意思是图片中的 0 全部被 1 替换， 1 全部被 0 替换。例如，反转 [0, 1, 1] 的结果是 [1, 0, 0]。

 ```
 示例 1：
     输入：[[1,1,0],[1,0,1],[0,0,0]]
     输出：[[1,0,0],[0,1,0],[1,1,1]]
     解释：首先翻转每一行: [[0,1,1],[1,0,1],[0,0,0]]；
          然后反转图片: [[1,0,0],[0,1,0],[1,1,1]]
 示例 2：
     输入：[[1,1,0,0],[1,0,0,1],[0,1,1,1],[1,0,1,0]]
     输出：[[1,1,0,0],[0,1,1,0],[0,0,0,1],[1,0,1,0]]
     解释：首先翻转每一行: [[0,0,1,1],[1,0,0,1],[1,1,1,0],[0,1,0,1]]；
          然后反转图片: [[1,1,0,0],[0,1,1,0],[0,0,0,1],[1,0,1,0]]
 ```

**代码**

暴力法 直接进行翻转和反转即可

```
/*
 * 输入: 数组 长度
 * 输出: 翻转后的数组
*/
int * reverseInt(int * nums,int size){
    int i,j;
    for(i = 0;i < size/2;i++){
        int temp = nums[i];
        nums[i] = nums[size-i-1];
        nums[size-i-1] = temp;
    }
    return nums;
}

int** flipAndInvertImage(int** image, int imageSize, int* imageColSize, int* returnSize, int** returnColumnSizes){
    *returnSize = imageSize;
	*returnColumnSizes = imageColSize;
    //首选进行水平翻转
    int i,j;
    for(i = 0;i < imageSize;i++)
        reverseInt(image[i],imageColSize[i]);

    //然后进行反转图片
    for(i = 0;i < imageSize;i++){
        for(j = 0;j < imageColSize[i];j++)
            image[i][j] = image[i][j] == 1 ? 0 : 1;
    }
    return image;
}
```



## 82、山脉数组的峰顶索引(LC 852)

符合下列属性的数组 arr 称为 山脉数组 ：
arr.length >= 3
存在 i（0 < i < arr.length - 1）使得：
arr[0] < arr[1] < ... arr[i-1] < arr[i]
arr[i] > arr[i+1] > ... > arr[arr.length - 1]
给你由整数组成的山脉数组 arr ，返回任何满足 arr[0] < arr[1] < ... arr[i - 1] < arr[i] > arr[i + 1] > ... > arr[arr.length - 1] 的下标 i 。

 **示例**

```
示例 1：
    输入：arr = [0,1,0]
    输出：1
示例 2：
    输入：arr = [0,2,1,0]
    输出：1
示例 3：
    输入：arr = [0,10,5,2]
    输出：1
示例 4：
	输入：arr = [3,4,5,1]
    输出：2
示例 5：
	输入：arr = [24,69,100,99,79,78,67,36,26,19]
	输出：2
```

**代码**

暴力法

```c
int peakIndexInMountainArray(int* arr, int arrSize){
    //暴力查找 - 实质上就是查找山顶 最大值下标
    int i,j,max = 0,index = 0;
    for(i = 0;i <arrSize;i++){
        if(max < arr[i]){
            max = arr[i];
            index = i;
        }
    }
    return index;
}
```



## 83、转置矩阵(LC 867)

给你一个二维整数数组 `matrix`， 返回 `matrix` 的 **转置矩阵** 。

矩阵的 **转置** 是指将矩阵的主对角线翻转，交换矩阵的行索引与列索引。

![img](img/hint_transpose.png)

**示例**

```
示例 1：
	输入：matrix = [[1,2,3],[4,5,6],[7,8,9]]
	输出：[[1,4,7],[2,5,8],[3,6,9]]
示例 2：
	输入：matrix = [[1,2,3],[4,5,6]]
	输出：[[1,4],[2,5],[3,6]]
```

**代码**

间接数组 , 不同尺度赋值

```c
int** transpose(int** matrix, int matrixSize, int* matrixColSize, int* returnSize, int** returnColumnSizes){
    //生成 行大小、列大小
    int m = matrixSize;
    int n = matrixColSize[0];
    int i, j;
    //转置后矩阵为n * m 
    int ** nums = (int**)malloc(sizeof(int*) * n);    
    //分配空间  
    *returnColumnSizes = (int*)malloc(sizeof(int) * n); 
    
    for (i = 0; i < n; i++) {
        nums[i] = (int*)malloc(sizeof(int) * m);        //分配空间
        (*returnColumnSizes)[i] = m;        //设置返回的列值
        //转置
        for (j = 0; j < m; j++) 
            nums[i][j] = matrix[j][i];
    }
    *returnSize = n;
    return nums;
}
```



## 84、按奇偶排序数组I (LC 905)

给定一个非负整数数组 A，返回一个数组，在该数组中， A 的所有偶数元素之后跟着所有奇数元素。

你可以返回满足此条件的任何数组作为答案。

**示例**

```
输入：[3,1,2,4]
输出：[2,4,3,1]
输出 [4,2,3,1]，[2,4,1,3] 和 [4,2,1,3] 也会被接受。
```

**代码**

间接数组 偶数放前面,奇数放后面

```c
int* sortArrayByParity(int* A, int ASize, int* returnSize){
    int *ret = malloc(sizeof(int) * ASize);
    *returnSize = ASize;
    int head = 0,tail = ASize -1;

    for(int i = 0; i < ASize;i++){
        if(A[i] & 1){
            ret[tail--] = A[i];
        }else{
            ret[head++] = A[i];
        }
    }

    return ret;
}
```



## 85、最小差值I (LC 908)

给你一个整数数组 nums，请你给数组中的每个元素 nums[i] 都加上一个任意数字 x （-k <= x <= k），从而得到一个新数组 result 。

返回数组 result 的最大值和最小值之间可能存在的最小差值。

 **示例**

```
示例 1：
    输入：nums = [1], k = 0
    输出：0
    解释：result = [1]
示例 2：
    输入：nums = [0,10], k = 2
    输出：6
    解释：result = [2,8]
示例 3：
    输入：nums = [1,3,6], k = 3
    输出：0
    解释：result = [3,3,3] or result = [4,4,4]
```

**代码**

题目理解

```c
int smallestRangeI(int* nums, int numsSize, int k){
    //理解题 考虑 min 和 max 的差值
    // 如果差值 < 2 * k ,也即通过调整 min 和 max 可以使 max = min
    // 同理, min < x < max 也可已通过调整调整为一样的值  也即结果 = 0
    // 当 差值 > 2 * k , 则无法通过调整使 min = max    
    //   结果 = max - k - (min + k) =  max - min - 2k
    int i = 0;
    int max = nums[0],min = nums[0];
    for(i = 0;i < numsSize;i++){
        max = fmax(max,nums[i]);
        min = fmin(min,nums[i]);      
    }
    return (max - min > 2 * k) ? (max - min - 2 * k) : 0;
}
```



## 86、按奇偶排序数组II (LC 922)

给定一个非负整数数组 A， A 中一半整数是奇数，一半整数是偶数。

对数组进行排序，以便当 A[i] 为奇数时，i 也是奇数；当 A[i] 为偶数时， i 也是偶数。

你可以返回任何满足上述条件的数组作为答案。

**示例**

输入：[4,2,5,7]
输出：[4,5,2,7]
解释：[4,7,2,5]，[2,5,4,7]，[2,7,4,5] 也会被接受。

**代码**

思路与 I 相似  , 使用间接数组存放结果。

```c
int* sortArrayByParityII(int* nums, int numsSize, int* returnSize){
    int * result = malloc(sizeof(int) * numsSize);
    * returnSize = numsSize;
    int left = 0,right = numsSize -1;
    int tag1 = 0,tag2 = 1;

    for(int i = 0; i < numsSize;i++){
        //Hash映射思想 存放到数组的i 与 2i 位置
          if(nums[i] & 1){
            result[tag2] = nums[i];
            tag2+=2;
        } else{
            result[tag1] = nums[i];
            tag1+=2;
        }
    }

    return result;
}
```



## 87、三角形的最大周长

给定由一些正数（代表长度）组成的数组 A，返回由其中三个长度组成的、面积不为零的三角形的最大周长。

如果不能形成任何面积不为零的三角形，返回 0。

 **示例**

```
示例 1：
    输入：[2,1,2]
    输出：5
示例 2：
    输入：[1,2,1]
    输出：0
示例 3：
    输入：[3,2,3,4]
    输出：10
示例 4：
    输入：[3,6,2,3]
    输出：8
```

**代码**

排序 根据结果选取集合, 构造

```c
int cmp(const void*a,const void *b){
    return (*(int*)a-*(int*)b);
}
int largestPerimeter(int* nums, int numsSize){
    int i,temp;
    int maxlen = 0;
    qsort(nums,numsSize,sizeof(int),cmp);       //排序
    //如果边数小于3 , 直接返回周长 0 
    if(numsSize<3)
        return 0;
    
    //遍历所有边长集合,取出最大集进行构造
    for(i= 1 ;i < numsSize-1;i++){
        if(nums[i-1]+nums[i]>nums[i+1]){
            temp = nums[i-1]+nums[i]+nums[i+1];
            maxlen = fmax(maxlen,temp);
        }
    }
    return maxlen;
}
```



## 88、十进制整数的反码

每个非负整数 N 都有其二进制表示。例如， 5 可以被表示为二进制 "101"，11 可以用二进制 "1011" 表示，依此类推。注意，除 N = 0 外，任何二进制表示中都不含前导零。

二进制的反码表示是将每个 1 改为 0 且每个 0 变为 1。例如，二进制数 "101" 的二进制反码为 "010"。

给你一个十进制数 N，请你返回其二进制表示的反码所对应的十进制整数。

 **示例**

```
示例 1：
    输入：5
    输出：2
    解释：5 的二进制表示为 "101"，其二进制反码为 "010"，也就是十进制中的 2 。
示例 2：
    输入：7
    输出：0
    解释：7 的二进制表示为 "111"，其二进制反码为 "000"，也就是十进制中的 0 。
示例 3：
    输入：10
    输出：5
    解释：10 的二进制表示为 "1010"，其二进制反码为 "0101"，也就是十进制中的 5 。
```

**代码**

```c
/*
 * 输入: 整数 num 可返回的长度 size
 * 输出: 转换后的二进制的数组  数组长度参数
 * 说明: 该数组返回的数组结果从小端的 从个位开始, 并且正负值转换后都得到的是正值
 * 		如: -1/1 -> 1    -2/2 -> 10   -3/3 -> 11 
*/
int * tenToBinArray(int num,int * size){
    //边界条件 - 0
    if(!num){
        *size = 1;
        int * nums= malloc(sizeof(int) * *size);
        nums[0] = 0;
        return nums;
    }

    //计算长度 - 无关正负, 取绝对值
    int temp = abs(num);
    int len = 0;
    while(temp){
        temp /= 2;
        len++;
    }

    //转换为2进制, 保存到数组
    int * nums= malloc(sizeof(int) * len);
    int tag = 0,i;  //tag用于移动nums数组下标

    temp = abs(num);
    while(temp){
        nums[tag++] = temp % 2;
        temp /= 2;
    }
    *size = len;
    return nums;
}

int bitwiseComplement(int n){
    //十进制转2进制数组
    int size;
    int * binnums = tenToBinArray(n,&size);
    //按位取反 + 二进制转十进制数字
    int i,result=0;
    for(i = 0;i < size;i++){
        binnums[i] = binnums[i] == 1 ? 0 : 1;
        result +=  binnums[i] * pow(2,i);
    }
    return result;
}
```



## 89、删除最外层的括号

有效括号字符串为空 ""、"(" + A + ")" 或 A + B ，其中 A 和 B 都是有效的括号字符串，+ 代表字符串的连接。

例如，""，"()"，"(())()" 和 "(()(()))" 都是有效的括号字符串。
如果有效字符串 s 非空，且不存在将其拆分为 s = A + B 的方法，我们称其为原语（primitive），其中 A 和 B 都是非空有效括号字符串。

给出一个非空有效字符串 s，考虑将其进行原语化分解，使得：s = P_1 + P_2 + ... + P_k，其中 P_i 是有效括号字符串原语。

对 s 进行原语化分解，删除分解中每个原语字符串的最外层括号，返回 s 。

 **示例**

```c
示例 1：
    输入：s = "(()())(())"
    输出："()()()"
    解释：
    输入字符串为 "(()())(())"，原语化分解得到 "(()())" + "(())"，
    删除每个部分中的最外层括号后得到 "()()" + "()" = "()()()"。
示例 2：
    输入：s = "(()())(())(()(()))"
    输出："()()()()(())"
    解释：
    输入字符串为 "(()())(())(()(()))"，原语化分解得到 "(()())" + "(())" + "(()(()))"，
    删除每个部分中的最外层括号后得到 "()()" + "()" + "()(())" = "()()()()(())"。
示例 3：
    输入：s = "()()"
    输出：""
    解释：
    输入字符串为 "()()"，原语化分解得到 "()" + "()"，
    删除每个部分中的最外层括号后得到 "" + "" = ""。
```

**代码**

忽略最外层的括号, 每次从 `count = 1` 开始计数进行赋值

```c
char * removeOuterParentheses(char * s){
    //赋值法 忽略最外层的括号, 取内层括号进行赋值
    int i, count = 0, tag = 0,size = strlen(s);
    for(i = 0; i < size; i++){
        if(s[i] == '('){
            count++;
            if(count>1)
                s[tag++] = '(';
        }
        else{
            count--;
            if(count>0)
                s[tag++] = ')';
        }
    }
    s[tag] = '\0';      // 这行也记得要！
    return s;
}
```



## 90、除数博弈

爱丽丝和鲍勃一起玩游戏，他们轮流行动。爱丽丝先手开局。

最初，黑板上有一个数字 N 。在每个玩家的回合，玩家需要执行以下操作：

选出任一  `x`，满足 `0 < x < N 且 N % x == 0 。`
用 `N - x` 替换黑板上的数字 N 。
如果玩家无法执行这些操作，就会输掉游戏。

只有在爱丽丝在游戏中取得胜利时才返回 `True`，否则返回 `False`。假设两个玩家都以最佳状态参与游戏。

 **示例**

```
示例 1：

输入：2
输出：true
解释：爱丽丝选择 1，鲍勃无法进行操作。
示例 2：

输入：3
输出：false
解释：爱丽丝选择 1，鲍勃也选择 1，然后爱丽丝无法进行操作。
```

**代码**

实质上就是博弈心理, 由于爱丽丝先手, 那么在 n 为偶数情况下, 爱丽丝选 1 即可胜利。 但是偶数时, 无论爱丽丝选几, 最终鲍勃都会选恰当得数而不拜。 也即谁拿到偶数 N 谁就胜利。

```c
bool divisorGame(int n){
    return n % 2 == 0 ? true : false;
}
```



## 91、最后一块石头的重量（LC 1046）

有一堆石头，每块石头的重量都是正整数。

每一回合，从中选出两块 最重的 石头，然后将它们一起粉碎。假设石头的重量分别为 x 和 y，且 x <= y。那么粉碎的可能结果如下：

如果 x == y，那么两块石头都会被完全粉碎；
如果 x != y，那么重量为 x 的石头将会完全粉碎，而重量为 y 的石头新重量为 y-x。
最后，最多只会剩下一块石头。返回此石头的重量。如果没有石头剩下，就返回 0。

**示例**

```
输入：[2,7,4,1,8,1]
输出：1
解释：
先选出 7 和 8，得到 1，所以数组转换为 [2,4,1,1,1]，
再选出 2 和 4，得到 2，所以数组转换为 [2,1,1,1]，
接着是 2 和 1，得到 1，所以数组转换为 [1,1,1]，
最后选出 1 和 1，得到 0，最终数组转换为 [1]，这就是最后剩下那块石头的重量。
```

**代码**
迭代 每次取两个最值进行计算得出结果

```c
int lastStoneWeight(int* stones, int stonesSize){
    //每次选取两个最大数，复杂度为 O（2n）
    int i,max1 = 0,max2 = 0,tag1=0,tag2=0,flag=0;
    while(1){
        for(i = 0;i < stonesSize;i++){
            //循环终止计数
            if(stones[i] != 0)
                flag++;
            if(max1 < stones[i]){
                max1 = stones[i];
                tag1 = i;
            }
        }
        if(flag == 1)
            break;
        else if(flag == 0){
            max1 = 0;
            break;
        }
        stones[tag1] = 0;       //去掉该值，防止比较失败
        for(i = 0;i < stonesSize;i++){
            if(max2 < stones[i]){
                max2 = stones[i];
                tag2 = i;
            }
        }
        //printf("%d %d  %d %d      ",max1,max2,tag1,tag2);
        //只有一个石头时返回最大值即可 max1
        if(max1 == max2){
            stones[tag1] = stones[tag2] = 0;    //粉碎
        } else if(max1 > max2){
            stones[tag2] = 0;
            stones[tag1] = max1 - max2;
        } else if(max1 < max2){
            stones[tag1] = 0;
            stones[tag2] = max2 - max1;
        }
        //重置计数
        tag1 = tag2 = 0;
        max1 = max2 = 0;
        flag = 0;
    }
    return max1;
}
```



## 92、删除字符串中的所有重复项（LC 1047）

给出由小写字母组成的字符串 S，重复项删除操作会选择两个相邻且相同的字母，并删除它们。
在 S 上反复执行重复项删除操作，直到无法继续删除。
在完成所有重复项删除操作后返回最终的字符串。答案保证唯一。

**示例**

```
输入："abbaca"
输出："ca"
解释：
例如，在 "abbaca" 中，我们可以删除 "bb" 由于两字母相邻且相同，这是此时唯一可以执行删除操作的重复项。之后我们得到字符串 "aaca"，其中又只有 "aa" 可以执行重复项删除操作，所以最后的字符串为 "ca"。
```

**代码**

```c
char* removeDuplicates(char* s) {
    int length = strlen(s);  //获取字符串长度
    char * result = malloc(sizeof(char) * (length + 1));    //结果字符串
    int retSize = 0;    //结果字符串大小
    //取两个字符串相比较， 如果出现相同的指针就-1回溯再与另一串的后续比较，当串为空
    //就进行赋值
    //相当于栈  a 入 b 入（b与b相等） b 出 （a与a相等）a出 c入 a 入
    //结果为 ca  栈的思想
    for (int i = 0; i < length; i++) {
        //当结果字符串大小》0并且结果字符串前一个位置 == s【i】
        if (retSize > 0 && result[retSize - 1] == s[i]) {
            retSize--;
        } else {
            result[retSize++] = s[i];
        }
    }
    result[retSize] = '\0';
    return result;
}
```



## 93、高度检查器（LC 1051）

学校打算为全体学生拍一张年度纪念照。根据要求，学生需要按照 非递减 的高度顺序排成一行。

排序后的高度情况用整数数组 expected 表示，其中 expected[i] 是预计排在这一行中第 i 位的学生的高度（下标从 0 开始）。

给你一个整数数组 heights ，表示 当前学生站位 的高度情况。heights[i] 是这一行中第 i 位学生的高度（下标从 0 开始）。
返回满足 heights[i] != expected[i] 的 下标数量 。

**示例**

```
输入：heights = [1,1,4,2,1,3]
输出：3 
解释：
高度：[1,1,4,2,1,3]
预期：[1,1,1,2,3,4]
下标 2 、4 、5 处的学生高度不匹配。
示例 2：
输入：heights = [5,1,2,3,4]
输出：5
解释：
高度：[5,1,2,3,4]
预期：[1,2,3,4,5]
所有下标的对应学生高度都不匹配。
示例 3：
输入：heights = [1,2,3,4,5]
输出：0
解释：
高度：[1,2,3,4,5]
预期：[1,2,3,4,5]
所有下标的对应学生高度都匹配。
```

**代码**

```c
排序比较 实际上就是递增排序后比较与排序结果不同的项数目
int cmp(const void *a,const void *b){
    return *(int*)a-*(int*)b;
}

int heightChecker(int* heights, int heightsSize){
    //实际上就是递增排序后比较与排序结果不同的项数目
    int * nums = malloc(sizeof(int) * heightsSize);
    //赋值
    int i,count=0;
    for(i = 0;i < heightsSize;i++)
        nums[i] = heights[i];
    qsort(nums,heightsSize,sizeof(int),cmp);
    for(i = 0;i < heightsSize;i++)
        if(nums[i] != heights[i])
            count++;
    return count;
}
```

