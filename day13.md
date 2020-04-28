## day13 - Java面向对象

### 向下转型

`Person p2= new Man();`

`p2.earnMoney();` 不能调用子类Man()中的属性和方法

有了对象的多态性之后，内存中实际上是加载了子类特有的属性和方法的（因为new的是一个子类），但是由于变量声明为父类类型，导致编译时，只能调用父类中声明的属性和方法，子类特有的属性和方法不能调用。

调用子类特有的属性和方法：使用强制类型转换符（向下转型）

`Man m1 = (Man) p2;` 

<img src="C:\Users\lfrdw\AppData\Roaming\Typora\typora-user-images\image-20200221115339034.png" alt="image-20200221115339034" style="zoom:80%;" />



### 关键字instanceof 

a instanceof A: 判断对象a是否是A的实例，如果是则返回true

在使用向下类型转换时，需要先使用instanceof来判断是否是实例：

```
		//练习：
		//问题一：编译时通过，运行时不通过
		//举例一：
//		Person p3 = new Woman();
//		Man m3 = (Man)p3;
		//举例二：
//		Person p4 = new Person();
//		Man m4 = (Man)p4;

		
		//问题二：编译通过，运行时也通过
//		Object obj = new Woman();
//		Person p = (Person)obj;
		
		//问题三：编译不通过
//		Man m5 = new Woman();
		
//		String str = new Date();
		//编译能过，运行不能过
//		Object o = new Date();
//		String str1 = (String)o;
```



### 例题

子类继承父类：

- 若子类重写了父类**方法**，就意味着子类里定义的方法彻底覆盖了父类里的同名方法，系统将不可能把父类里的方法转移到子类中。编译看左边，运行看右边。

- 对于**实例变量(属性)**则不存在这样的现象，即使子类里定义了与父类完全相同的实例变量，这个实例变量依然不可能覆盖父类中定义的实例变量。编译运行都看左边。

![image-20200221233653845](C:\Users\lfrdw\AppData\Roaming\Typora\typora-user-images\image-20200221233653845.png)

求输出：分别为20，true，10，20。注意display的是子类的结果。



### 总结多态性

多态性总共两个要点：

- 定义：父类的引用指向子类的对象 Person p2 = new Man();
- 虚拟方法调用：调用子父类同名同参数的方法时，实际执行的是**子类重写父类的方法**



### Object类的使用

- 如果没有使用extends关键字，默认是java.lang.Object的子类。

- Object类是所有JAva类的根父类。

- Object类中的功能（属性和方法）具有通用性。
- 重点关注的方法：equals()对象比较 toString()对象打印

- 在垃圾回收之前会调用finalize()方法

  垃圾回收机制关键点：

  - 垃圾回收机制**只回收JVM堆内存里的对象空间**。

  - 对其他物理连接，比如数据库连接、输入流输出流、Socket连接无能为力

  - 现在的JVM有多种垃圾回收实现算法，表现各异。

  - 垃圾回收发生具有不可预知性，程序无法精确控制垃圾回收机制执行。

  - 可以将对象的引用变量设置为null，暗示垃圾回收机制可以回收该对象。

  - 程序员可以通过System.gc()或者Runtime.getRuntime().gc()来通知系统进行垃圾回收，会有
    一些效果，但是系统是否进行垃圾回收依然不确定。

  - 垃圾回收机制回收任何对象之前，总会先调用它的finalize方法（如果覆盖该方法，让一
    个新的引用变量重新引用该对象，则会重新激活对象）。

  - 永远不要主动调用某个对象的finalize方法，应该交给垃圾回收机制调用。

##### 面试题：

finalize, final, finally的区别：后两个是关键字，finalize是个方法

#### equals()

##### 面试题：

![image-20200222111534893](C:\Users\lfrdw\AppData\Roaming\Typora\typora-user-images\image-20200222111534893.png)

==可以比较不同的基本数据类型(**自动类型提升**)，比如比较char c=10; double d=10.0; 用==比较结果为true

==比较引用数据类型时，比较的是两个对象的地址值是否相同。

使用equals方法，**重写后的equals()方法**（eg String File Date等类）一般比较类中的属性的值是否都相等。

equals只能比较两个类（传入的是引用数据类型）**a.equals(b)**

如果**没有重写过equals()**，则默认调用的object中的equals()方法，和==是相同的。

- 重写equals()的方法

  ```java
  	//重写的原则：比较两个对象的实体内容(即：name和age)是否相同
  	//手动实现equals()的重写
  	@Override
  	public boolean equals(Object obj) {
  		System.out.println("Customer equals()....");
  		if (this == obj) {  //判断引用地址是不是一样，如果一样的话一定是相同的
              return true;
          }
  		
  		if(obj instanceof Customer){
  			Customer cust = (Customer)obj;  //向下转换
  			//比较两个对象的每个属性是否都相同
  			if(this.age == cust.age && this.name.equals(cust.name)){
  				return true;
  			}else{
  				return false;
  			}
              
  //			//或
  //			return this.age == cust.age && this.name.equals(cust.name);
  		}else{
  			return false;
  			
  		}
  ```

  - 也可以用Eclipse-Source中自动生成equals()方法



#### toString()

Object类中toString()的使用：

 * 当我们输出一个对象的引用时，实际上就是调用当前对象的toString()
 * **Object类中toString()的定义：**

   public String toString() {
      return getClass().getName() + "@" + Integer.toHexString(hashCode());
   }
 * 像String、Date、File、包装类等都重写了Object类中的toString()方法。使得在调用对象的toString()时，返回"实体内容"信息
 * 自定义类也可以重写toString()方法，当调用此方法时，返回对象的"实体内容"

```
	@Override
	public String toString() {
		return "Customer [name=" + name + ", age=" + age + "]";
	}
```





### 包装类的使用

### 包装类的使用

针对8种基本年数据类型定义相应的引用类型——包装类(封装类)

<img src="C:\Users\lfrdw\AppData\Roaming\Typora\typora-user-images\image-20200222115608499.png" alt="image-20200222115608499" style="zoom:67%;" />





### 单元测试方法

想要测试特定的某几行

Java中的JUnit单元测试

步骤：

1. 选中当前工程 - 右键选择：build path - add libraries - JUnit 4 - 下一步

2. 创建任何一个Java类，进行单元测试。**(如下文中的JUnitTest、PersonTest之类的类)**

   此时的Java类要求：① 此类是public的  ②此类提供公共的无参的构造器

3. 此类中声明单元测试方法。

   此时的单元测试方法：方法的权限是public,没有返回值，没有形参

4. 此单元测试方法上需要声明**注解**：@Test,并在单元测试类中导入：import org.junit.Test;

5. 声明好单元测试方法以后，就可以在方法体内测试相关的代码。

6. 写完代码以后，左键双击单元测试方法名，右键：run as - JUnit Test

- 在任何一个Java类中引入@Test就可以测试某一段代码

说明：

1.如果执行结果没有任何异常：绿条

2.如果执行结果出现异常：红条

```java
public class JUnitTest {
	
	int num = 10;
	
	@Test
	public void testEquals(){
		String s1 = "MM";
		String s2 = "MM";
		System.out.println(s1.equals(s2));
		//ClassCastException的异常
//		Object obj = new String("GG");
//		Date date = (Date)obj;
		
		System.out.println(num);
		show();
	}
	
	public void show(){
		num = 20;
		System.out.println("show()....");
	}
	
	@Test  //另一个单元测试，测试另一块代码
	public void testToString(){
		String s2 = "MM";
		System.out.println(s2.toString());
	}
}
```

- 基本数据类型转化为包装类——调用包装类的构造器：

```java
	@Test
	public void test1(){		
		int num1 = 10;
//		System.out.println(num1.toString());
		Integer in1 = new Integer(num1);
		System.out.println(in1.toString());
		
		Integer in2 = new Integer("123");
		System.out.println(in2.toString());
		
		//报异常
//		Integer in3 = new Integer("123abc");
//		System.out.println(in3.toString());
		
		Float f1 = new Float(12.3f);
		Float f2 = new Float("12.3");
		System.out.println(f1);
		System.out.println(f2);
		
		Boolean b1 = new Boolean(true);
		Boolean b2 = new Boolean("TrUe");
		System.out.println(b2);
		Boolean b3 = new Boolean("true123");
		System.out.println(b3);//false
		
		
		Order order = new Order();
		System.out.println(order.isMale);//false
		System.out.println(order.isFemale);//null
	}
```

- 包装类转化基本数据类型：调用xxxValue()

  (转化为基本数据类型后才能做加减乘除的运算)



- JDK 5.0特性：自动装箱和自动拆箱

  包装类和基本数据类型之间自动转换



- ```java
  	//String类型 --->基本数据类型、包装类：调用包装类的parseXxx(String s)
    	@Test
    	public void test5(){
    		String str1 = "123";
    		//错误的情况：
  //		int num1 = (int)str1;
  //		Integer in1 = (Integer)str1;  //没有子父类关系，不能强转
  		//可能会报NumberFormatException
  		int num2 = Integer.parseInt(str1);
  		System.out.println(num2 + 1);
  		
  		String str2 = "true1";
  		boolean b1 = Boolean.parseBoolean(str2);
  		System.out.println(b1);
  	}
  	
  	
  		//基本数据类型、包装类--->String类型：调用String重载的valueOf(Xxx xxx)
  	@Test
  	public void test4(){
  		
  		int num1 = 10;
  		//方式1：连接运算
  		String str1 = num1 + "";
  		//方式2：调用String的valueOf(Xxx xxx)
  		float f1 = 12.3f;
  		String str2 = String.valueOf(f1);//"12.3"
  		
  		Double d1 = new Double(12.4);
  		String str3 = String.valueOf(d1);
  		System.out.println(str2);
  		System.out.println(str3);//"12.4"
  		
  	}
  ```

  

#### 面试题（包装类）

![image-20200222232705907](C:\Users\lfrdw\AppData\Roaming\Typora\typora-user-images\image-20200222232705907.png)

第一个会有自动类型提升，三运算符要求冒号前后两个是一样的类型

![image-20200222232902160](C:\Users\lfrdw\AppData\Roaming\Typora\typora-user-images\image-20200222232902160.png)

第一个：ij都是地址

第二个：ij都不是地址

第三个：Integer内部定义了IntegerCache结构，IntegerCache中定义了Integer[], 保存了从-128~127范围的整数。如果我们使用自动装箱的方式，给Integer赋值的范围在-128~127范围内时，可以直接使用数组中的元素，不用再去new了。目的：提高效率