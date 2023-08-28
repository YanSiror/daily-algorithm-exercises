## 1 算法思维类型

### 动态规划

**步骤**

- 定义子问题
- 写出子问题的递推关系
- 确定DP数组的计算顺序
- 空间优化



**例子**

[LC 198: 打家劫舍](https://leetcode.cn/problems/house-robber/solutions/138131/dong-tai-gui-hua-jie-ti-si-bu-zou-xiang-jie-cjavap/?envType=study-plan-v2&envId=leetcode-75)

 

### 双指针

#### 1) 对撞指针

> 对撞指针是指在 `有序数组` 中，将指向最左侧的索引定义为左指针(left)，最右侧的定义为右指针(right)，然后从两头向中间进行数组遍历。对撞数组适用于有序数组，也就是说当你遇到题目给定有序数组时，应该第一时间想到用对撞指针解题。

**思想**

`来源于二分查找`

```java
int binarySearch(int[] nums, int target) {
    int left = 0; 
    int right = nums.length - 1;
    while(left <= right) {
        int mid = left + (right - left) / 2;
        if(nums[mid] == target)
            return mid; 
        else if (nums[mid] < target)
            left = mid + 1; 
        else if (nums[mid] > target)
            right = mid - 1;
    }
    return -1;
}
```

**模板**

```java
public void clashPointer(int[] array) {
    int left = 0;
    int right = array.length-1;
    while(left <= right){
        if(array[left] + array[right] == target){
            //操作
        } else if(array[left] + array[right] < target){
            left++;
        } else if(array[left] + array[right] > target){
            right--;
        }
    }
}
```

**例题**

`给定有序数组 nums, 求符合 nums[i] + nums[j] = target 的下标 i, j 值 `

```java
public int[] twoSum(int[] nums, int target) {
    int left = 0;
    int right = nums.length-1;
    Arrays.sort(nums);  //排序
    while(left <= right){
        if(nums[left] + nums[right] == target){
            return new int[] {left, right};
        } else if(nums[left] + nums[right] < target){
            left++;
        } else if(nums[left] + nums[right] > target){
            right--;
        }
    }
    return new int[] {0, 1};
}
```



#### 2) 快慢指针

> 快慢指针也是双指针，但是两个指针从同一侧开始遍历数组，将这两个指针分别定义为快指针（fast）和慢指针（slow），两个指针以不同的策略移动，直到两个指针的值相等（或其他特殊条件）为止，如fast每次增长两个，slow每次增长一个。

**模板**

`判断环是经典问题`

```java
public boolean fsPointer(ListNode head) {
    ListNode slow, fast;
    slow = fast = head;
    while(slow != null && slow.next != null){
        slow = slow.next;
        fast = fast.next.next;
        if(slow == fast){
            return true;
        }
    }
    return false;
}
```

**例题**

`LC 141: 给定一个链表, 判断是否是环形链表`

```java
public boolean hasCycle(ListNode head) {
    ListNode slow, fast;
    slow = fast = head;
    while(fast != null && fast.next != null){
        slow = slow.next;
        fast = fast.next.next;
        if(slow == fast){
            return true;
        }
    }
    return false;
}
```





### 贪心

> 贪心是一种**算法思想**， 在某些问题中，当前状态对后续状态没有影响（也叫做问题**无后效性**），这样一来，当前状态的最优解最终会造成全局的最优解，此时我们每一步（每个状态）都选取当前最优解（而不考虑之后的情况），这就是贪心。
>
> **实质上就是取当前的最优解, 不考虑以后**
>
> - 贪心算法与动态规划的区别:
>
> ​	动态规划顾名思义会“动态”地求解问题，会将之前的结果记录下来从而找到最优解，而贪心是一直往前，会对每一个方案都做出选择



**例题**

`LC122: 买卖股票的最佳时机 II `

给你一个整数数组 `prices` ，其中 `prices[i]` 表示某支股票第 `i` 天的价格。

在每一天，你可以决定是否购买和/或出售股票。你在任何时候 **最多** 只能持有 **一股** 股票。你也可以先购买，然后在 **同一天** 出售。

返回 *你能获得的 **最大** 利润* 。

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

`实质上就是只加了利润为正的情况, 其他情况不再计算, 只要有利润就卖。`

```java
public int maxProfit(int[] prices) {
    if(prices.length == 1){
        return 0;
    }
    int max = 0;
    for(int i = 0; i < prices.length - 1; i++){
        if(prices[i] < prices[i+1]){
            max += prices[i+1] - prices[i];
        }
    }
    return max;
}
```





## 2 数据结构

### 数组

#### 排序 | 赋值 | 切割

```java
Arrays.sort(nums);		//排序
Arrays.fill(arr, 0);  	//赋值
Arrays.copyOfRange(nums, stratIndex, endIndex);	//切割
```



#### 比较

```java
Math.max(a,b);
//比较两个数组对应值是否相等
List<Integer> arr1 = new ArrayList<Integer>();
List<Integer> arr2 = new ArrayList<Integer>();
//true or false
arr1.equals(arr2);	
```



### 字符串

```java
String s = "hello";
t.charAt(i);					//获取第i个字符
//
char[] chars = s.toCharArray();		//转换为 char 数组
String b = new String(chars);		//转换为 String 字符串
```



### 优先队列

> PriorityQueue 是 Java 中的一个优先队列实现类，它可以用于实现基于优先级的队列，即队列中的元素会按照优先级被排序，优先级高的元素先出队列。
>
> PriorityQueue 中的元素必须实现 Comparable 接口，或者在创建 PriorityQueue 对象时传入一个 Comparator 对象以指定元素的比较方式。使用 PriorityQueue 可以实现以下常用功能：
>
> 1. 添加元素：使用 `add()` 或 `offer()` 函数向队列中添加元素，添加的元素会根据其优先级被放置在队列中的合适位置。
> 2. 获取队首元素：使用 `peek()` 函数获取队列中优先级最高的元素，但不会将其从队列中移除。
> 3. 获取并移除队首元素：使用 `poll()` 函数获取队列中优先级最高的元素，并将其从队列中移除。
> 4. 判断队列是否为空：使用 `isEmpty()` 函数判断队列是否为空。
>
> 以下是 PriorityQueue 类中常用的一些函数：
>
> 1. `add(E element)`：将元素添加到队列中，如果队列已满则会抛出异常。
> 2. `offer(E element)`：将元素添加到队列中，如果队列已满则会返回 false。
> 3. `peek()`：获取队列中优先级最高的元素，但不会将其从队列中移除。
> 4. `poll()`：获取队列中优先级最高的元素，并将其从队列中移除。
> 5. `remove(Object o)`：从队列中移除指定的元素，如果队列中不存在该元素则会返回 false。
> 6. `size()`：返回队列中元素的数量。
> 7. `isEmpty()`：判断队列是否为空。
> 8. `clear()`：清空队列中的所有元素。





### 哈希表

#### 遍历

- **Entry**

  ```java
  HashMap<Integer, Integer> map = new HashMap<Integer, Integer>();
  Iterator<Map.Entry<Integer, Integer>> it = map.entrySet().iterator();
  while (it.hasNext()) {
      Map.Entry<Integer, Integer> entry = it.next();
      System.out.println(entry.getKey());
      System.out.println(entry.getValue());
  }
  ```

- **EntrySet**

  ```java
  //Hash 表
  HashMap<Integer, Integer> map = new HashMap<Integer, Integer>();
  for(Map.Entry<Integer, Integer> entry : map.entrySet()){
      System.out.println(entry.getKey());
      System.out.println(entry.getValue());
  }
  ```

- **KeySet**

  ```java
  //Hash 表
  HashMap<Integer, Integer> map = new HashMap<Integer, Integer>();
  for(Integer key: map.keySet()){
      System.out.println(key);
      System.out.println(map.get(key));
  }
  ```



#### 取值或设为默认 | 取第一个元素

```java
map.getOrDefault('key', 0)		//存在key则返回值, 不存在key则设为0
map.entrySet().iterator().next();	//返回第1个元素
```



### 队列

Java 的 ArrayQueue 类（也称为数组队列）实现了 Queue 接口，提供了以下方法：

```java
add(E e)：在队列的尾部添加指定元素，如果队列已满则抛出 IllegalStateException 异常。
offer(E e)：在队列的尾部添加指定元素，如果队列已满则返回 false。
remove()：移除并返回队列头部的元素，如果队列为空则抛出 NoSuchElementException 异常。
poll()：移除并返回队列头部的元素，如果队列为空则返回 null。
element()：返回队列头部的元素，但不会移除该元素，如果队列为空则抛出 NoSuchElementException 异常。
peek()：返回队列头部的元素，但不会移除该元素，如果队列为空则返回 null。
size()：返回队列中元素的数量。
isEmpty()：检查队列是否为空。
contains(Object o)：检查队列中是否包含指定元素。
toArray()：将队列中的元素以数组形式返回。
clear()：移除队列中的所有元素。
```



### 栈

```java
push() - 添加元素到栈顶
pop() - 删除栈顶元素
peek() - 查看栈顶元素
size() - 查看栈的大小
empty() - 检查栈是否为空
search() - 查找栈中一个元素
```



### 树

#### 二叉树的前 | 中 | 后 | 层序遍历

`前序`

$递归$

```java
public void preOrder(TreeNode head){
    if(head == null){
        return;
    }
    System.out.println(head.val);
    preOrder(head.left);
    preOrder(head.right);
}
```

$迭代$

```java
 public int[] preOrder(TreeNode root){
        List<Integer> res = new ArrayList<>();
        if(root == null){
            return res.stream().mapToInt(Integer::valueOf).toArray();
        }

        Deque<TreeNode> stack = new LinkedList<TreeNode>();
        while(root != null || !stack.isEmpty()){
            //先一条路走到头, 然后退栈
            while(root != null){
                stack.push(root);
                res.add(root.val);     //添加值到lsit
                root = root.left;
            }
            //到头了, 退栈
            root = stack.pop();
            root = root.right;      //向右遍历
        }
        int[] ress = res.stream().mapToInt(Integer::valueOf).toArray();
        return ress;
    }
```



`中序`

$递归$

```java
public void midOrder(TreeNode head){
    if(head == null){
        return;
    }
    midOrder(head.left);
    System.out.println(head.val);
    midOrder(head.right);
}
```

$迭代$

```java
public int[] midOrder(TreeNode root){
    Deque<TreeNode> stack = new LinkedList<TreeNode>();
    List<Integer> res = new ArrayList<>();
    while(root != null || !stack.isEmpty()){
        //先一条路走到头, 然后退栈
        while(root != null){
            stack.push(root);
            root = root.left;
        }
        //到头了, 退栈
        root = stack.pop();
        res.add(root.val);     //添加值到lsit
        root = root.right;      //向右遍历
    }
    int[] ress = res.stream().mapToInt(Integer::valueOf).toArray();
    return ress;
}
```



`后序`

$递归$

```java
public void afterOrder(TreeNode head){
    if(head == null){
        return;
    }
    afterOrder(head.left);
    afterOrder(head.right);
    System.out.println(head.val);
}
```

$迭代$

```java
public int[] afterOrder(TreeNode root){
    List<Integer> res = new ArrayList<>();
    if(root == null){
        return res.stream().mapToInt(Integer::valueOf).toArray();
    }

    Deque<TreeNode> stack = new LinkedList<TreeNode>();
    TreeNode pre = null;
    while(root != null || !stack.isEmpty()){
        //先一条路走到头, 然后退栈
        while(root != null){
            stack.push(root);
            root = root.left;
        }

        root = stack.pop();
        //根据情况判断是否有右结点 && 未被访问过
        if(root.right == null || root.right == pre){
            res.add(root.val);
            pre = root;
            root = null;

        } else{
            stack.push(root);
            root = root.right;
        }
    }
    return res.stream().mapToInt(Integer::valueOf).toArray();
}
```



`层序`

通过 BFS 改造而来, 记录每次入队的个数然后添加到二维数组的对应列 : 主要是通过BFS得到每一层的结点信息, 然后将节点信息存到新的数组, 再拼接为二维数组即可。

```java
 public List<List<Integer>> levelOrder(TreeNode root) {
     List<List<Integer>> res = new ArrayList<List<Integer>>();
     Queue<TreeNode> queue = new ArrayDeque<>();
     if(root != null){
         queue.add(root);
     }
     while(!queue.isEmpty()){
         List<Integer> level = new ArrayList<>();
         int n = queue.size();
         for(int i = 0; i < n; i++){
             //遍历每一层的所有节点, 添加到列表内 - 以下是层序遍历
             TreeNode node = queue.poll();
             if(node.left != null){
                 queue.add(node.left);
             }
             if(node.right != null){
                 queue.add(node.right);
             }
             level.add(node.val);
         }
         res.add(level);
     }
     return res;
 }
```





#### 二叉树深度优先遍历(DFS) | 广度优先遍历(BFS)

`DFS`

```java
public void DFS(TreeNode head){
    if(head == null){
        return;
    }
    //list.add(node.val)
    DFS(head.left);
    DFS(head.right);
}
```

`BFS`

```java
public List<Integer> BFS(TreeNode root){
    Queue<TreeNode> queue = new LinkedList<TreeNode>();
    List<Integer> list= new LinkedList<Integer>();

    if(root == null){
        return res;
    }
    queue.add(root);
    while(!queue.isEmpty()){
        TreeNode node = queue.poll();
        if(node.left != null){
            queue.add(node.left);
        }
        if(node.right != null){
            queue.add(node.right);
        }
        list.add(node.val);
        System.out.println(node.val);
    }
    return list;
}
```





### 图





## 3 常见算法

### Lambda 表达式

```java
Arrays.stream(flowerbed).forEach(num ->{
     System.out.print(num + " ");
});
>>>         
Arrays.stream(flowerbed).forEach(System.out::println);
```



### 位运算

```java
i & 1    //检测 i 的最低位是多少(0 或 1), 可以用于对2取模
i | 1    //将 i 的最低位强行设为 1
i >> 1   //右移一位,相当于除以 2
i << 1   //左移一位,相当于乘以 2
```



### 手撕算法

#### 1) 有效括号

```java
public boolean isValid(String s) {
    int n = s.length();
    if(n % 2 == 1){
        return false;
    }

    //定义 MAP 保存 Key - Value
    Map<Character, Character> map = new HashMap<Character, Character>() {{
        put(')', '(');
        put(']', '[');
        put('}', '{');
    }};
    //初始化栈
    Deque<Character> stack = new LinkedList<Character>();
    for(int i = 0; i < n; i++){
        char c = s.charAt(i);
        if(map.containsKey(c)){
            //如果后置括号出现: 1) 栈空, 匹配失败 2) 不等于map中匹配的括号, 匹配失败
            if(stack.isEmpty() || stack.peek() != map.get(c)){
                return false;
            }
            stack.pop();
        } else{
            stack.push(c);
        }
    }
    return stack.isEmpty();
}
```



#### 2) LRU

> 最近最久未用(Least Recently Used)算法: 也就是检查最近最少使用的数据的算法。这个算法通常使用在内存淘汰策略中，用于将不常用的数据转移出内存，将空间腾给最近更常用的“热点数据”。

```java
class LRUCache {
    int capacity;
    Map<Integer, Integer> map;

    public LRUCache(int capacity) {
        this.capacity = capacity;
        this.map = new LinkedHashMap<Integer, Integer>();
    }

    public int get(int key) {
        if(!map.containsKey(key)){
            return -1;
        }
        //先删除旧位置, 再放入新位置
        Integer value = map.remove(key);
        map.put(key, value);
        return value;
    }

    public void put(int key, int value) {
        if(map.containsKey(key)){
            map.remove(key);
            map.put(key, value);
            return;
        }
        map.put(key, value);
        //如果 size() 超出 capacity, 删除最近最久未用的元素, 也即删除最前面的一个元素
        if(map.size() >capacity){
            Integer tempKey = map.entrySet().iterator().next().getKey();
            map.remove(tempKey);
        }
    }
}
```



#### 3)











## 数据库

### 判断空值

**例**

```cmd
+------+------+-----------+
| id   | name | referee_id|
+------+------+-----------+
|    1 | Will |      NULL |
|    2 | Jane |      NULL |
|    3 | Alex |         2 |
|    4 | Bill |      NULL |
|    5 | Zack |         1 |
|    6 | Mark |         2 |
+------+------+-----------+
```



```sql
select name
from customer
where referee_id != 2 or referee_id is null;
```



### 连接

> 数据库中的链接（join）用于将两个或多个表格中的数据进行连接操作，以便进行更复杂的查询和分析。在链接操作中，有三种常见的链接类型：左链接、右链接和内链接。
>
> 1. 左链接（Left Join）：左链接操作返回左表格中的所有记录和右表格中符合条件的记录。如果右表格中没有符合条件的记录，则该记录的右侧列将显示NULL值。左链接 `以左表格为基础` ，右表格中的数据是可选的，左表格中的所有数据都会被返回。
> 2. 右链接（Right Join）：右链接操作返回右表格中的所有记录和左表格中符合条件的记录。如果左表格中没有符合条件的记录，则该记录的左侧列将显示NULL值。右链接 `以右表格为基础` ，左表格中的数据是可选的，右表格中的所有数据都会被返回。
> 3. 内链接（Inner Join）：内链接操作返回两个表格中符合条件的记录。在内链接中，只有在两个表格中都存在符合条件的记录时才会返回结果。
>
> 总的来说，左链接和右链接是外链接的一种，内链接是一种常见的内部链接。左链接和右链接可以帮助我们查找数据表中存在但在另一个表格中不存在的数据，而内链接则用于查找两个表格中共同存在的数据。

#### JOIN

> join 会过滤掉无法匹配的行,也就是说只返回能够匹配上的行。



#### 左链接

**例**

```
输入：
Employees 表:
+----+----------+
| id | name     |
+----+----------+
| 1  | Alice    |
| 7  | Bob      |
| 11 | Meir     |
| 90 | Winston  |
| 3  | Jonathan |
+----+----------+
EmployeeUNI 表:
+----+-----------+
| id | unique_id |
+----+-----------+
| 3  | 1         |
| 11 | 2         |
| 90 | 3         |
+----+-----------+
```

**代码**

```sql
select unique_id, name
from Employees e left join EmployeeUNI ei
on e.id = ei.id;
```

**结果**

```sql
+-----------+----------+
| unique_id | name     |
+-----------+----------+
| null      | Alice    |
| null      | Bob      |
| 2         | Meir     |
| 3         | Winston  |
| 1         | Jonathan |
+-----------+----------+
```





#### 右链接

**例**

```
输入：
Employees 表:
+----+----------+
| id | name     |
+----+----------+
| 1  | Alice    |
| 7  | Bob      |
| 11 | Meir     |
| 90 | Winston  |
| 3  | Jonathan |
+----+----------+
EmployeeUNI 表:
+----+-----------+
| id | unique_id |
+----+-----------+
| 3  | 1         |
| 11 | 2         |
| 90 | 3         |
+----+-----------+
```

**代码**

```sql
select unique_id, name
from Employees e right join EmployeeUNI ei
on e.id = ei.id;
```

**结果**

```sql
| unique_id | name     |
| --------- | -------- |
| 1         | Jonathan |
| 2         | Meir     |
| 3         | Winston  |
```



#### 内连接

**例**

```
输入：
Employees 表:
+----+----------+
| id | name     |
+----+----------+
| 1  | Alice    |
| 7  | Bob      |
| 11 | Meir     |
| 90 | Winston  |
| 3  | Jonathan |
+----+----------+
EmployeeUNI 表:
+----+-----------+
| id | unique_id |
+----+-----------+
| 3  | 1         |
| 11 | 2         |
| 90 | 3         |
+----+-----------+
```

**代码**

```sql
select unique_id, name
from Employees e inner join EmployeeUNI ei
on e.id = ei.id;
```

**结果**

```sql
| unique_id | name     |
| --------- | -------- |
| 2         | Meir     |
| 3         | Winston  |
| 1         | Jonathan |
```



### 函数

#### Round

ROUND 是一个函数，用于将一个数值四舍五入到指定的小数位数。在使用 ROUND 函数时，需要指定要进行舍入的数值和要舍入到的小数位数。

```sql
round(sum(price*units)/sum(units), 2)		//保留2位小数
```



#### SUM

在 SQL 中，SUM 是一个聚合函数，用于计算指定列的总和。在使用 SUM 函数时，需要指定要进行计算的列。

```sql
sum(price)		//计算价格总和
```



#### AVG

计算平均值

```sql
select round(avg(b.timestamp -a.timestamp), 3) as processing_time 
from activity a , activity b
where a.machine_id = b.machine_id;
```





#### DATEDIFF

DATEDIFF() 函数返回两个日期之间的天数。

```
DATEDIFF(date1,date2)
```

*date1* 和 *date2* 参数是合法的日期或日期/时间表达式。

**注释：**只有值的日期部分参与计算。

**实例**

**例子 1**

使用如下 SELECT 语句：

```
SELECT DATEDIFF('2008-12-30','2008-12-29') AS DiffDate
```

结果：

| DiffDate |
| :------- |
| 1        |

**例子 2**

使用如下 SELECT 语句：

```
SELECT DATEDIFF('2008-12-29','2008-12-30') AS DiffDate
```

结果：

| DiffDate |
| :------- |
| -1       |



#### DATE_ADD

`DATE_ADD()` 是 MySQL 中的一个日期函数，用于在指定日期上添加一定的时间间隔，返回一个新的日期值

**语法**

```sql
DATE_ADD(date, INTERVAL expr unit)
```

其中，`date` 是指要添加时间间隔的日期；`expr` 是要添加的时间间隔数；`unit` 是时间间隔的单位，可以是 `MICROSECOND`，`SECOND`，`MINUTE`，`HOUR`，`DAY`，`WEEK`，`MONTH`，`QUARTER`，`YEAR` 或它们的缩写形式。

例如，在一个名为 `orders` 的表中，`order_date` 字段包含订单的日期，需要将订单日期加上两个月，可以使用以下语句：

```sql
SELECT DATE_ADD(order_date, INTERVAL 2 MONTH) AS new_order_date FROM orders;
```

这将返回一个包含新的订单日期的结果集，其中每个订单日期都比原来的日期晚两个月。

注意，`DATE_ADD()` 还可以与 `NOW()` 函数一起使用，以便在当前日期上添加时间间隔。例如：

```SQL
SELECT DATE_ADD(NOW(), INTERVAL 1 DAY) AS tomorrow;
```

这将返回一个包含明天日期的结果集。



#### LEFT

`取前 N 个字符:  LEFT(STR, 7)`

使用 left() 函数取 trans_date 列的前7个字符,也即取月份。

```sql
left(trans_date, 7)
```



#### RIGHT

`RIGHT()` 是一种 SQL 函数，可用于从字符串中提取指定数量的字符，从字符串的右侧开始。

**语法**

```sql
RIGHT(string, length)
```

例如，假设有一个名为 `employees` 的表，其中包含 `first_name` 和 `last_name` 两个列，需要将每个员工的姓名缩写为首字母加上姓氏后两个字符，可以使用以下 SQL 查询语句：

```
SELECT CONCAT(LEFT(first_name, 1), RIGHT(last_name, 2)) AS initials
FROM employees;
```

这将返回一个包含每个员工姓名缩写的结果集。在上面的查询中，`RIGHT(last_name, 2)` 函数将从 `last_name` 列的右侧提取两个字符，并将这两个字符与 `first_name` 列的第一个字符拼接在一起，形成员工姓名缩写。

请注意，`RIGHT()` 函数在从字符串的右侧提取字符时非常有用，但在某些情况下，可能需要使用 LEFT() 函数来从字符串的左侧提取字符。



#### COUNT

`用于计算数目`

**语法**

- Simple

  计算 item 出现的次数

  ```sql
  COUNT(item)
  ```

- Hard

  如果 `state='approved'` 成立则赋值为1, 否则赋值为 NULL

  ```sql
  COUNT(IF(state='approved',1,NULL))
  ```

  

#### length

判断字符串的长度

```sql
length(str)
```



#### GROUP_CONCAT









### 语法

#### ORDER BY

> 升序: asc
>
> 降序: desc
>
> 多组排序: 按书写的前后为优先级一次进行排序

```sql
order by percentage desc, r.contest_id asc; 	//返回的结果表按 percentage 的 降序 排序，若相同则按 contest_id 的 升序 排序。
```





#### GROUP BY

GROUP BY 子句用于按照指定的列对查询结果进行分组。在 GROUP BY 子句中，指定的列将成为分组的依据，查询结果将根据这些列的不同组合而被分为不同的组。

**例**

以下 SQL 查询用于计算 `orders` 表中每个客户的订单总额，并将结果按照客户名称进行分组，同时将总额舍入到小数点后两位：。这个查询将返回一个结果集，其中每行包含一个客户的名称和该客户的订单总额（经过四舍五入处理）。结果集中的行数等于 `orders` 表中不同客户的数量。

```sql
SELECT customer_name, ROUND(SUM(order_total), 2)
FROM orders
GROUP BY customer_name;
```



#### DiSTINCT

在 SQL 中，`DISTINCT` 是用于去重的关键字，它可以用于查询操作中，返回一组不重复的结果集。

具体来说，`DISTINCT` 关键字可以用于以下两种情况：

1. 在 `SELECT` 语句中，用于去除查询结果中的重复行。

例如，下面的 SQL 语句查询 `employee` 表中的所有不重复的部门名称：

```
SELECT DISTINCT department FROM employee;
```

2. 在聚合函数中，用于对指定列进行去重并进行聚合计算。

例如，下面的 SQL 语句计算 `employee` 表中不同部门的平均薪资：

```
SELECT department, AVG(DISTINCT salary) FROM employee GROUP BY department;
```

需要注意的是，`DISTINCT` 关键字会对查询的性能产生影响，因为它需要在内存中对查询结果进行去重。在处理大数据量时，使用 `DISTINCT` 可能会导致查询变慢，因此需要根据具体情况进行优化。





#### HAVING

HAVING 关键字类似 WHERE 关键字,但有两个区别:

1. WHERE 关键字用于过滤行, HAVING 关键字用于过滤分组。
2. WHERE 关键字在分组之前运行, HAVING 关键字在分组之后运行。

也就是说,HAVING 关键字用于基于分组后的计算结果对分组应用过滤条件。

**语法**

`aggregate_function() 是聚合函数,如 count()、sum() 等, 也即只可用聚合函数做条件`

```sql
SELECT column_name, aggregate_function(column_name)
FROM table_name
WHERE column_name operator value
GROUP BY column_name
HAVING aggregate_function(column_name) operator value;
```

举个例子:

> 这里我们先对 employees 表根据 department 字段分组,然后使用 HAVING 过滤只有员工人数大于 10 的部门。
>
> 所以简单来说, HAVING 关键字的作用是:基于分组后的计算结果对结果集应用过滤条件。

```sql
SELECT department, COUNT(*) FROM employees
GROUP BY department
HAVING COUNT(*) > 10;
```





#### CASE ... WHEN

`使用 CASE 来锁定需要使用条件语句判断输出结果的信息`

写一个SQL查询，每三个线段报告它们是否可以形成一个三角形。

```sql
SELECT *,
    CASE
        WHEN x + y > z AND x + z > y AND y + z > x THEN 'Yes'
        ELSE 'No'
    END AS 'triangle'
FROM
    triangle;
```





#### IF

`使用 IF 来锁定需要使用条件语句判断输出结果的信息`

写一个SQL查询，每三个线段报告它们是否可以形成一个三角形。

```sql
Select *,IF(x+y>z and x+z>y and y+z>x, "Yes", "No") AS triangle
FROM triangle
```





#### IFNULL

`IFNULL()` 是 MySQL 中的一个函数，用于检查一个表达式是否为 `NULL`，如果是 `NULL`，则返回一个指定的替代值；如果不是 `NULL`，则返回原始的表达式值。

**语法**

```sql
IFNULL(expr1, expr2)
```

其中，`expr1` 是要检查的表达式，`expr2` 是 `expr1` 为 `NULL` 时要返回的替代值。

例如，如果有一个名为 `orders` 的表，其中包含 `total_price` 和 `discount` 两个列，需要计算每个订单的实际支付金额，可以使用以下 SQL 查询语句：

```
SELECT total_price - IFNULL(discount, 0) AS actual_price
FROM orders;
```

这将返回一个包含每个订单实际支付金额的结果集。如果某个订单没有折扣，那么该订单的 `discount` 列将为 `NULL`，在计算实际支付金额时，将使用 `IFNULL(discount, 0)` 来将 `NULL` 替换为 0，以确保计算结果的正确性。





#### UNION & UNION ALL

- UNION

  `UNION 操作符用于合并两个或多个 SELECT 语句的结果集。 请注意，UNION 内部的每个 SELECT 语句必须拥有相同数量的列。列也必须拥有相似的数据类型。同时，每个 SELECT 语句中的列的顺序必须相同。`

  **1) 语法**

  ```sql
  SELECT column_name(s) FROM table1
  UNION
  SELECT column_name(s) FROM table2;
  ```

  ​	**注释：**默认地，UNION 操作符选取不同的值。如果允许重复的值，请使用 UNION ALL。

  **2) 实例**

  下面的 SQL 语句从 "Websites" 和 "apps" 表中选取所有**不同的** country（只有不同的值）：

  ```sql
  SELECT country FROM data1
  UNION
  SELECT country FROM data2
  ORDER BY country;
  ```

- UNION ALL

  **1) 语法**

  ​    注释：UNION 结果集中的列名总是等于 UNION 中第一个 SELECT 语句中的列名。

  ```sql
  SELECT column_name(s) FROM table1
  UNION ALL
  SELECT column_name(s) FROM table2;
  ```

  **2) 实例**

  下面的 SQL 语句从 "Websites" 和 "apps" 表中选取所有**不同的** country（也有重复的值）：

  ```sql
  SELECT country FROM data1
  UNION ALL
  SELECT country FROM data2
  ORDER BY country;
  ```

- 区别

  `UNION ALL` 允许重复值, `UNION` 不允许重复值



#### LIMIT





#### REGEXP







#### 窗户函数 OVER - PARTITION BY

> 在 MySQL 中，窗口函数是一种用于对查询结果集进行计算和分析的高级功能。它们允许在查询中应用聚合函数，同时保留原始查询结果的行和列的完整性。
>
> 窗口函数使用 **OVER** 子句来定义它们的行为，其中包括 **PARTITION BY** 子句和 ORDER BY 子句。
>
> - PARTITION BY：通过指定一个或多个列，将结果集分割成不同的分区。在每个分区中，窗口函数将独立计算结果。
> - ORDER BY：用于对每个分区内的行进行排序，以确定窗口函数计算的顺序。

**举例**

以下是一个示例，演示如何使用窗口函数在 MySQL 中计算每个部门的销售总额和每个部门中每个员工的销售额排名：

```
SELECT
  department,
  employee,
  sales,
  SUM(sales) OVER (PARTITION BY department) AS department_total_sales,
  RANK() OVER (PARTITION BY department ORDER BY sales DESC) AS rank
FROM
  sales_table;
```

上述查询将从名为 "sales_table" 的表中选择部门、员工和销售额列。使用窗口函数，它计算了每个部门的销售总额，并为每个部门的每个员工计算了销售额的排名。



**常见的窗口函数包括：**

1. ROW_NUMBER()：为每一行分配一个唯一的整数值，根据指定的排序顺序排序。

2. RANK()：为每个行分配一个唯一的整数值，根据指定的排序顺序排序。如果存在相同的值，则会跳过下一个整数值。`也即当排序数值重复时会为重复数值赋值以不同的编号`

3. DENSE_RANK()：为每个行分配一个唯一的整数值，根据指定的排序顺序排序。如果存在相同的值，则不会跳过下一个整数值。`也即当排序数值重复时会为重复数值赋值以相同的编号`

   LC185 [部门工资前三高的所有员工](https://leetcode.cn/problems/department-top-three-salaries/)

   表: `Employee`

   ```
   +--------------+---------+
   | Column Name  | Type    |
   +--------------+---------+
   | id           | int     |
   | name         | varchar |
   | salary       | int     |
   | departmentId | int     |
   +--------------+---------+
   id 是该表的主键列(具有唯一值的列)。
   departmentId 是 Department 表中 ID 的外键（reference 列）。
   该表的每一行都表示员工的ID、姓名和工资。它还包含了他们部门的ID。
   ```

   表: `Department`

   ```
   +-------------+---------+
   | Column Name | Type    |
   +-------------+---------+
   | id          | int     |
   | name        | varchar |
   +-------------+---------+
   id 是该表的主键列(具有唯一值的列)。
   该表的每一行表示部门ID和部门名。
   ```

   公司的主管们感兴趣的是公司每个部门中谁赚的钱最多。一个部门的 **高收入者** 是指一个员工的工资在该部门的 **不同** 工资中 **排名前三** 。

   编写解决方案，找出每个部门中 **收入高的员工** 。

   以 **任意顺序** 返回结果表。

   返回结果格式如下所示。

   **示例 1:**

   ```
   输入: 
   Employee 表:
   +----+-------+--------+--------------+
   | id | name  | salary | departmentId |
   +----+-------+--------+--------------+
   | 1  | Joe   | 85000  | 1            |
   | 2  | Henry | 80000  | 2            |
   | 3  | Sam   | 60000  | 2            |
   | 4  | Max   | 90000  | 1            |
   | 5  | Janet | 69000  | 1            |
   | 6  | Randy | 85000  | 1            |
   | 7  | Will  | 70000  | 1            |
   +----+-------+--------+--------------+
   Department  表:
   +----+-------+
   | id | name  |
   +----+-------+
   | 1  | IT    |
   | 2  | Sales |
   +----+-------+
   输出: 
   +------------+----------+--------+
   | Department | Employee | Salary |
   +------------+----------+--------+
   | IT         | Max      | 90000  |
   | IT         | Joe      | 85000  |
   | IT         | Randy    | 85000  |
   | IT         | Will     | 70000  |
   | Sales      | Henry    | 80000  |
   | Sales      | Sam      | 60000  |
   +------------+----------+--------+
   解释:
   在IT部门:
   - Max的工资最高
   - 兰迪和乔都赚取第二高的独特的薪水
   - 威尔的薪水是第三高的
   
   在销售部:
   - 亨利的工资最高
   - 山姆的薪水第二高
   - 没有第三高的工资，因为只有两名员工
   ```

   **题解**

   ```sql
   SELECT d.name AS Department, e.name AS Employee, e.salary AS Salary
   FROM Department AS d, (
     SELECT *, DENSE_RANK() OVER(PARTITION BY departmentId ORDER BY salary DESC) AS RK
     FROM Employee
   ) e
   WHERE e.RK < 4 AND  e.departmentId = d.id; 
   ```

4. SUM()、COUNT()、AVG() 等聚合函数：用于计算分区内的聚合值。

5. LAG()、LEAD(): 用于获取当前行前面或后面的行的值。









