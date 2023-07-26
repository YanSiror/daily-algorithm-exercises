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



#### Sum

在 SQL 中，SUM 是一个聚合函数，用于计算指定列的总和。在使用 SUM 函数时，需要指定要进行计算的列。

```sql
sum(price)		//计算价格总和
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



