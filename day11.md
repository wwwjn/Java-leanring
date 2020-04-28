## day11 - Java面向对象3

### Eclipse快捷键

Eclipse中的快捷键： 

1.**补全代码的声明：alt + /**

2.快速修复: ctrl + 1  

3.批量导包：ctrl + shift + o

4.使用单行注释：ctrl + /

5.使用多行注释： ctrl + shift + /   

6.取消多行注释：ctrl + shift + \

7.复制指定行的代码：ctrl + alt + down 或 ctrl + alt + up

8.删除指定行的代码：ctrl + d

9.上下移动代码：alt + up  或 alt + down

10.切换到下一行代码空位：shift + enter

11.切换到上一行代码空位：ctrl + shift + enter

12.**如何查看源码**：ctrl + 选中指定的结构   或  ctrl + shift + t

13.退回到前一个编辑的页面：alt + left 

14.进入到下一个编辑的页面(针对于上面那条来说的)：alt + right

15.光标选中指定的类，查看继承树结构：ctrl + t

16.复制代码： ctrl + c

17.撤销： ctrl + z

18.反撤销： ctrl + y

19.剪切：ctrl + x 

20.粘贴：ctrl + v

21.保存： ctrl + s

22.全选：ctrl + a

23.格式化代码： ctrl + shift + f

24.选中数行，整体往后移动：tab

25.选中数行，整体往前移动：shift + tab

26.在当前类中，显示类结构，并支持搜索指定的方法、属性等：ctrl + o

27.批量修改指定的变量名、方法名、类名等：alt + shift + r

28.选中的结构的大小写的切换：变成大写： ctrl + shift + x

29.选中的结构的大小写的切换：变成小写：ctrl + shift + y

30.调出生成getter/setter/构造器等结构： alt + shift + s

31.显示当前选择资源(工程 or 文件)的属性：alt + enter

32.快速查找：参照选中的Word快速定位到下一个 ：ctrl + k

----------------不常用------------------------------

33.关闭当前窗口：ctrl + w

34.关闭所有的窗口：ctrl + shift + w

35.查看指定的结构使用过的地方：ctrl + alt + g

36.查找与替换：ctrl + f

37.最大化当前的View：ctrl + m

38.直接定位到当前行的首位：home

39.直接定位到当前行的末位：end



### 项目2

（省略）



### 面向对象特征之二: 继承性

![image-20200220105400699](C:\Users\lfrdw\AppData\Roaming\Typora\typora-user-images\image-20200220105400699.png)

- 避免重复定义很多方法和属性
- 子类（派生类） & 父类（基类），子类获得父类的属性、方法（私有的属性和方法都继承到了）
- 子类不能直接访问父类中私有的成员变量和方法（但是可以通过get和set操作来实现）
- 格式：` class A extends B{}` 



- Java只支持单继承和多层集成：
  - 一个子类只能有一个父类
  - 一个父类可以被多个子类继承



- Java中关于继承性的规定：

  1.一个类可以被多个子类继承。

  2.Java中类的单继承性：一个类只能有一个父类

  3.子父类是相对的概念。

  4.子类直接继承的父类，称为：直接父类。间接继承的父类称为：间接父类

  5.子类继承父类以后，就获取了直接父类以及所有间接父类中声明的属性和方法



- 如果我们没有显式的声明一个类的父类的话，则此类继承于**java.lang.Object类**

所有的java类（除java.lang.Object类之外）都直接或间接的继承于java.lang.Object类

意味着，所有的java类具有java.lang.Object类声明的功能。