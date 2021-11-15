# 1 数组翻转

## 1.1 整型数组的翻转

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



## 1.2 字符数组的翻转

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







## 2、十进制转二进制数组

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



## 3、十进制转 N 进制数组(进阶)

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



## 4、CHAR 与 INT 的相互转换

CHAR(字符型)  转换到 INT(整型)

```c
/*
 * 输入: 字符 c
 * 输出: 整数 
*/
int charToInt(char c){
	return c - '0';
}
```

INT(整型)  转换到 CHAR(字符型)

```
/*
 * 输入: 整数 
 * 输出: 字符 c
*/
char intToChar(int n){
	return n + '0';
}
```



## 5、冒泡排序

**降序**

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

**升序**

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



## 6、二进制求和

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





​		

