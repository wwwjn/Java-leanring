

## day07 - 数组中的算法

### 数组中涉及到的常见算法

#### 数组元素的赋值（杨辉三角、回形数）

创建一个长度为6的int型数组，要求数组元素的值都在1-30之间，且是随机赋值。同时，要求
元素的值各不相同。

```java
class ArrayExer {
	public static void main(String[] args) {
		//方式一：
//		int[] arr = new int[6];
//		for (int i = 0; i < arr.length; i++) {// [0,1) [0,30) [1,31)
//			arr[i] = (int) (Math.random() * 30) + 1;
//
//			boolean flag = false;
//			while (true) {
//				for (int j = 0; j < i; j++) {
//					if (arr[i] == arr[j]) {
//						flag = true;
//						break;
//					}
//				}
//				if (flag) {
//					arr[i] = (int) (Math.random() * 30) + 1;
//					flag = false;
//					continue;
//				}
//				break;
//			}
//		}
//
//		for (int i = 0; i < arr.length; i++) {
//			System.out.println(arr[i]);
//		}
		//方式二：
		int[] arr = new int[6];
		for (int i = 0; i < arr.length; i++) {// [0,1) [0,30) [1,31)
			arr[i] = (int) (Math.random() * 30) + 1;
			
				for (int j = 0; j < i; j++) {
					if (arr[i] == arr[j]) {
						i--;
						break;
					}
				}
			}

		for (int i = 0; i < arr.length; i++) {
			System.out.println(arr[i]);
		}
	}
}

```

#### 回形数格式方阵的实现

从键盘输入一个整数（1~20） 

则以该数字为矩阵的大小，把1,2,3…n*n 的数字按照顺时针螺旋的形式填入其中。例如： 输入数字2，则程序输出： 1 2 

4 3 

输入数字3，则程序输出： 1 2 3 

8 9 4 

7 6 5 

输入数字4， 则程序输出： 

1  2  3  4 

12 13 14 5 

11 16 15 6 

10  9 8  7

```java
class RectangleTest {
	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);
		System.out.println("输入一个数字");
		int len = scanner.nextInt();
		int[][] arr = new int[len][len];

		int s = len * len;
		/*
		 * k = 1:向右 k = 2:向下 k = 3:向左 k = 4:向上
		 */
		int k = 1;
		int i = 0, j = 0;
		for (int m = 1; m <= s; m++) {
			if (k == 1) {
				if (j < len && arr[i][j] == 0) {
					arr[i][j++] = m;
				} else {
					k = 2;
					i++;
					j--;
					m--;
				}
			} else if (k == 2) {
				if (i < len && arr[i][j] == 0) {
					arr[i++][j] = m;
				} else {
					k = 3;
					i--;
					j--;
					m--;
				}
			} else if (k == 3) {
				if (j >= 0 && arr[i][j] == 0) {
					arr[i][j--] = m;
				} else {
					k = 4;
					i--;
					j++;
					m--;
				}
			} else if (k == 4) {
				if (i >= 0 && arr[i][j] == 0) {
					arr[i--][j] = m;
				} else {
					k = 1;
					i++;
					j++;
					m--;
				}
			}
		}

		// 遍历
		for (int m = 0; m < arr.length; m++) {
			for (int n = 0; n < arr[m].length; n++) {
				System.out.print(arr[m][n] + "\t");
			}
			System.out.println();
		}
	}
}

```

 方式2

```java
class RectangleTest1 {

	public static void main(String[] args) {
		int n = 7;
		int[][] arr = new int[n][n];

		int count = 0; // 要显示的数据
		int maxX = n - 1; // x轴的最大下标
		int maxY = n - 1; // Y轴的最大下标
		int minX = 0; // x轴的最小下标
		int minY = 0; // Y轴的最小下标
		while (minX <= maxX) {
			for (int x = minX; x <= maxX; x++) {
				arr[minY][x] = ++count;
			}
			minY++;
			for (int y = minY; y <= maxY; y++) {
				arr[y][maxX] = ++count;
			}
			maxX--;
			for (int x = maxX; x >= minX; x--) {
				arr[maxY][x] = ++count;
			}
			maxY--;
			for (int y = maxY; y >= minY; y--) {
				arr[y][minX] = ++count;
			}
			minX++;
		}

		for (int i = 0; i < arr.length; i++) {
			for (int j = 0; j < arr.length; j++) {
				String space = (arr[i][j] + "").length() == 1 ? "0" : "";
				System.out.print(space + arr[i][j] + " ");
			}
			System.out.println();
		}
	}
}

```



#### 求数值型数组中元素的最大值、最小值、平均数、总数等

![image-20200218160702737](C:\Users\lfrdw\AppData\Roaming\Typora\typora-user-images\image-20200218160702737.png)



#### 数组的复制、反转和查找（线性查找，二分法查找）

` int[] array1 = new int[]{1,2,3,4};`

`array2 = array1;` ，修改array2 然后打印array1，array1也发生了变化。在堆空间中只有一个array1数组。

- 浅复制，只复制了array1的地址给array2
-  只new了一次，在堆空间中就只有一份array数组

- 如果想要实现深复制——通过循环逐个给array2赋值

##### 反转

```java
//数组的反转
//方法一：
		for(int i = 0;i < arr.length / 2;i++){
			String temp = arr[i];
			arr[i] = arr[arr.length - i -1];
			arr[arr.length - i -1] = temp;
		}
		
//方法二：
		for(int i = 0,j = arr.length - 1;i < j;i++,j--){
			String temp = arr[i];
			arr[i] = arr[j];
			arr[j] = temp;
		}
		
```

##### 查找

1. 线性查找：从左到右找
2. 二分法查找：要查找的数组必须有序



#### 排序算法

衡量算法优劣：时间复杂度/空间复杂度/稳定性

##### 冒泡排序：每一轮比相邻两个元素的大小

```java
public class BubbleSortTest{
	public static void main(String[] args){
		int[] arr= new int[]{43,32,76,-98,0,63,-21,32,99};
        
        //冒泡排序
        for(int i =0; i < arr.length-1; i++){  //扫描几个轮次
            for(int j=0;j < arr.length-1-i;j++){  //注意这个地方不用扫描到整个长度
            	if(arr[j] > arr[j+1]){
                    int temp = arr[j];  //交换
                    arr[j] = arr[j+1];
                    arr[j+1] = temp;
                }
            }
        }
        for(int i=0; i < arr.length; i++){
            System.out.print(arr[i]);
        }
	}
}
```

- 内部循环不用循环整个数组长度，因为最大的数已经冒泡到了最右侧应该在的位置
- <img src="C:\Users\lfrdw\AppData\Roaming\Typora\typora-user-images\image-20200218174904721.png" alt="image-20200218174904721" style="zoom:50%;" />



##### 快速排序

![image-20200218175259028](C:\Users\lfrdw\AppData\Roaming\Typora\typora-user-images\image-20200218175259028.png)

- high右侧都是比pivot大的，low左侧都是比pivot小的

- 把Pivot放在合适的地方后，对于左侧和右侧单独递归执行快排算法



### Array工具类的使用

- 提供了比较、复制、排序等方法

  ![image-20200218175806607](C:\Users\lfrdw\AppData\Roaming\Typora\typora-user-images\image-20200218175806607.png)



### 数组使用中常见的异常

ArrayIndexOutOfBoundsException: 数组越界异常

NullPointException：空指针异常

- 如果数组名的指针是null，会发生空指针异常

- 二维数组第二维度没有指明

  ` int[][] arr2 = new int[4][]`

  ` System.out.print(arr2[0][0])`