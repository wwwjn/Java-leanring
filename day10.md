## day10 - Java面向对象2

### 面向对象特征1：封装和隐藏

- 实际问题中，我们往往需要给属性赋值加入额外的限制条件。这个条件就不能在属性声明时体现，我们只能通过方法进行限制条件的添加。（比如：setLegs()）同时，我们需要避免用户再使用"对象.属性"的方式对属性进行赋值。则需要将属性声明为私有的(private).-->此时，针对于属性就体现了封装性。

- 封装性的体现：

  我们将类的**属性xxx私有化(private)**,同时，**提供公共的(public)方法来获取(getXxx)**和**设置(setXxx)此属性的值拓展**：封装性的体现：① 如上  ② 不对外暴露的私有的方法  ③ 单例模式   ...

- 在setXxx()方法中限制值的范围，超出范围时抛出一个异常-->控制private值的范围

  ```java
  	//提供关于属性age的get和set方法
  	public int getAge(){
  		return age;
  	}
  	public void setAge(int a){
  		age = a;
  	}
  ```

- 封装性的体现，需要权限修饰符来配合。
   * Java规定的4种权限（从小到大排列）：private、缺省、protected 、public 
   * 4种权限可以用来修饰类及类的内部结构：属性、方法、构造器、内部类
   * 具体的，4种权限都可以用来修饰类的内部结构：属性、方法、构造器、内部类
   * 修饰类的话，只能使用：缺省、public

- 总结封装性：Java提供了4种权限修饰符来修饰类及类的内部结构，体现类及类的内部结构在被调用时的可见性的大小。

<img src="C:\Users\lfrdw\AppData\Roaming\Typora\typora-user-images\image-20200219194424164.png" alt="image-20200219194424164" style="zoom:80%;" />



### 类的成员之三：构造器(构造方法) Constructor

- 任何一个类都有构造器，前两个成员是属性、方法

- ` Person p = new Person();`  new+构造器

- 如果没有显式的定义类的构造器，则系统默认提供一个空参的构造器

- 手动定义构造器：

  ```java
  	public Person(String n){
          name = n;
  		age = 15;
  		System.out.println("Person().....");
  	}
  ```

- 一个类中定义的多个构造器，彼此构成重载

 * 一旦我们显式的定义了类的构造器之后，系统就不再提供默认的空参构造器
 * 一个类中，至少会有一个构造器。



### JavaBean

是一种Java语言写成的可重用组件

<img src="C:\Users\lfrdw\AppData\Roaming\Typora\typora-user-images\image-20200219225948818.png" alt="image-20200219225948818" style="zoom:80%;" />



### UML类图

- \+表示 public 类型，\- 表示 private 类型，# 表示 protected 类型

+ 表示类的属性和方法



### 关键字this

在方法内需要用到**调用该方法的对象**时，就用this。this表示"当前对象"

**用this来区分属性和局部变量**

以下两种写法是等价的：

```java
//属性
private String name;
//方法（写法1）
public void setName(String n){
	name = n;
}
//写法2
public void setName(String name){
    this.name = name;
}
```

this关键字的使用：

1. this可以用来修饰、调用：属性、方法、构造器

2. this修饰属性和方法：

   this理解为：**当前对象**  或 **当前正在创建的对象**

   2.1   在类的**方法**中，我们可以使用**"this.属性"或"this.方法"**的方式，调用当前对象属性或方法。但是，通常情况下，我们都选择省略"this."。特殊情况下，如果方法的形参和类的属性同名时，我们必须显式的使用"this.变量"的方式，表明此变量是属性，而非形参。

   2.2   在类的**构造器**中，我们可以使用"this.属性"或"this.方法"的方式，调用当前正在创建的对象属性或方法。但是，通常情况下，我们都选择省略"this."。特殊情况下，如果构造器的形参和类的属性同名时，我们必须显式的使用"this.变量"的方式，表明此变量是属性，而非形参。

3. this调用构造器

   ① 我们在类的构造器中，可以显式的使用"this(形参列表)"方式，**调用本类中指定的其他构造器**

   ② 构造器中不能通过"this(形参列表)"方式调用自己

   ③ 如果一个类中有n个构造器，则最多有 n - 1构造器中使用了"this(形参列表)"

   ④ 规定："this(形参列表)"必须声明在当前构造器的首行

   ⑤ 构造器内部，最多只能声明一个"this(形参列表)"，用来调用其他的构造器

   ```java
   	public Person(){	
   		this.eat();
   		String info = "Person初始化时，需要考虑如下的1,2,3,4...(共40行代码)";
   		System.out.println(info);
   	}
   	
   	public Person(String name){
   		this();  //调用第一个Person()构造器
   		this.name = name;
   	}
   	
   	public Person(int age){
   		this();  //调用第一个Person()构造器
   		this.age = age;		
   	}
   	
   	public Person(String name,int age){
   		this(age);
   		this.name = name;
   		//Person初始化时，需要考虑如下的1,2,3,4...(共40行代码)
   	}
   	
   ```

   - 每个构造器都有相似的部分，为了避免冗余，可以在一个构造器中调用其他构造器。
   - 在上例中，第二和第三个构造器都调用了第一个构造器
   - 第四个构造器调用了第三个构造器



### 关键字：Package、import的使用

#### 一、package关键字的使用

1. 为了更好的实现项目中类的管理，提供包的概念

2. 使用package声明类或接口所属的包，声明在源文件的首行

3. 包，属于标识符，遵循标识符的命名规则、规范(xxxyyyzzz)、“见名知意”

4. 每"."一次，就代表一层文件目录。eg: com.atguigu.java2

补充：同一个包下，不能命名同名的接口、类。不同的包下，可以命名同名的接口、类。



#### 二、import关键字的使用

import:导入

 * 在源文件中显式的使用import结构导入指定包下的类、接口
 * import后接的位置在包的声明和类的声明之间
 * 如果需要导入多个结构，则并列写出即可
 * 可以使用" **import xxx.* **"的方式，表示可以导入xxx包下的所有结构
 * 如果使用的类或接口是java.lang包下定义的，则可以省略import结构
 * 如果使用的类或接口是本包下定义的，则可以省略import结构
 * 如果在源文件中，使用了不同包下的**同名的类**，则必须至少有一个类需要以全类名的方式显示。
 * 使用“**import xxx.* **"方式表明可以调用xxx包下的所有结构。但是如果使用的是xxx**子包**下的结构，则仍需要显式导入

 * import static:导入指定类或接口中的静态结构(属性或方法)。

  eg: import static java.lang.System. \* ;   out.println();
  import static java.lang.Math.* ;  PI

### MVC设计模式

不同于后面讲的23种设计模式

视图模型层——控制器层——数据模型层

view——controller——model

<img src="C:\Users\lfrdw\AppData\Roaming\Typora\typora-user-images\image-20200219232814703.png" alt="image-20200219232814703" style="zoom:80%;" />

<img src="C:\Users\lfrdw\AppData\Roaming\Typora\typora-user-images\image-20200219232853567.png" alt="image-20200219232853567" style="zoom:80%;" />