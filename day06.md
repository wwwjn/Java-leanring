

## day06 - 数组

### Eclipse配置

（见文件 .\eclipse首次配置）

- 导入文件：

  文件乱码——UTF-8和GBK（ANSI）之间的转换

  注意导入的文件要最开始要增加 `package xxxx.xxxx.xxxx`

- 导入包： import-- defalut-- exsiting xxx



### 一维数组

- 数组是引用数据类型，数组中的元素可以是任何数据类型
- 内存中连续存放
- 数组的长度一旦确定就不能更改

#### 数组的声明和初始化

`int a[]=new int[5];` 动态初始化

- 数组初始化和数组元素的赋值分开进行

`int[] ids = new int[]{1001,1002,1003,1004};`静态初始化

- 数组的初始化和数组元素的赋值操作同时进行

- 注意：只有以上两种类型的写法合法
- 等号右端[]内如果有长度，就不可以用{}；如果没有长度，才可以有{}



#### 调用指定位置元素

- 数组索引从0开始！

  `names[0]="Java";`



#### 获取数组长度

`System.out.print(names.length);`



#### 遍历数组

`for(int i=0;i<names.length;i++){`

​	`System.out.println(names[i]);`

`}`



#### 默认初始化值

- 如果数组元素是整型，默认初始化值为0
- 浮点型：默认是0.0
- char：ASCII码是0
- boolean型是false



#### 一维数组的内存解析

数组名字保存在栈结构中，数组内容保存在堆结构中

- array重新指向一个堆空间后，启动"应用技术的辣鸡回收机制"

![image-20200218115233637](C:\Users\lfrdw\AppData\Roaming\Typora\typora-user-images\image-20200218115233637.png)



### 二维数组

#### 声明和初始化

`int[][] arr1 = new int[][]{{1,2,3}{2,3,4}{5,6,7}};` 静态初始化

`String[][] arr2 = new String[3][2] `  动态初始化

`String[][] arr2 = new String[3][] `   动态初始化，先声明一个维度的大小也可以

`int[] arr4[] = new int[][]{{1,2,3}{2,3,4}{5,6,7}};`  也是正确的

#### 调用指定位置

`arr[3][4]`

#### 获取数组的长度

`int[] arra4[] =new int [3][2];`

System.out.println(arr4.length);  //3

System.out.println(arr4[0].length);



#### 遍历二维数组

二维循环



#### 默认地址值

```java
	int[][] arr = new int[4][3];
	System.out.println(arr[0]);//[I@15db9742   一个地址值
	System.out.println(arr[0][0]);//0
```
```java
	double[][] arr3 = new double[4][];
	System.out.println(arr3[1]);//null
```
- 数组内层还没有初始化过，不知道指向堆的哪里，所以是个null空指针



#### 内存解析

![image-20200218154401836](C:\Users\lfrdw\AppData\Roaming\Typora\typora-user-images\image-20200218154401836.png)