## day16 - Java异常处理

### 异常

程序性中发生的不正常情况（不包括语法错误和逻辑错误）

Error：比如堆溢出和栈溢出（暂时不考虑）

异常：因编程错误或偶然的外在因素导致的一般性问题，使用针对性的代码进行处理

- 可以分为编译时异常、运行时异常
- 下图蓝色就是编译时异常，红色是运行时异常

<img src="C:\Users\lfrdw\AppData\Roaming\Typora\typora-user-images\image-20200224135001923.png" alt="image-20200224135001923" style="zoom: 50%;" />

#### Java异常体系结构

java.lang.Error:

java.lang.Excepetion: 可以进行异常的处理

- 编译时异常（checked）
  - IOException
    - FileNotFoundException
  - ClassNotFoundException
- 运行时异常（Unchecked）
  - NullPointerException
  - ArrayIndexOutOfBoundsException
  - ClassCastExcepetion
  - NumberFormatException
  - InputMismatchException
  - ArithmaticException



#### 常见异常举例

- NullPointerException：

  `int[] arr =null; System.out.println(arr[3]);`

  `String str="abc"; str= null; System.out.println(str.charAr(0));`

- ArrayIndexOurOfBoundsException:

  `int[] arr=new int[10];System.out.println(arr[10]);`

  `String str="abc"; System.out.println(str.charAr(3));`

- ClassCastException类型转换错误

  ` Object obj = new Date(); String str = (String)obj;`

- NumFormatException

  `String str="abc"; int num= Integer.parseInt(str);`

- InputMismatchException:

  一个需要控制台输入，并把输入转化为integer的函数，如果输入abc

- ArithmeticExcpetion:

  ![image-20200224142420726](C:\Users\lfrdw\AppData\Roaming\Typora\typora-user-images\image-20200224142420726.png)

  比如除0

- 编译时异常举例:（无法通过编译）

  IOException: 文件的输入流

  ![image-20200224144239944](C:\Users\lfrdw\AppData\Roaming\Typora\typora-user-images\image-20200224144239944.png)



### Java异常处理机制——抓抛模型

抛——程序在正常执行额过程中，一旦出现异常，就会在异常代码处生成一个对应异常类的对象，并将此对象抛出。一旦抛出异常后，其后的代码就不再执行。

抓——抓住抛出的异常，异常的处理方式（两种方式）

#### try-catch-finally

```java
try{
 		//可能出现异常的代码

}catch(异常类型1 变量名1){
		//处理异常的方式1
}catch(异常类型2 变量名2){
		//处理异常的方式2
}catch(异常类型3 变量名3){
		//处理异常的方式3
}
....
finally{
	 //一定会执行的代码
}
```

- finally是可选的
- 用try把可能出现异常的代码包裹起来
- catch中的异常类型如果没有子父类关系，则谁声明在上，谁声明在下无所谓；catch中的**异常类型如果满足子父类关系**，则要求子类一定声明在父类的上面。否则，报错
- 常用的异常对象处理的方式： ① **String  getMessage()**    ② **printStackTrace()**更全
- 在try{}结构中声明的变量，再出了try结构以后，就**不能再被调用**
- 使用try-catch-finally处理编译时异常，是得程序在编译时就不再报错，但是运行时仍可能报错。相当于我们使用try-catch-finally将一个**编译时可能出现的异常，延迟到运行时出现。**
- 开发中，由于运行时异常比较常见，所以我们通常就**不针对运行时异常编写**try-catch-finally了。针对于编译时异常，我们说一定要考虑异常的处理。
- 运行时异常，处理和不处理结果相近（一般不做异常处理，应该回来改代码）运行时异常本身也不报错（报的是exception)。编译时异常如果不处理的话就无法通过编译，所以一定要处理 :star:

##### 对finally的说明

- finally是可选的

- finally中声明的是一定会被执行的代码。即使catch中又出现异常了，try中有return语句，catch中有return语句等情况。(相对的，直接在try-catch结构外部写的代码不一定会执行)

- 像**数据库连接、输入输出流、网络编程Socket等资源，JVM是不能自动的回收的**，我们需要自己手动的进行资源的释放。此时的资源释放，就需要声明在finally中。

- finally在抛出throw之前执行

  

#### throws+异常类型

throws：抛出异常，让上一级（调用者）处理

```java
	public static void method3(){
		try {
			method2();
		} catch (IOException e) {
			e.printStackTrace();
		}
	}
		
	public static void method2() throws IOException{
		method1();
	}

	public static void method1() throws FileNotFoundException,IOException{
		File file = new File("hello1.txt");
		FileInputStream fis = new FileInputStream(file);		
		int data = fis.read();
		while(data != -1){
			System.out.print((char)data);
			data = fis.read();
		}		
		fis.close();		
		System.out.println("hahaha!");
	}
```

1. "throws + 异常类型"写在方法的声明处。指明此方法执行时，可能会抛出的异常类型。

   一旦当方法体执行时，出现异常，仍会在异常代码处生成一个异常类的对象，此对象满足throws后异常类型时，就会被抛出。异常代码后续的代码，就不再执行！

2. 体会：try-catch-finally:真正的将异常给处理掉了。

   throws的方式只是将异常**抛给了方法的调用者**。  并没有真正将异常处理掉。  

3. 开发中如何选择使用try-catch-finally 还是使用throws？

   - 如果父类中被重写的方法没有throws方式处理异常，则子类重写的方法也不能使用throws，意味着如果子类重写的方法中有异常，必须使用try-catch-finally方式处理。

   -  执行的方法中，先后又调用了另外的几个方法，这几个方法是递进关系（一个方法算出的结果，让另一个方法来使用）执行的。我们建议这几个方法使用throws的方式进行处理。而执行的方法a可以考虑使用try-catch-finally方式进行处理。

- 方法重写的规则之一：子类重写的方法抛出的异常类型不大于父类被重写的方法抛出的异常类型。
- 如果父类的方法中没有使用throws抛异常，那么子类重写的方法也不能用throws



### 手动抛出异常

手动生成一个异常对象，并抛出

```java
class Student{
	
	private int id;
	
	public void regist(int id) throws Exception {
		if(id > 0){
			this.id = id;
		}else{
//			System.out.println("您输入的数据非法！");
			//手动抛出异常对象
//或			throw new RuntimeException("您输入的数据非法！");
            //throw Exception时需要搭配 throws Exception
//或			throw new Exception("您输入的数据非法！");
			throw new MyException("不能输入负数");
			//错误的
//			throw new String("不能输入负数");
		}		
	}
	@Override
	public String toString() {
		return "Student [id=" + id + "]";
	}		
}
//自定义异常类
public class MyException extends Exception{	
	static final long serialVersionUID = -7034897193246939L;	
	public MyException(){		
	}	
	public MyException(String msg){  //msg是父类已有的属性
		super(msg);
	}
}

```

如何自定义异常类？

 * 继承于现有的异常结构：RuntimeException 、Exception
 * 提供全局常量：serialVersionUID
 * 提供重载的构造器



### 用户自定义异常类

如何自定义异常类：（例子见上）

- 继承于现有的异常结构，RuntimeError、Exception
- 提供全局常量，serialVersionUID（类似于序列号）
- 只有异常类的对象才可以throw()



![image-20200224205113454](C:\Users\lfrdw\AppData\Roaming\Typora\typora-user-images\image-20200224205113454.png)

### 练习

#### 面试题

throws和throw的区别：

- throw是生成异常对象的，表示抛出一个异常类的对象，生成异常对象的过程，声明在方法体内。
- throws属于异常处理的一种方式，声明在方法的声明处