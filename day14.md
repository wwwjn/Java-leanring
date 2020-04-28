## day13 - Java面向对象

### 关键字static

#### static修饰属性

- 希望无论new产生了个多少对象，某些特定的数据在内存空间中只有一份。如所有的中国人都有个国家名称，每个中国人都共享这个国家名称。

- 使用static修饰的变量不归某一个对象所有，是共享的。不用造对象，直接调用

  <img src="C:\Users\lfrdw\AppData\Roaming\Typora\typora-user-images\image-20200223100733081.png" alt="image-20200223100733081" style="zoom:80%;" />

- **实例变量**：我们创建了类的多个对象，每个对象都独立的拥有一套类中的非静态属性。当修改其中一个对象中的非静态属性时，不会导致其他对象中同样的属性值的修改。

 *       **静态变量**：我们创建了类的多个对象，多个对象共享同一个静态变量。当通过某一个对象修改静态变量时，会导致其他对象调用此静态变量时，是修改过了的。

- 其他说明：
  - 实例变量随着对象创建而加载，静态变量随着类的加载而加载。（静态变量的加载更早）
  - 可以通过“类.静态变量”调用
  - 由于类只会加载一次，静态变量在内存中只会存在一份（存在方法区的静态域中）
  - ![image-20200223101821720](C:\Users\lfrdw\AppData\Roaming\Typora\typora-user-images\image-20200223101821720.png)

- 静态结构举例：System.out   Math.PI

- 内存解析：

  ![image-20200223102044833](C:\Users\lfrdw\AppData\Roaming\Typora\typora-user-images\image-20200223102044833.png)

  - 栈：存放局部变量
  - 堆：new出来的结构（eg 对象、数组）
  - 方法区：类的加载信息，静态域，常量池

#### static修饰方法

- **随着类的加载而加载**，可以通过"**类.静态方法**"的方式进行调用（不用造对象）
- ![image-20200223102627554](C:\Users\lfrdw\AppData\Roaming\Typora\typora-user-images\image-20200223102627554.png)

-  **静态方法中能调用静态的方法和属性**，非静态方法中静态和非静态的方法和属性都能调用

  （主要原因是静态和非静态生命周期不同）



#### static注意点

在静态的方法中，不能使用this关键字、super关键字

静态属性、静态方法的使用，都从**生命周期**的角度去理解



#### 什么时候声明为static

- 属性：被多个对象共用时，不随着对象的不同而不同；类中的常量通常声明为static

- 方法：封装静态属性的方法，通常声明为static；工具类（Math，Array，Collections)中的方法，声明为static（因为不用先造对象了）



### 单例设计模式（Singleton）

设计模式：优选的代码结构、编程风格、解决问题的思考方式“套路”

单例：保证在整个软件系统中，某个类只能存在一个对象实例

#### 实现方法：

- 饿汉式实现

  1. 私有化类的构造器

  2. 内部创建一个类的对象

  3. 提供公共的方法，返回创建的类的对象

  

- 懒汉式实现

  1. 私有化构造器

  2. 声明当前类对象，没有初始化

  3. 声明public，static的返回当前类对象的方法（注意判断是否已经创造过对象）

  4. 此实例也必须声明为static

     <img src="C:\Users\lfrdw\AppData\Roaming\Typora\typora-user-images\image-20200223105344739.png" alt="image-20200223105344739" style="zoom:60%;" />

- 区别

  饿汉式：天然是线程安全的；但是对象加载时间过长

  懒汉式：延迟对象的创建；但是存在线程安全问题-->后面讲到多线程问题时可以修复

#### 单例模式的优点

减少了系统性能开销

#### 应用场景

![image-20200223110103521](C:\Users\lfrdw\AppData\Roaming\Typora\typora-user-images\image-20200223110103521.png)



### main方法的再次说明

public static void main(String[] args){

}

main()方法的使用说明：

 * main()方法作为程序的入口

 * main()方法也是一个普通的静态方法

 * main()方法可以作为我们与控制台交互的方式。（之前：使用Scanner）【main方法的形参】

   args作为控制台的输入： java MainDemo 80 90 23



### 代码块（初始化块）

- 只能使用static修饰

- 只有一个大括号

- 通常用于初始化类、对象

![image-20200223113218623](C:\Users\lfrdw\AppData\Roaming\Typora\typora-user-images\image-20200223113218623.png) 

- 静态代码块内只能调用静态的属性和方法，非静态代码块都可以调用

- 静态代码块使用示例：可能用与单例模式中只执行1次的步骤

#### 代码块、构造器的执行顺序例题：

```java
//总结：由父及子，静态先行
class Root{
	static{
		System.out.println("Root的静态初始化块");
	}
	{
		System.out.println("Root的普通初始化块");
	}
	public Root(){
		super();
		System.out.println("Root的无参数的构造器");
	}
}
class Mid extends Root{
	static{
		System.out.println("Mid的静态初始化块");
	}
	{
		System.out.println("Mid的普通初始化块");
	}
	public Mid(){
		super();
		System.out.println("Mid的无参数的构造器");
	}
	public Mid(String msg){
		//通过this调用同一类中重载的构造器
		this();
		System.out.println("Mid的带参数构造器，其参数值："
			+ msg);
	}
}
class Leaf extends Mid{
	static{
		System.out.println("Leaf的静态初始化块");
	}
	{
		System.out.println("Leaf的普通初始化块");
	}	
	public Leaf(){
		//通过super调用父类中有一个字符串参数的构造器
		super("尚硅谷");
		System.out.println("Leaf的构造器");
	}
}
public class LeafTest{
	public static void main(String[] args){
		new Leaf(); 
		System.out.println();
		new Leaf();
	}
}

```

先执行静态代码块，然后new对象的时候再执行普通代码块-->构造器



#### 代码块+变量赋值的顺序

![image-20200223151814892](C:\Users\lfrdw\AppData\Roaming\Typora\typora-user-images\image-20200223151814892.png)

- 初始化块=代码块



### 关键字 final

- final可以用于修饰：类、方法、变量。
- final修饰类：表示该结构不能被其他类继承（如String System StringBuffer）

- final修饰一个方法：表明此方法不可以被重写

- final修饰一个变量：此时修饰的“变量”其实为一个常量，不能再改（有名字的常量）

  - final修饰一个属性：final修饰属性，可以考虑赋值的位置有——显式初始化、代码块中初始化、构造器初始化（如果有多个构造器，需要对某一属性初始化，每个构造器均需要对这个属性初始化）

  - final修饰一个局部变量：

    final修饰一个形参：当我们调用此方法时，给变量形参赋一个实参，一旦赋值以后，方法内只能调用，不能进行重新赋值

- static final ：用于修饰方法、全局变量                                   

- 在一般工作中，final修饰方法很少见，final修饰常量很多见

