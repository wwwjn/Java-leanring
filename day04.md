## day04 - Java基本语法(2)

### 流程控制

- 分支结构

- if-else结构

  ```java
  if(条件1){
  	执行语句1;
      System.out.println("check");
  }
  else if(条件2){
  	执行语句2;
  }
  else{
  	执行语句3;
  }
  ```

- switch-case结构

  ① 根据switch表达式中的值，依次匹配各个case中的常量。一旦匹配成功，则进入相应case结构中，调用其执行语句。 当调用完执行语句以后，则仍然继续向下执行其他case结构中的执行语句，直到遇到break关键字或此switch-case结构末尾结束为止。

  ②遇到break才会退出

  ③ switch结构中的表达式，只能是如下的6种数据类型之一：
     **byte 、short、char、int、枚举类型(JDK5.0新增)、String类型(JDK7.0新增)**

  ​	switch的表达式**不能是boolean**。

  ```java
  class SwitchCaseTest {
  	public static void main(String[] args) {
  		
  		int number = 5;
  		switch(number){
  		case 0:
  			System.out.println("zero");
  			break;
  		case 1:
  			System.out.println("one");
  			break;
  		case 2:
  			System.out.println("two");
  			break;
  		case 3:
  			System.out.println("three");
  			break;
  		default:
  			System.out.println("other");
  			//break;
  		}
  ```

  

- 循环结构

  - for循环：注意4是最后执行的
  
    for(①;②;④){
    	③
    }
  
    执行过程：① - ② - ③ - ④ - ② - ③ - ④ - ... - ②
  
    ```java
    		for(int i = 1;i <= 5;i++){//i:1,2,3,4,5
    			System.out.println("Hello World!");
    		}
    
    		//练习：
    		int num = 1;
    		for(System.out.print('a');num <= 3;System.out.print('c'),num++){
    			System.out.print('b');
    		}
    		//输出结果：abcbcbc
    ```
  
    初始条件：System.out.print('a')
  
    迭代部分：System.out.print("c"),num++
  
    
  
  - while循环
  
    
  
  - do-while循环
  
  

### 从控制台/键盘获取不同类型变量

- 使用Scanner类：导入包——实例化——使用nextxxx()方法

  ```java
  /*
  如何从键盘获取不同类型的变量：需要使用Scanner类
  
  具体实现步骤：
  1.导包：import java.util.Scanner;
  2.Scanner的实例化:Scanner scan = new Scanner(System.in);
  3.调用Scanner类的相关方法（next() / nextXxx()），来获取指定类型的变量
  
  注意：
  需要根据相应的方法，来输入指定类型的值。如果输入的数据类型与要求的类型不匹配时，会报异常：InputMisMatchException
  导致程序终止。
  */
  //1.导包：import java.util.Scanner;
  import java.util.Scanner;
  
  class ScannerTest{
  	public static void main(String[] args){
  		//2.Scanner的实例化
  		Scanner scan = new Scanner(System.in);
  		
  		//3.调用Scanner类的相关方法
  		System.out.println("请输入你的姓名：");
  		String name = scan.next();
  		System.out.println(name);
  
  		System.out.println("请输入你的芳龄：");
  		int age = scan.nextInt();
  		System.out.println(age);
  
  		System.out.println("请输入你的体重：");
  		double weight = scan.nextDouble();
  		System.out.println(weight);
  
  		System.out.println("你是否相中我了呢？(true/false)");
  		boolean isLove = scan.nextBoolean();
  		System.out.println(isLove);
  
  		//对于char型的获取，Scanner没有提供相关的方法。只能获取一个字符串
  		System.out.println("请输入你的性别：(男/女)");
  		String gender = scan.next();//"男"
  		char genderChar = gender.charAt(0);//获取索引为0位置上的字符
  		System.out.println(genderChar);
  	}
  }
  ```

  

