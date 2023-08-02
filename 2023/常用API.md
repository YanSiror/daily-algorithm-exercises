## 数组

### 排序

```java
Arrays.sort(nums)
```



### 初始赋值

```java
Arrays.fill(arr, 0);
```



### 切割

```java
Arrays.copyOfRange(nums, stratIndex, endIndex)
```



### 比较

```java
Math.max(a,b);

//比较两个数组对应值是否相等
List<Integer> arr1 = new ArrayList<Integer>();
List<Integer> arr2 = new ArrayList<Integer>();
//true or false
arr1.equals(arr2);	

```



## 字符串

### 获取第 i 个字符

```java
t.charAt(i)
```



### 字符数组转换

```java
String s = "hello";
char[] chars = s.toCharArray();		//转换为 char 数组
String b = new String(chars);		//转换为 String 字符串
```



## Lambda 表达式

### 遍历

```java
Arrays.stream(flowerbed).forEach(num ->{
     System.out.print(num + " ");
});
```



## 优先队列

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



## 哈希表

### 遍历

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



### 取值或设为默认

```java
 map.getOrDefault('key', 0)		//存在key则返回值, 不存在key则设为0
```





## 队列

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



## 栈

```java
push() - 添加元素到栈顶
pop() - 删除栈顶元素
peek() - 查看栈顶元素
size() - 查看栈的大小
empty() - 检查栈是否为空
search() - 查找栈中一个元素
```



## 位运算

```java
i & 1    //检测 i 的最低位是多少(0 或 1), 可以用于对2取模
i | 1    //将 i 的最低位强行设为 1
i >> 1   //右移一位,相当于除以 2
i << 1   //左移一位,相当于乘以 2
```



## 树

### 深度优先遍历(DFS)

```java
List<TreeNode> treeNodeList = new ArrayList<>();
public List<TreeNode> dfsRec(TreeNode root) {

    if (root == null) {
        return null;
    }
    treeNodeList.add(root);
    //System.out.print(root.value+" ");
    dfsRec(root.left);
    dfsRec(root.right);
    return treeNodeList;
}
```



### 广度优先遍历(BFS)

```java
public static <V> void bfs(List<TreeNode<V>> children, int depth) {
    List<TreeNode<V>> thisChildren, allChildren = new ArrayList<>();
    for (TreeNode<V> child: children) {
        //打印节点值以及深度
        System.out.println(child.getValue().toString() + ",   " + depth);
        thisChildren = child.getChildList();
        if (thisChildren != null && thisChildren.size() > 0) {
            allChildren.addAll(thisChildren);
        }
    }
    if (allChildren.size() > 0)  {
        bfs(allChildren, depth + 1);
    }
}
```









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



### 聚合函数

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

### 语法

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



#### LEFT

`取前 N 个字符:  LEFT(STR, 7)`

使用 left() 函数取 trans_date 列的前7个字符,也即取月份。

```sql
left(trans_date,7)
```



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

1. WHERE 关键字用于过滤行,HAVING 关键字用于过滤分组。
2. WHERE 关键字在分组之前运行,HAVING 关键字在分组之后运行。

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







