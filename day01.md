## day0-Java编程基础

- Java跨平台性：运行在不同的JVM上，不同操作系统有不同的JVM

- JDK：Java开发工具包（开发，编写）

  JRE：Java Runtime Environment （运行需要）

  JVM：Java虚拟机，JRE=JVM+Java SE标准类库

  IDE：Intelligent development Environment: 集成开发环境

- 第一个代码段：

  ```java
  public class HelloJava{
      public static void main(String[] args){
          System.out.println("Hello World!");
      }
  }
  ```

- 总结第一个代码段

  - Java 源文件以“ java ”为扩展名。源文件的基本组成部分是类 class 如本例中的HelloJava类。

  - Java 应用程序的执行入口是 **main() 方法**，它有**固定的书写格式**public static void main(String[] args)

  - Java 语言严格区分大小写。

  - Java 方法由一条条语句构成，每个语句以“ “;”结束。

  - 大括号都是成对出现的， 缺一不可

  - 一个源文件中最多**只能有一个public 类**。其它类的个数不限，如果源文件包含一个 public 类，则文件名必须按该类名命名。

    

- 编译： javac xxx.java
  
  - 如果源文件中有多个类会编译生成多个.class 文件
- 运行：java xxx(类名) 



- 注释：

  - 单行注释
  - 多行注释
  - 文档注释（生成说明文档）

  ![image-20200214110433029](C:\Users\lfrdw\AppData\Roaming\Typora\typora-user-images\image-20200214110433029.png)

