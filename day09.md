## day09 - Java面向对象2

### “万事万物皆对象”

1. 在Java语言范畴中，都将功能、结构封装到类中，通过类的实例化，调用具体的功能结构

2. 涉及到Java语言与前端HTML、后端的数据库交互时，前后端的结构在java层面交互时，都体现为类、对象



### 数组对象的内存解析

- 一个数组里的每个元素都是一个对象

  ![image-20200219112134056](C:\Users\lfrdw\AppData\Roaming\Typora\typora-user-images\image-20200219112134056.png)



### 匿名对象

`new Phone().price=1999;`

`new Phone().showPrice();`  // 0.0

new之后直接调用方法或者属性，没有显式的变量名



### 再谈方法

#### 方法的重载

在同一个类中，同名方法，形参不同（形参个数或者类型不同）

#### 可变个数的形参

- 允许直接定义能和多个实参相匹配的形参

```java
	public void show(String ... strs){  //可以接受0、1个或多个string类型形参
		System.out.println("show(String ... strs)");
		
		for(int i = 0;i < strs.length;i++){
			System.out.println(strs[i]);
		}
	}
	//不能与上一个方法同时存在
//	public void show(String[] strs){
//		
//	}
	
	//The variable argument type String of the method 
	//show must be the last parameter
//	public void show(String ...strs,int i){
//		
//	}
```

- 可变个数形参的方法与本类中方法名相同，形参不同的方法之间构成重载

 *   可变个数形参的方法与本类中方法名相同，形参类型也相同的数组之间不构成重载。换句话说，二者不能共存。
 *   可变个数形参在方法的形参中，必须声明在末尾
 * 	 可变个数形参在方法的形参中,最多只能声明一个可变形参。



#### 方法参数的值传递机制:star:

Java的实参值如何传入方法呢？**值传递**

将实际参数值的复制品传入方法内，参数本身不受影响



- 基本数据类型赋值时` int m = n;`是值传递，会产生一个n的复制品

- 引用数据类型（如数组、对象），赋值的是变量所保存的数据的地址值



##### 值传递

1. 参数类型为基本数据类型时

   <img src="C:\Users\lfrdw\AppData\Roaming\Typora\typora-user-images\image-20200219153835742.png" alt="image-20200219153835742" style="zoom:80%;" />

   使用上图中的代码无法达到交换m和n的效果，why？

   - m n 通过值传递的方法传递给swap， 在栈空间中复制了一份数据

   - swap方法执行后，栈空间中的所有swap()占用的部分被销毁
   - 继续在main()中打印后，打印的是main中定义的m和n，所以不能实现交换功能

2.  参数为引用数据类型时的交换

   - 通过同样的方法可以实现Data的m属性和n属性交换，因为传递的引用数据类型的地址

   ![image-20200219162523100](C:\Users\lfrdw\AppData\Roaming\Typora\typora-user-images\image-20200219162523100.png)

- 可以参照实现交换数组某2个位置的值交换

  ```java
  	public void swap(String[] arr,int m,int n){
  		int temp = arr[m] ;
  		arr[m] = arr[n];
  		arr[n] = temp;
  	}
  ```

##### 例题

![image-20200219164803687](C:\Users\lfrdw\AppData\Roaming\Typora\typora-user-images\image-20200219164803687.png)

![image-20200219164810773](C:\Users\lfrdw\AppData\Roaming\Typora\typora-user-images\image-20200219164810773.png)

有两个v，第二个v是在调用second()时，形参是采用值传递的方法，

**例题2**

![image-20200219165019116](C:\Users\lfrdw\AppData\Roaming\Typora\typora-user-images\image-20200219165019116.png)

方法2是重写输出流

![image-20200219165359369](C:\Users\lfrdw\AppData\Roaming\Typora\typora-user-images\image-20200219165359369.png)

<img src="C:\Users\lfrdw\AppData\Roaming\Typora\typora-user-images\image-20200219165328465.png" alt="image-20200219165328465" style="zoom:80%;" />

**例题3**

![image-20200219165621915](C:\Users\lfrdw\AppData\Roaming\Typora\typora-user-images\image-20200219165621915.png)

**例题4**

第二个输出的是char数组的内容。因为两个println调用的不是同一个方法，是两个重载的方法

<img src="C:\Users\lfrdw\AppData\Roaming\Typora\typora-user-images\image-20200219165744918.png" alt="image-20200219165744918" style="zoom:80%;" />

#### 递归方法

一个方法体内调用它自身。注意要有起始条件，朝着已知方向递归。

例题：Fibonacci数列，汉诺塔问题，快排

```java
	public int f(int n){
		if(n == 0){
			return 1;
		}else if(n == 1){
			return 4;
		}else{
			return 2*f(n - 1) + f(n - 2);
		}
	}
```

