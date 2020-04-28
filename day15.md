## day15 - Java面向对象

### 抽象类

将父类设计的非常抽象，以至于它没有具体的实例，这样的类叫做抽象类

- abstract关键字修饰一个类——抽象类
- abstract修饰方法——抽象方法
- 抽象类**不能实例化**
- 抽象类中一定有构造器（不直接声明也会有间接声明的），用于子类对象实例化
- 开发中需要提供重写后的子类

#### 抽象方法

- 抽象方法：没有方法体
- 包含抽象方法的类一定是抽象类。反之，**抽象类中可以没有抽象方法。**
- 若子类重写了父类中所有的抽象方法后，此子类方可实例化。若子类没有重写全部的抽象方法，仍为抽象类，需要使用abstract修饰

#### abstract使用的注意点

1. abstract不能用于修饰：属性、构造器
2. abstract不能用于修饰私有方法、静态方法、final的方法、final的类

#### 抽象类的匿名子类

- 匿名对象：` method1(new Worker());//非匿名的类匿名的对象`

- 匿名子类：

  ```java
  		//创建了一匿名子类的对象：p
  		Person p = new Person(){
  
  			@Override
  			public void eat() {
  				System.out.println("吃东西");
  			}
  
  			@Override
  			public void breath() {
  				System.out.println("好好呼吸");
  			}
  			
  		};
  		
  		method1(p);
  		System.out.println("********************");
  		//创建匿名子类的匿名对象
  		method1(new Person(){
  			@Override
  			public void eat() {
  				System.out.println("吃好吃东西");
  			}
  
  			@Override
  			public void breath() {
  				System.out.println("好好呼吸新鲜空气");
  			}
  		});
  ```



### 模板方法设计模式

抽象类作为多个子类的通用模板，子类在抽象类的基础上进行扩展、改造。

```java
/*
 * 抽象类的应用：模板方法的设计模式
 * 
 */
public class TemplateTest {
	public static void main(String[] args) {		
		SubTemplate t = new SubTemplate();		
		t.spendTime();
	}
}

abstract class Template{  //父类：抽象方法——模板
	//计算某段代码执行所需要花费的时间
	public void spendTime(){
		long start = System.currentTimeMillis();
		this.code();//不确定的部分、易变的部分
		long end = System.currentTimeMillis();
		System.out.println("花费的时间为：" + (end - start));
	}
	public abstract void code();
}

class SubTemplate extends Template{
	@Override
	public void code() {
		for(int i = 2;i <= 1000;i++){
			boolean isFlag = true;
			for(int j = 2;j <= Math.sqrt(i);j++){	
				if(i % j == 0){
					isFlag = false;
					break;
				}
			}
			if(isFlag){
				System.out.println(i);
			}
		}
	}
	
}

```

举例：写一个计算程序运行时间的方法，重写中间抽象的code就可以实现模板



### 接口

- 接口和类是两个并列的结构，一个类可以实现多个
- Java不支持多重继承，有了接口可以得到多重继承的结果（从多个类中派生出一个子类）

- 接口 就是规范，定义的是一组规则，体现了现实世界中“如果你是 要 则必须能 ......”的思想。 继承是一个 **是不是** 的关系，而接口实现则是 **能不能**的关系。

- 使用interface关键字来定义

  ```java
  interface Flyable{
  	
  	//全局常量
  	public static final int MAX_SPEED = 7900;//第一宇宙速度
  	int MIN_SPEED = 1;//省略了public static final
  	
  	//抽象方法
  	public abstract void fly();
  	//省略了public abstract
  	void stop();
  	
  	//Interfaces cannot have constructors
  //	public Flyable(){
  //		
  //	}
  }
  ```

- 接口中可以定义的成员：

  1. JDK7及以前：只能定义全局常量和抽象方法

   - 全局常量：**public static final**的。但是书写时，可以省略不写
   - 抽象方法：public abstract的

  2. JDK8：除了定义全局常量和抽象方法之外，还可以定义静态方法、默认方法（略）

- 接口不可以定义构造器！ ->接口不能实例化

- 接口的使用：接口通过**让类去实现(implements)的方式来使用**

  - 如果实现类覆盖了接口中的所有抽象方法，则此实现类就可以实例化

   *    如果实现类没有覆盖接口中所有的抽象方法，则此实现类仍为一个抽象类

  ```java
  abstract class Kite implements Flyable{
  	@Override
  	public void fly() {
          System.out.println("风筝飞");
  	}
      
  class Plane implements Flyable{
  	@Override
  	public void fly() {
  		System.out.println("通过引擎起飞");
  	}
  
  	@Override
  	public void stop() {
  		System.out.println("驾驶员减速停止");
  	}
  }
  ```

  

- Java类可以实现多个接口   --->弥补了Java单继承性的局限性

  格式：class AA extends BB implements CC,DD,EE

  ```java
  class Bullet extends Object implements Flyable,Attackable,CC{
  
  	@Override
  	public void attack() {
  		// TODO Auto-generated method stub
  		
  	}
  
  	@Override
  	public void fly() {
  		// TODO Auto-generated method stub
  		
  	}
  
  	@Override
  	public void stop() {
  		// TODO Auto-generated method stub
  		
  	}
  
  	@Override
  	public void method1() {
  		// TODO Auto-generated method stub
  		
  	}
  
  	@Override
  	public void method2() {
  		// TODO Auto-generated method stub
  		
  	}
  	
  }
  ```

  

- 接口与接口之间可以继承，而且可以多继承

  ```
  interface AA{
  	void method1();
  }
  interface BB{
  	
  	void method2();
  }
  
  interface CC extends AA,BB{
  	
  }
  ```

- 接口的具体使用——体现了多态性

  ```java
  class Computer{
      //接口体现多态性（看似写的是USB，实际使用的是Flash
  	public void transferData(USB usb){//USB usb = new Flash();  
  		usb.start();
  		System.out.println("具体传输数据的细节");
  		usb.stop();
  	}
  }
  
  interface USB{
  	//常量：定义了长、宽、最大最小的传输速度等	
  	void start();	
  	void stop();	
  }
  class Flash implements USB{
  	@Override
  	public void start() {
  		System.out.println("U盘开启工作");
  	}
  	@Override
  	public void stop() {
  		System.out.println("U盘结束工作");
  	}
  	
  }
  ```

  

- 接口实际上可以看做**一种规范**（eg 某个东西想要实现飞，就必须实现flyable的接口）

  

> 面试题：抽象类与接口有哪些异同
>
> 1. 抽象类与接口都无法实例化



### 接口的匿名实现类

接口的没有名字的实现类（直接写在接口使用的地方附近）

```java
public class USBTest {
	public static void main(String[] args) {		
		Computer com = new Computer();
		//1.创建了接口的非匿名实现类的非匿名对象
		Flash flash = new Flash();
		com.transferData(flash);		
		//2. 创建了接口的非匿名实现类的匿名对象
		com.transferData(new Printer());		
		//3. 创建了接口的匿名实现类的非匿名对象
		USB phone = new USB(){
			@Override
			public void start() {
				System.out.println("手机开始工作");
			}
			@Override
			public void stop() {
				System.out.println("手机结束工作");
			}			
		};
		com.transferData(phone);		
		//4. 创建了接口的匿名实现类的匿名对象		
		com.transferData(new USB(){
			@Override
			public void start() {
				System.out.println("mp3开始工作");
			}
			@Override
			public void stop() {
				System.out.println("mp3结束工作");
			}
		});
	}
}
```



### 接口的应用：代理模式

为其他对象提供一种代理以控制这个对象的访问

```java
/*
 * 接口的应用：代理模式
 * 
 */
public class NetWorkTest {
	public static void main(String[] args) {
		Server server = new Server();
//		server.browse();
		ProxyServer proxyServer = new ProxyServer(server);		
		proxyServer.browse();		
	}
}

interface NetWork{	
	public void browse();	
}
//被代理类
class Server implements NetWork{
	@Override
	public void browse() {
		System.out.println("真实的服务器访问网络");
	}
}

//代理类
class ProxyServer implements NetWork{	
	private NetWork work;	
	public ProxyServer(NetWork work){
		this.work = work;
	}	
	public void check(){
		System.out.println("联网之前的检查工作");
	}	
	@Override
	public void browse() {
		check();		
		work.browse();		
	}	
}
```

表面上是调用了代理类的browse()方法，实际上内部也调用了被代理类的browse()方法

在` ProxyServer proxyServer = new ProxyServer(server); `体现了接口的多态性



### 接口的应用：工厂模式

没有工厂时：

<img src="C:\Users\lfrdw\AppData\Roaming\Typora\typora-user-images\image-20200223203825965.png" alt="image-20200223203825965" style="zoom: 80%;" />

(包含23种设计模式中有的工厂方法模式、抽象工厂模式)

- 工厂模式：创建者和调用者分离 xxxFactory类

  <img src="C:\Users\lfrdw\AppData\Roaming\Typora\typora-user-images\image-20200223204013195.png" alt="image-20200223204013195" style="zoom:80%;" />



### Java8中关于接口的改进

可以为接口添加**静态方法**和**默认方法**

静态方法：使用static关键字修饰，只能通过**接口**直接调用静态方法，不能通过实现类对象来调用

默认方法：使用default关键字修饰，可以通过**实现类对象**来调用。如果实现类重写了默认方法，实际调用的是重写后的方法。

- 如果子类(或实现类)继承的父类和实现的接口中声明了同名同参数的方法， 那么子类在没有重写此方法的情况下，默认调用的是父类中同名同参数的方法（类优先原则）
  
- eg ` class SubClassA extends SuperClassA inplements InterfaceA`
  
- 若 一个接口中定义了一个默认方法，而另外一 个接口中也定义 了一个同名同参数的 方法（不管此方法 是否是默认方法），在实现类同时实现了这两个接口时，会出现：**接口冲突**。

- 如何在子类(或者实现类)的方法中调用父类、接口中被重写的方法

  super.method3(); //调用的是父类中声明的
  CompareA.super.method3();  //调用接口中的默认方法

```java
public class SubClassTest {
	public static void main(String[] args) {
		SubClass s = new SubClass();		
//		s.method1();
//		SubClass.method1();
		//知识点1：接口中定义的静态方法，只能通过接口来调用。
		CompareA.method1();
		//知识点2：通过实现类的对象，可以调用接口中的默认方法。
		//如果实现类重写了接口中的默认方法，调用时，仍然调用的是重写以后的方法
		s.method2();
		//知识点3：如果子类(或实现类)继承的父类和实现的接口中声明了同名同参数的默认方法，
		//那么子类在没有重写此方法的情况下，默认调用的是父类中的同名同参数的方法。-->类优先原则
		//知识点4：如果实现类实现了多个接口，而这多个接口中定义了同名同参数的默认方法，
		//那么在实现类没有重写此方法的情况下，报错。-->接口冲突。
		//这就需要我们必须在实现类中重写此方法
		s.method3();
	}	
}

class SubClass extends SuperClass implements CompareA,CompareB{
	
	public void method2(){
		System.out.println("SubClass：上海");
	}
	
	public void method3(){
		System.out.println("SubClass：深圳");
	}
	
	//知识点5：如何在子类(或实现类)的方法中调用父类、接口中被重写的方法
	public void myMethod(){
		method3();//调用自己定义的重写的方法
		super.method3();//调用的是父类中声明的
		//调用接口中的默认方法
		CompareA.super.method3();
		CompareB.super.method3();
	}
}

public interface CompareA {
	
	//静态方法
	public static void method1(){
		System.out.println("CompareA:北京");
	}
	//默认方法
	public default void method2(){
		System.out.println("CompareA：上海");
	}
	
	default void method3(){
		System.out.println("CompareA：上海");
	}
}

public interface CompareB {
	
	default void method3(){
		System.out.println("CompareB：上海");
	}
	
}

```



### 内部类

在开发中使用不多，但是看源码的时候可能有。

1. Java中允许将一个类A声明在另一个类B中，则类A就是内部类，类B称为外部类

2. 内部类的分类：成员内部类（静态、非静态）  vs 局部内部类(方法内、代码块内、构造器内)

3. 成员内部类：

   一方面，作为外部类的成员：

   - 调用外部类的结构
   - 可以被static修饰
   - 可以被4种不同的权限修饰

   另一方面，作为一个类：

   - 类内可以定义属性、方法、构造器等
   - 可以被final修饰，表示此类不能被继承。言外之意，不使用final，就可以被继承
   - 可以被abstract修饰

4. 关注如下的3个问题
   - 如何实例化成员内部类的对象
   - 如何在成员内部类中区分调用外部类的结构
   - 开发中局部内部类的使用  见下方代码块2

```java
public class InnerClassTest {
	public static void main(String[] args) {
		
		//创建Dog实例(静态的成员内部类):
		Person.Dog dog = new Person.Dog();
		dog.show();
		//创建Bird实例(非静态的成员内部类):
//		Person.Bird bird = new Person.Bird();//错误的
        //非静态需要先new Person()
		Person p = new Person();
		Person.Bird bird = p.new Bird();
		bird.sing();
		
		System.out.println();
		bird.display("黄鹂");
		
	}
}


class Person{
	
	String name = "小明";
	int age;
	
	public void eat(){
		System.out.println("人：吃饭");
	}
	
	
	//静态成员内部类
	static class Dog{
		String name;
		int age;
		
		public void show(){
			System.out.println("卡拉是条狗");
//			eat();
		}
		
	}
	//非静态成员内部类
	class Bird{
		String name = "杜鹃";
		
		public Bird(){
			
		}
		
		public void sing(){
			System.out.println("我是一只小小鸟");
			Person.this.eat();//调用外部类的非静态属性
			eat();
			System.out.println(age);
		}
		
		public void display(String name){
			System.out.println(name);//方法的形参
			System.out.println(this.name);//内部类的属性
			System.out.println(Person.this.name);//外部类的属性
		}
	}
	
	
	public void method(){
		//局部内部类
		class AA{
			
		}
	}
	
	{
		//局部内部类
		class BB{
			
		}
	}
	
	public Person(){
		//局部内部类
		class CC{
			
		}
	}	
}
```

```java
public class InnerClassTest1 {		
	//开发中很少见
	public void method(){
		//局部内部类
		class AA{
			
		}
	}		
	//返回一个实现了Comparable接口的类的对象
	public Comparable getComparable(){
		
		//创建一个实现了Comparable接口的类:局部内部类
		//方式一：
//		class MyComparable implements Comparable{
//
//			@Override
//			public int compareTo(Object o) {
//				return 0;
//			}
//			
//		}
//		
//		return new MyComparable();
		
		//方式二：
		return new Comparable(){
			@Override
			public int compareTo(Object o) {
				return 0;
			}			
		};		
	}	
}
```

