

## day08 - Java面向对象1

### 主线

1. Java类及类的成员：属性、方法、构造器；代码块、内部类
2. 面向对象的三大特征：封装性、继承性、多态性
3. 其他关键字：this super static final abstract interface package import等



- OOP（Object Oriented programming）

### 类和对象

类=抽象的概念；对象=实实在在的东西（某个类的实例化）

属性(field)=类中的成员变量； 方法(Method)=类中的成员方法

- 面向对象的设计重点是类的设计

- 类的设计其实就是类的成员的设计

```java
class Person{
	
	//属性
	String name;
	int age = 1;
	boolean isMale;
	
	//方法
	public void eat(){
		System.out.println("人可以吃饭");
	}
	
	public void sleep(){
		System.out.println("人可以睡觉");
	}
	
	public void talk(String language){  //可以带参数的方法
		System.out.println("人可以说话,使用的是：" + language);
	}
	
}
```



- 如果创建了一个类的多个对象，每个对象都有独立的一套类的属性（非static的）
- `Person p3=p1;` 将p3的指向p1，p3是一个指针，修改p3会导致p1一起变化。



#### JVM中的对象的内存解析

- 堆中存放对象实例，对象实例及数组都要在堆上分配内存。
- 栈（虚拟机栈）中存放局部变量，基本数据类型、对象引用(reference类型，是对象在堆内存的首地址)



#### 类中属性的使用

属性（成员变量） vs 局部变量

- 属性：定义在类的{}内

- 局部变量：声明在方法内、方法形参、代码块内、构造器形参、构造器内部的变量

  eg： language

  ```
  public void talk(String language){  //可以带参数的方法
  	System.out.println("人可以说话,使用的是：" + language);
  }
  ```

- 属性在声明时可以指明其权限、使用权限修饰符：private, public, protected, 缺省
- 属性的默认初始化值：整型浮点型字符型-0；引用数据类型-null



#### 类中方法的声明与使用

##### 声明 

` public void sleep(int hour)` void 表示该方法没有返回值

` public String getName(){}` String表示有返回值

##### 可能用的关键词

static final abstract可能会修饰方法，后面讲

##### 权限修饰符

共四种 （讲解封装性的时候再讲）

##### 返回值

return和 函数定义时的类型一定得相同

如果没有返回值，可以使用` return;`

##### 形参列表

方法可以声明0或1个或多个形参

##### return

return使用在方法体中，用于结束一个方法

使用return xxx来返回相应的返回值

##### 注意

在方法的使用中，可以调用当前类的**属性**或**方法**。

不能在一个方法中再定义另一个方法。



#### 应用举例

```java
package com.atguigu.exer;
/*
 * 4. 对象数组题目：
定义类Student，包含三个属性：学号number(int)，年级state(int)，成绩score(int)。
 创建20个学生对象，学号为1到20，年级和成绩都由随机数确定。
问题一：打印出3年级(state值为3）的学生信息。
问题二：使用冒泡排序按学生成绩排序，并遍历所有学生信息

提示：
1) 生成随机数：Math.random()，返回值类型double;  
2) 四舍五入取整：Math.round(double d)，返回值类型long。
 * 
 * 
 * 此代码是对StudentTest.java的改进：将操作数组的功能封装到方法中。
 * 
 */
public class StudentTest1 {
	public static void main(String[] args) {
		
		//声明Student类型的数组
		Student1[] stus = new Student1[20];  
		
		for(int i = 0;i < stus.length;i++){
			//给数组元素赋值
			stus[i] = new Student1();
			//给Student对象的属性赋值
			stus[i].number = (i + 1);
			//年级：[1,6]
			stus[i].state = (int)(Math.random() * (6 - 1 + 1) + 1);
			//成绩：[0,100]
			stus[i].score = (int)(Math.random() * (100 - 0 + 1));
		}
		
		StudentTest1 test = new StudentTest1();
		
		//遍历学生数组
		test.print(stus);
		
		System.out.println("********************");
		
		//问题一：打印出3年级(state值为3）的学生信息。
		test.searchState(stus, 3);
		
		System.out.println("********************");
		
		//问题二：使用冒泡排序按学生成绩排序，并遍历所有学生信息
		test.sort(stus);
		
		//遍历学生数组
		test.print(stus);
		
	}
	
	/**
	 * 
	 * @Description  遍历Student1[]数组的操作
	 * @author shkstart
	 * @date 2019年1月15日下午5:10:19
	 * @param stus
	 */
	public void print(Student1[] stus){
		for(int i = 0;i <stus.length;i++){
			System.out.println(stus[i].info());
		}
	}
	/**
	 * 
	 * @Description 查找Stduent数组中指定年级的学生信息
	 * @author shkstart
	 * @date 2019年1月15日下午5:08:08
	 * @param stus 要查找的数组
	 * @param state 要找的年级
	 */
	public void searchState(Student1[] stus,int state){
		for(int i = 0;i <stus.length;i++){
			if(stus[i].state == state){
				System.out.println(stus[i].info());
			}
		}
	}
	
	/**
	 * 
	 * @Description 给Student1数组冒泡排序
	 * @author shkstart
	 * @date 2019年1月15日下午5:09:46
	 * @param stus
	 */
	public void sort(Student1[] stus){
		for(int i = 0;i < stus.length - 1;i++){
			for(int j = 0;j < stus.length - 1 - i;j++){
				if(stus[j].score > stus[j + 1].score){
					//如果需要换序，交换的是数组的元素：Student对象！！！
					Student1 temp = stus[j];
					stus[j] = stus[j + 1];
					stus[j + 1] = temp;
				}
			}
		}
	}
}

class Student1{
	int number;//学号
	int state;//年级
	int score;//成绩
	
	//显示学生信息的方法
	public String info(){
		return "学号：" + number + ",年级：" + state + ",成绩：" + score;
	}
}

```

