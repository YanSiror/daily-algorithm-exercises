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

- Entry

  ```java
  HashMap<Integer, Integer> map = new HashMap<Integer, Integer>();
  Iterator<Map.Entry<Integer, Integer>> it = map.entrySet().iterator();
  while (it.hasNext()) {
      Map.Entry<Integer, Integer> entry = it.next();
      System.out.println(entry.getKey());
      System.out.println(entry.getValue());
  }
  ```

- EntrySet

  ```java
  //Hash 表
  HashMap<Integer, Integer> map = new HashMap<Integer, Integer>();
  for(Map.Entry<Integer, Integer> entry : map.entrySet()){
      System.out.println(entry.getKey());
      System.out.println(entry.getValue());
  }
  ```

- KeySet

  ```java
  //Hash 表
  HashMap<Integer, Integer> map = new HashMap<Integer, Integer>();
  for(Integer key: map.keySet()){
      System.out.println(key);
      System.out.println(map.get(key));
  }
  ```

  
