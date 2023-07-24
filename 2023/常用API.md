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
Arrays.copyOfRange(nums,stratIndex,endIndex)
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



