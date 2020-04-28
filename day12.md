## day12 - Java面向对象3

### Eclipse Debug实现

进入debug的透视图——step into(进入某个函数)——Step Over(执行下一行语句)

如果step into不能正常进入某个函数，是Debug Configuration中JRE位置设置不对



### 方法的重写Overwrite

![image-20200220201553040](C:\Users\lfrdw\AppData\Roaming\Typora\typora-user-images\image-20200220201553040.png)

- 子类中对父类继承来的方法进行改造
- 重写 必须要有**相同的方法名称和参数列表**；重载是同名不同参数

- 重写以后，创建子类对象并通过子类对象调用子父类中的同名同参数的方法时，实际执行的是子类的方法



- 关于返回值类型：
  - 父类被重写的方法的返回值类型是void，子类重写的方法的返回类型只能是void类型
  - 父类被重写的方法的返回值类型是A， 子类重写方法的返回值类型可以是A类或者A的子类
  - 父类被重写的方法的返回值类型是基本数据结构（double等），则子类重写的方法的返回值类型必须是相同的



### 四种权限修饰符

- protected：可以在**不同包**中的**子类**(带有Extend的)中看到该属性或者方法
- <img src="C:\Users\lfrdw\AppData\Roaming\Typora\typora-user-images\image-20200220214042197.png" alt="image-20200220214042197" style="zoom:80%;" />



### 关键字Super()

- eg： **Person()为父类，Student()为子类，都有一个int id的属性。在内存的堆空间中有两个id（对于属性来说不存在覆盖、重写的问题）**

**super关键字的使用**

1. super理解为：父类的

2. super可以用来调用：属性、方法、构造器

3. super的使用：调用属性和方法

   3.1 我们可以在子类的方法或构造器中。通过使用"super.属性"或"super.方法"的方式，显式的调用

   父类中声明的属性或方法。但是，通常情况下，我们习惯省略"super."

   3.2 特殊情况：当子类和父类中定义了同名的属性时，我们要想在子类中调用父类中声明的属性，则必须显式的使用"super.属性"的方式，表明调用的是父类中声明的属性。

   3.3 特殊情况：当子类重写了父类中的方法以后，我们想在子类的方法中调用父类中被重写的方法时，则必须显式的使用"super.方法"的方式，表明调用的是父类中被重写的方法。

4. super调用构造器

   4.1  我们可以在子类的构造器中显式的使用"super(形参列表)"的方式，调用父类中声明的指定的构造器 eg ` super(name,age)`调用父类中的构造器 

   4.2 "super(形参列表)"的使用，必须**声明在子类构造器的首行**！

   4.3 我们在类的构造器中，针对于"this(形参列表)"或"super(形参列表)"只能二选一，不能同时出现

   4.4 在构造器的首行，没有显式的声明"this(形参列表)"或"super(形参列表)"，则**默认调用的是父类中空参的构造器：super()**

   4.5 在类的多个构造器中，至少有一个类的构造器中 使用了"super(形参列表)"，调用父类中的构造器

**总结：**

- 如果是**this.属性**的话，会先在子类中寻找是否存在该属性，再在父类中寻找是否存在该属性
- 如果是**super.属性**的话，直接在父类中寻找该属性
- 想要调用**父类(直接父类和间接父类)中被重写的方法**，可以用类似super.eat();



### 子类对象实例化的过程——调用父类的构造器

 * 从结果上来看：（继承性）

   子类继承父类以后，就获取了父类中声明的属性或方法。

   创建子类的对象，在堆空间中，就会加载所有父类中声明的属性。

 * 从过程上来看：

   当我们通过子类的构造器创建子类对象时，我们一定会直接或间接的调用其父类的构造器，进而调用父类的父类的构造器，...直到调用了java.lang.Object类中空参的构造器为止。正因为加载过所有的父类的结构，所以才可以看到内存中有父类中的结构，子类对象才可以考虑进行调用。

**明确**：虽然创建子类对象时，调用了父类的构造器，但是自始至终**只创建过一个对象**，即为new的子类对象。

<img src="C:\Users\lfrdw\AppData\Roaming\Typora\typora-user-images\image-20200220233556500.png" alt="image-20200220233556500" style="zoom:67%;" />





### 面向对象的特征之三：多态性

```java
//对象的多态性：父类的引用指向子类的对象
Person p2 = new Man();
//Person p3 = new Woman();
//多态的使用：当调用子父类同名同参数的方法时，实际执行的是子类重写父类的方法 ---虚拟方法调用

p2.eat();
p2.walk();
```

- Man和Woman为Person的子类。左侧定义了一个父类的引用，右侧new的是一个子类的对象

- **虚拟方法调用：**调用子父类同名同参数的方法时，实际**执行的是子类重写父类的方法**

#### 面向对象特征之三：多态性

1. 理解多态性：可以理解为一个事物的多种形态。

2. 何为多态性：

   对象的多态性：父类的引用指向子类的对象（或子类的对象赋给父类的引用）

3. 多态的使用：虚拟方法调用

   有了对象的多态性以后，我们在编译期，只能调用父类中声明的方法，但在运行期，我们实际执行的是子类重写父类的方法。

   总结：编译，看左边；运行，看右边。

4. 多态性的使用前提：  ① 类的继承关系  ② 方法的重写

5. 对象的多态性，**只适用于方法，不适用于属性**（编译和运行都看左边）子父类有同名属性时

<img src="C:\Users\lfrdw\AppData\Roaming\Typora\typora-user-images\image-20200221110217128.png" alt="image-20200221110217128" style="zoom:80%;" />

- 也称为**虚方法**
- 多态性是一个**运行时行为**，不是编译时行为（在编译时无法确定其行为）
  - 重载，在方法调用之前，编译器就已经确定了所要调用的方法——早绑定
  - 多台，只有等到方法调用的时刻，解释运行器才会确定调用的具体方法——晚绑定

```
package com.atguigu.java5;
import java.util.Random;

//面试题：多态是编译时行为还是运行时行为？
//证明如下：
class Animal  { 
	protected void eat() {
		System.out.println("animal eat food");
	}
}

class Cat  extends Animal  { 
	protected void eat() {
		System.out.println("cat eat fish");
	}
}

class Dog  extends Animal  { 
	public void eat() {
		System.out.println("Dog eat bone");
	}
}

class Sheep  extends Animal  { 
	public void eat() {
		System.out.println("Sheep eat grass");
	} 
}

public class InterviewTest {
	public static Animal  getInstance(int key) {
		switch (key) {
		case 0:
			return new Cat ();
		case 1:
			return new Dog ();
		default:
			return new Sheep ();
		}
	}
	public static void main(String[] args) {
		int key = new Random().nextInt(3);
		System.out.println(key);
		Animal  animal = getInstance(key);		
		animal.eat();		 
	}
}
```

