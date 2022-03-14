# 1 数据处理

## 1.1  数组翻转

### 整型数组的翻转

```c
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
```

### 整型数字的交换

```c
/*
 * 输入: 待交换的两个数
 * 输出: 交换后的结果
*/
void swap(int * a,int * b){
    int temp = *a;
    *a = *b;
    *b = temp;
}
```

### 整形数组最大值

```c
/*
 * 输入: 数组 数组大小 可返回的最大值下标位置
 * 输出: 最大值
*/
int getMax(int * nums,int numsSize,int * index){
    int i = 0,max = 0;
    *index = 0;		//初始化index
    for(i = 0;i < numsSize;i++){
        if(max < nums[i]){
            max = nums[i];
            *index = i;
        }
    }
    return max;
}
```

### 整形数组最小值

```c
/*
 * 输入: 数组 数组大小 可返回的最小值下标位置
 * 输出: 最小值
*/
int getMin(int * nums,int numsSize,int * index){
    if(numsSize == -1)
        return -1;
    int i = 0,min = nums[0];
    *index = 0;		//初始化index
    for(i = 0;i < numsSize;i++){
        if(min > nums[i]){
            min = nums[i];
            *index = i;
        }
    }
    return min;
}
```

### 整形数组取子数组元素

```c
/*
 * 输入: 数组 数组大小 起始下标 终止下标 结果数组大小
 * 输出: 数组值 / NULL
*/
int * getSubArr(int * nums,int numsSize,int start,int end,int * returnSize){
    int i,j,tag = 0;
    //判断错误
    if(start < 0 || end > numsSize - 1){
        printf("参数错误!");
        return NULL;
    }

    int * result = malloc(sizeof(int) * (end - start + 1));
    for(i = start;i <= end;i++)
        result[tag++] = nums[i];
    *returnSize = tag;
    return result;
}
```



### 整型数字拆分

- **倒序**

  与输入的数字高低位 相反  `reverse order`

  ```c
  /*
   * 输入: 数字 可返回的数字位数
   * 输出: 数字拆分后的一维数组(倒序)  reverse order
  */
  int * splitDigitRE(int num,int * size){
      //记录数字位数
      int length = 0,temp = num;
      while(temp){
          temp /= 10;
          length++;
      }
      *size = length;
  
      //划分数组
      int * nums = malloc(sizeof(int) * length);
      temp = num;
      int i = 0;
      while(temp){
          nums[i++] = temp % 10;
          temp /= 10;
      }
      return nums;
  }
  ```

- **正序**

  与输入的数字高低位 相同  `positive order`

  ```c
  /*
   * 输入: 数字 可返回的数字位数
   * 输出: 数字拆分后的一维数组(正序 - 翻转即可) positive order
  */
  int * splitDigitPO(int num,int * size){
      //记录数字位数
      int length = 0,temp = num;
      while(temp){
          temp /= 10;
          length++;
      }
      *size = length;
  
      //划分数组
      int * nums = malloc(sizeof(int) * length);
      temp = num;
      int i = 0;
      while(temp){
          nums[i++] = temp % 10;
          temp /= 10;
      }
  
      //翻转
      for(i = 0;i < length/2;i++){
          int temp = nums[i];
          nums[i] = nums[length-i-1];
          nums[length-i-1] = temp;
      }
      return nums;
  }
  ```

  

### 整型数组合并(纯正数)

- **倒序**

  与输入的数字高低位 相反   `reverse order`

  ```c
  /*
   * 输入: 拆分后的数组 长度
   * 输出: 合并后的数字 reverse order
  */
  int digitCombinationRO(int * nums,int size){
      int i;
      double result = 0;
      for(i = 0;i < size;i++)
          result += nums[i] * pow(10,i);
      return result;
  }
  ```

- **正序**

  与输入的数字高低位 相同   `positive order`

  ```c
  /*
   * 输入: 拆分后的数组 长度 
   * 输出: 合并后的数字 positive order
  */
  int digitCombinationPO(int * nums,int size){
      int i,result = 0;
      for(i = size - 1;i >= 0;i--)
          result += nums[i] * pow(10,size - i - 1);
      return result;
  }
  ```




### 整型数组合并(正负均可)

```c
/*
 * 输入: 拆分后的数组 长度 正或负(1/0)
 * 输出: 合并后的数字 positive order
 * 解释: result > INT_MAX 返回 INT_MAX
        result < INT_MIN 返回 INT_MIN
        tag 表示正负标号
*/
int digitCombinationPO(int * nums,int size,int tag){
    int i,result = 0;
    //正数
    if(tag == 1){
        for(i = size - 1;i >= 0;i--){
            if(result + nums[i] * pow(10,size - i - 1) > INT_MAX)
                return INT_MAX;
            result += nums[i] * pow(10,size - i - 1);
        }
    }
    else if(tag == 0){
        for(i = size - 1;i >= 0;i--){
            if(result - nums[i] * pow(10,size - i - 1) < INT_MIN)
                return INT_MIN;
            result -= nums[i] * pow(10,size - i - 1);
        }
    }
    return result;
}
```





## 1.2 字符数组

### 二维转一维

`code::blocks` 版本

```c
/*
 * 输入: 数组 数组大小
 * 输出: 平铺后的一维字符数组
*/
char * flatten(char str[][10],int strSize){
    //统计长度
    int i,j,length = 0;
    for(i = 0;i < strSize;i++)
        for(j = 0;j < strlen(str[i]);j++)
            length++;
    //平铺
    char * result = malloc(sizeof(char) * (length+1));
    int tag = 0;    //记录下标
    for(i = 0;i < strSize;i++)
        for(j = 0;j < strlen(str[i]);j++)
            result[tag++] = str[i][j];
    result[tag] = '\0';     //标识终止符
    printf("%s ",result);
    return result;
}
```

`LeetCode` 版本

```c
/*
 * 输入: 数组 数组大小
 * 输出: 平铺后的一维字符数组
*/
char * flatten(char ** str,int strSize){
    //统计长度
    int i,j,length = 0;
    for(i = 0;i < strSize;i++)
        for(j = 0;j < strlen(str[i]);j++)
            length++;
    //平铺
    char * result = malloc(sizeof(char) * (length+1));
    int tag = 0;    //记录下标
    for(i = 0;i < strSize;i++)
        for(j = 0;j < strlen(str[i]);j++)
            result[tag++] = str[i][j];
    result[tag] = '\0';     //标识终止符
    return result;
}

```



### 字符数组的翻转

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
```



### 字符数组转整型

```c
/*
 * 输入: 可转换为数字的字符数组
 * 输出: 转换后的数字
*/
int strToInt(char * str){
    int length = strlen(str);
    int i;
    int * nums = malloc(sizeof(int) * length);
    for(i = 0;i < length;i++)
        nums[i] = str[i] - '0';

    //合并数组为整数
    double result = 0;
    for(i = length - 1;i >= 0;i--)
        result += nums[i] * pow(10,length - i - 1);
    return result;
}
```



### 按字符分割字符串

```c
/*
 * 输入: 将字符串根据字符 ch 进行划分
 * 输出: 划分后的二维数组
 * 可接受: ss1bb1  以1位分割符
*/
char ** splitAsChar(char * str,char ch,int * returnsize){
    //首先记录字符长度
    int length = 1,i;
    char * head = str;
    while(*head){
        if(*head == ch)
            length++;
        head++;
    }

    //生成二维数组
    int ** result = malloc(sizeof(char*) * length);
    for(i = 0;i < length;i++)
        result[i] = malloc(sizeof(char) * 20);

    //开始分割
    head = str;
    char temp[10];
    int tag = 0,cur = 0;
    while(*head){
        if(*head != ch){
            temp[tag++] = *head;
            temp[tag] = '\0';
        } else{
            strcpy(result[cur++],temp);
            temp[tag] = '\0';
            tag = 0;
        }
        head++;
    }
    //末尾没有进行赋值
    strcpy(result[cur],temp);

    *returnsize = length;
    return result;
}
```



## 字符串拷贝

```c
/*
 * 输入: 需要拷贝的字符串
 * 输出: 拷贝完成后的的字符串指针
*/
char * strCopy(char * s){
    //拷贝一份
    int i = 0;
    char * temp = malloc(sizeof(char) * (strlen(s)+1));
    for(i = 0;i < strlen(s);i++)
        temp[i] = s[i];
    temp[i] = '\0';
    return temp;
}
```



## 字符串转整数   atoi() 

> 请你来实现一个 `myAtoi(string s)` 函数，使其能将字符串转换成一个 32 位有符号整数（类似 C/C++ 中的 `atoi` 函数）。
>
> 函数 `myAtoi(string s)` 的算法如下：
>
> 读入字符串并丢弃无用的前导空格
> 检查下一个字符（假设还未到字符末尾）为正还是负号，读取该字符（如果有）。 确定最终结果是负数还是正数。 如果两者都不存在，则假定结果为正。
> 读入下一个字符，直到到达下一个非数字字符或到达输入的结尾。字符串的其余部分将被忽略。
> 将前面步骤读入的这些数字转换为整数（即，"123" -> 123， "0032" -> 32）。如果没有读入数字，则整数为 0 。必要时更改符号（从步骤 2 开始）。
> 如果整数数超过 32 位有符号整数范围 [−231,  231 − 1] ，需要截断这个整数，使其保持在这个范围内。具体来说，小于 −231 的整数应该被固定为 −231 ，大于 231 − 1 的整数应该被固定为 231 − 1 。
> 返回整数作为最终结果。



```c
/*
 * 输入: 拆分后的数组 长度 正或负
 * 输出: 合并后的数字 positive order
*/
int digitCombinationPO(int * nums,int size,int tag){
    int i,result = 0;
    //正数
    if(tag == 1){
        for(i = size - 1;i >= 0;i--){
            if(result + nums[i] * pow(10,size - i - 1) > INT_MAX)
                return INT_MAX;
            result += nums[i] * pow(10,size - i - 1);
        }
    }
    else if(tag == 0){
        for(i = size - 1;i >= 0;i--){
            if(result - nums[i] * pow(10,size - i - 1) < INT_MIN)
                return INT_MIN;
            result -= nums[i] * pow(10,size - i - 1);
        }
    }
    return result;
}

int myAtoi(char * s){
    int tag = 1;        //判断是正或负 1正 0负
    int size = 0;       //数组大小
    int flag = 0;       //是否是前导空格
    int * nums = malloc(sizeof(int) * strlen(s));
    while(*s){
        if(*s == ' ' && flag == 0){
            s++;
            continue;
        }
        if(*s == '-' && flag == 0){
            tag = 0;
            s++;
        }
        else if(*s == '+' && flag == 0){
            tag = 1;
            s++;
        }
        flag = 1;       //前导读取完毕

        if(*s >= '0' && *s <= '9'){
            nums[size++] = *s - '0';
        }else
            break;
        s++;
    }
    int result = digitCombinationPO(nums,size,tag);
    return result;
}
```



## 1.3 进制运算

### 十进制转二进制

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
```



### 十进制转N进制

```c
/*
 * 输入: 整数 num 可返回的长度 size 待转换的进制数 N
 * 输出: 转换后的二进制的数组  数组长度参数
 * 说明: 该数组返回的数组结果从小端的 从个位开始, 并且正负值转换后都得到的是正值
 * 		如: -1/1 -> 1    -2/2 -> 10   -3/3 -> 11 
*/
int * tenToNArray(int num,int * size,int n){
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
        temp /= n;
        len++;
    }

    //转换为2进制, 保存到数组
    int * nums= malloc(sizeof(int) * len);
    int tag = 0,i;  //tag用于移动nums数组下标

    temp = abs(num);
    while(temp){
        nums[tag++] = temp % n;
        temp /= n;
    }
    *size = len;
    return nums;
}
```



### 二进制求和

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



## 1.4 CHAR 与 INT 的相互转换

- `char to int`

  ```c
  /*
   * 输入: 字符 c
   * 输出: 整数 
  */
  int charToInt(char c){
  	return c - '0';
  }
  ```

- `int to char`

  ```c
  /*
   * 输入: 整数 
   * 输出: 字符 c
  */
  char intToChar(int n){
  	return n + '0';
  }
  ```




## 1.5  数组数据重置

### 整型数组

```c
/*
 * 输入: 整型数组
 * 输出: 经重新赋值的数组
 * 参数: 数组 数组大小 目标值
*/
void resetArrayOfInt(int * nums,int size,int value){
    int i;
    for(i = 0;i < size;i++)
        nums[i] = value;
}
```



### 字符数组

```c
/*
 * 输入: 字符数组
 * 输出: 经重新赋值的字符数组
 * 参数: 数组 数组大小 目标值
*/
void resetArrayOfCh(char str[],int size,char value){
    int i;
    for(i = 0;i < size;i++)
        str[i] = value;
}
```





# 2 排序

## 2.1 冒泡排序

- **降序**

  ```c
  /*
   * 输入: 整型数组 数组大小
   * 输出: 返回型参数返回数组结果 或 返回整型数组
   * 说明: 降序排序
  */
  int * bubbleSortDC(int * nums,int size){
      int i,j;
      for(i = 0;i < size - 1;i++){
          for(j = 0;j < size - i - 1;j++){
              if(nums[j] < nums[j+1]){
                  int temp = nums[j];
                  nums[j] = nums[j+1];
                  nums[j+1] = temp;
              }
          }
      }
      return nums;
  }
  ```

- **升序**

  ```c
  /*
   * 输入: 整型数组 数组大小
   * 输出: 返回型参数返回数组结果 或 返回整型数组
   * 说明: 升序排序
  */
  int * bubbleSortAC(int * nums,int size){
      int i,j;
      for(i = 0;i < size - 1;i++){
          for(j = 0;j < size - i - 1;j++){
              if(nums[j] > nums[j+1]){
                  int temp = nums[j];
                  nums[j] = nums[j+1];
                  nums[j+1] = temp;
              }
          }
      }
      return nums;
  }
  ```

  



## 2.2 快速排序

- **调用 C 库函数内置 `qsort()` 函数**

  ```c
  int cmp(const void *a,const void *b){
      return *(int*)a - *(int*)b;
  }
  ```

- **降序**

  ```c
  /*
   * 降序排序
   * 输入: 整型数组 最小下标 最大下标
   * 输出: 空
  */
  void quickSortDC(int a[],int left,int right)
  {
      int i,j,key;
      i = left;
      j = right;
      key = a[left];
      if(left>right)
          return;
  
      //每次排序都以 key 为基准, 右侧寻找一个小于 key 的数
      //左侧寻找一个大于 key 的数, 两者交换
      //最后使得 最终位置 左侧都大于 key,右侧都小于 key ,也即key
      //来到了它的最终位置 FinalPosition
      while(i != j)
      {
          while(a[j] < key && j>i)    j--;    //从右向左查找第一个小于K的数
          if(j>i)
              a[i++] = a[j];
          while(a[i] > key && j>i)    i++;    //从左向右查找第一个大于K的数
          if(j>i)
              a[j--] = a[i];
  	}
      a[i] = key;
      quickSortDC(a,left,i-1);      // 排序k左边
      quickSortDC(a,i+1,right);     // 排序k右边
  }
  ```

- **升序**

  ```c
  /*
   * 升序排序
   * 输入: 整型数组 最小下标 最大下标
   * 输出: 空
  */
  void quickSortAC(int a[],int left,int right)
  {
      int i,j,key;
      i = left;
      j = right;
      key = a[left];
      if(left>right)
          return;
  
      //每次排序都以 key 为基准, 右侧寻找一个大于 key 的数
      //左侧寻找一个小于 key 的数, 两者交换
      //最后使得 最终位置 左侧都小于 key,右侧都大于 key ,也即key
      //来到了它的最终位置 FinalPosition
      while(i != j)
      {
          while(a[j] > key && j>i)    j--;    //从右向左查找第一个小于K的数
          if(j>i)
              a[i++] = a[j];
          while(a[i] < key && j>i)    i++;    //从左向右查找第一个小于K的数
          if(j>i)
              a[j--] = a[i];
  	}
      a[i] = key;
      quickSortAC(a,left,i-1);      // 排序k左边
      quickSortAC(a,i+1,right);     // 排序k右边
  }
  ```
  
  

# 3 查找

### 二分查找

```c
/**
 * 输入: 整型数组 最小下标 最大下标 待查找的目标值
 * 输出: 查找到返回下标,未查找到返回-1
 **/
int binSearch(int * nums,int low,int high,int target){
    int left = low,right = high;
    while(left <= right){
        int mid = (left+right)/2;
        if(nums[mid] == target){
            return mid;
        } else if(nums[mid] < target){
            left = mid + 1;
        } else if(nums[mid] > target){
            right = mid - 1;
        }
    }
    return -1;
}
```





​		

