## day02-Java编程基础

### Java中的各种类型变量: （8种数据类型）

- 加上static表明是类变量，不加的是实例变量

```java
class VariableTest1 {
	public static void main(String[] args) {
		//1. 整型：byte(1字节=8bit) \ short(2字节) \ int(4字节) \ long(8字节)
		//① byte范围：-128 ~ 127
		//
		byte b1 = 12;
		byte b2 = -128;
		//b2 = 128;//编译不通过
		System.out.println(b1);
		System.out.println(b2);
		// ② 声明long型变量，必须以"l"或"L"结尾
		// ③ 通常，定义整型变量时，使用int型。
		short s1 = 128;
		int i1 = 1234;
		long l1 = 3414234324L;
		System.out.println(l1);

		//2. 浮点型：float(4字节) \ double(8字节)
		//① 浮点型，表示带小数点的数值
		//② float表示数值的范围比long还大

		double d1 = 123.3;
		System.out.println(d1 + 1);
		//③ 定义float类型变量时，变量要以"f"或"F"结尾
		float f1 = 12.3F;
		System.out.println(f1);
		//④ 通常，定义浮点型变量时，使用double型。

		//3. 字符型：char (1字符=2字节)
		//① 定义char型变量，通常使用一对'',内部只能写一个字符
		char c1 = 'a';
		//编译不通过
		//c1 = 'AB';
		System.out.println(c1);

		char c2 = '1';
		char c3 = '中';
		char c4 = 'ス';
		System.out.println(c2);
		System.out.println(c3);
		System.out.println(c4);

		//② 表示方式：1.声明一个字符 2.转义字符 3.直接使用 Unicode 值来表示字符型常量
		char c5 = '\n';//换行符
		c5 = '\t';//制表符
		System.out.print("hello" + c5);
		System.out.println("world");

		char c6 = '\u0043';//Unicode值
		System.out.println(c6);

		//4.布尔型：boolean
		//① 只能取两个值之一：true 、 false
		//② 常常在条件判断、循环结构中使用
		boolean bb1 = true;
		System.out.println(bb1);

		boolean isMarried = true;
		if(isMarried){
			System.out.println("你就不能参加\"单身\"party了！\n很遗憾");
		}else{
			System.out.println("你可以多谈谈女朋友！");
		}

	}
}
```

- char类型：

  \n 换行； \t 制表符 Tab； \可以用于转义

  Java 中的所有字符都使用 Unicode 编码，故一个字符char可以存储一个字母，一个汉字，或其他书面语的一个字符。

- long类型：

  **long的存储范围比float存储的范围小**；

  定义long变量以L结尾。

- float类型：

  定义float类型以F结尾。

  

### Java中各种变量间的计算

- 自动类型提升：
  当容量小的数据类型的变量与容量大的数据类型的变量做运算时，结果自动提升为容量大的数据类型。 

  **byte 、char 、short --> int --> long --> float --> double** 

  - “容量大小”表示数的范围的大小，eg float容量大于long的大小

  - 特别的：**当byte、char、short三种类型的变量做运算时，结果为int型**

- 强制类型转换：

  - 使用`( )`强制类型转换，可能有精度损失

  ```java
  double d1 = 12.9;
  int i1 = (int)d1;//截断操作,四舍五入
  
  int i2 = 128;
  byte b = (byte)i2;  //超过了该类型能存储的数字的范围，转为二进制考虑
  System.out.println(b);//-128
  ```

  - 超过了该类型能存储的数字的范围，转为二进制考虑



### String

- String不是基本数据类型，引用数据类型
- String可以和8种基本数据类型做运算，且**只能是连接运算**：+
- 一个字符串可以串接另一个字符串，也可以直接串接其他类型的数据。例如：
  str= str + “xyz” ;
  int n = 100;
  str = str + n



### 进制及转换

![image-20200214114927652](C:\Users\lfrdw\AppData\Roaming\Typora\typora-user-images\image-20200214114927652.png)