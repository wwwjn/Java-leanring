

## day05 - Java基本语法(3)

### 流程控制

#### 循环结构

- for循环：注意4是最后执行的

- **while循环**

  一、循环结构的4个要素
  ① 初始化条件
  ② 循环条件  --->是boolean类型
  ③ 循环体
  ④ 迭代条件

  -----

  ①
  while(②){
  	③;
  	④;  //如果丢掉4可能会死循环
  }

  执行过程：① - ② - ③ - ④ - ② - ③ - ④ - ... - ②

  

- **do-while循环**

  ①
  do{
  	③;
  	④;

  }while(②);

  执行过程：① - ③ - ④ - ② - ③ - ④ - ... - ②

  - 说明：
    1.do-while循环**至少会执行一次循环体**！
    2.开发中，使用for和while更多一些。较少使用do-while



### 嵌套循环

- 内层循环，外层循环
- 内层循环m次，外层循环n次，内层循环体共执行了n*m次

#### 练习：100以内所有质数的输出

```java
class PrimeNumberTest{
	public static void main(String[] args){
        //从2到n-1都不能整除这个数
        
        for(int i=2;i<=100;i++){
            boolean flag = true;  // 表示i是不是质数
            
            for(int j=2;j<=i-1;j++){  //判断是不是质数
                if(i%j == 0){
                    flag = false;
                }
            }
 			if(flag==true){
                System.out.println(i+"是整数");
        	}
        }
    }
}
```

```java
//优化1: 只对非质数的自然数是有优化效果的

class PrimeNumberTest{
	public static void main(String[] args){
        //从2到n-1都不能整除这个数
        long start= System.currentTimeMillins(); // 当前时间的毫秒数
        
        for(int i=2;i<=100;i++){
            boolean flag = true;  // 表示i是不是质数
            
            for(int j=2;j<=i-1;j++){  //判断是不是质数
                if(i%j == 0){
                    flag = false;
                    break; // 如果有一个不是，后面就不用算了
                }
            }
 			if(flag==true){
                System.out.println(i+"是整数");
        	}
        }
        long end= System.currentTimeMillins(); // 当前时间的毫秒数
        System.out.println("时间:" + (end-start)/1000);
    }
}
```

```java
//优化2: 分解因数是一对一对的，只需要计算到根号n
//节省了质数的优化时间  O(sqrt(n))

class PrimeNumberTest{
	public static void main(String[] args){
        //从2到n-1都不能整除这个数
        long start= System.currentTimeMillins(); // 当前时间的毫秒数
        
        for(int i=2;i<=100;i++){
   
            
            for(int j=2;j <= Math.sqrt(i);j++){  //判断是不是质数
                if(i%j == 0){
                    flag = false;
                    break; // 如果有一个不是，后面就不用算了
                }
            }
 			if(flag==true){
                System.out.println(i+"是整数");
        	}
        }
        long end= System.currentTimeMillins(); // 当前时间的毫秒数
        System.out.println("时间:" + (end-start)/1000);
    }
}
```





### 流程控制中的关键字

#### break：结束当前循环

- for / while 循环中都可**使用break来退出**，退出某一层循环

- { 

   break;

  }

  有多层嵌套循环时，break退出当前层{}的循环。

#### continue：结束当次循环

```java
		for(int i = 1;i <= 10;i++){
			if(i % 4 == 0){
				continue;  //123567910
				System.out.println("一句不可能被打印的话");
			}
			System.out.print(i);
		}
```

- 紧跟在continue后面的语句不能被执行。

```java
		label:for(int i = 1;i <= 4;i++){
		
			for(int j = 1;j <= 10;j++){
				
				if(j % 4 == 0){
					//break;//默认跳出包裹此关键字最近的一层循环。
					//continue;

					//break label;//结束指定标识的一层循环结构
					continue label;//结束指定标识的一层循环结构当次循环
				}
				
				System.out.print(j);
			}
			
			System.out.println();
		}
```

- `break label / continue label` 可以结束/继续指定某一层的循环

- 与return区别，return是用于结束方法的



- 输出质数的优化版本

```java
class PrimeNumberTest2 {
	public static void main(String[] args) {	
		int count = 0;//记录质数的个数
		//获取当前时间距离1970-01-01 00:00:00 的毫秒数
		long start = System.currentTimeMillis();
		label:for(int i = 2;i <= 100000;i++){//遍历100000以内的自然数	
			for(int j = 2;j <= Math.sqrt(i);j++){//j:被i去除
				
				if(i % j == 0){ //i被j除尽，说明不是质数
					continue label;
				}		
			}
			//能执行到此步骤的，都是质数
			count++;
		}
		//获取当前时间距离1970-01-01 00:00:00 的毫秒数
		long end = System.currentTimeMillis();
		System.out.println("质数的个数为：" + count);
		System.out.println("所花费的时间为：" + (end - start));

	}
}
```

