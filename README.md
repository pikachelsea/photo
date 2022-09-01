java笔记一（对象与类、继承）
==
一、基本概念及构造器
--
1、由类构造对象的过程被称为`创建类的实例`<br>
2、对象的三个`主要特征`:对象的行为、对象的状态、对象的标识<br>
3、类之间的关系：<br>依赖（一个类的方法使用或操纵另一个类的对象，减少使用）<br>聚合（类A的对象包含类B的对象）<br>继承<br>
4、使用对象的具体过程：构造对象->指定初始状态->对对象应用方法<br>
5、`对象变量并没有实际包含一个对象，它只是引用一个对象`<br>
6、初始化对象变量方法：<br>一、引用新构造的对象（eg.`Date d1=new Date()`)<br>
二、设置对象变量引用一个已有的对象（eg.Date d2=d1）<br>
三、可以显式将对象变量设置为`null`，表示目前没有引用任何对象<br>
7、静态工厂方法：具有返回这个对象的一个实例这种特点的静态方法<br>
作用：`不使用new`来创建对象......待补充<br>
eg.LocalDate d1=LocalDate.now()  （获取当前时间）<br>
8、只访问对象而不修改对象的方法为访问器方法（与c++中const后缀相似）<br>
访问后对象状态会改变的方法为更改器方法<br>
9、要想构建一个完整的程序，会结合使用多个类，但其中`只有一个类有main方法`<br>
在一个源文件中，只能有一个公共类（内含作为程序入口的main，`类名需与文件名相同`），但可以有任意数目的非公共类
10、类的实例字段可以为基本类型，也可本身就是一个`对象`（即属于某个类类型）<br>
11、构造器  与类同名--可重载--可有0、1或多个参数--没有返回值--总是`伴随new操作符一起调用`<br>
不要在构造器中定义与实例字段同名的局部变量<br>
12、java中所有的方法必须在`类的内部定义`<br>
13、如果需要返回一个可变数据字段的副本，应该使用`clone`......待补充<br>
14、一个方法可以访问`所属类`的`所有对象`的`私有数据`<br>
15、final实例字段  必须在构造对象时初始化（或者直接在声明处赋值）--之后不能再修改这个字段......待补充<br>
eg.private final int b=9;(赋值方法）<br>
eg.private final int b;构造器内b=9;(构造器方法，每个构造器内都要有值）
16、实例字段直接赋值的优先级低于构造器，若都有赋值，实例字段为构造器内的值


二、静态字段和静态方法
--
1、静态字段<br>
每个类一个（`共享`），非静态字段为每个对象有自己的一个副本<br>
即使没有对象，静态字段仍存在，`静态字段属于类，而不属于任何单个的对象`<br>


2、静态常量<br>
eg.public static final double PI(圆周率)<br>
System.out(声明为public static final PrintStream out(在System类中))<br>
性质：不管静态常量还是普通常量只要是基本类型就不能在初始化后重新修改其值<br>
对象类型普通常量、静态常量可以在初始化后修改其对象状态，但不可以改变其引用<br>


3、静态方法<br>
性质一、`静态方法为不在对象上执行的方法`<br>
二、静态方法只能访问静态字段，不能访问非静态实例字段<br>
三、可用类名也可以使用对象来调用静态方法<br>
四、main方法也是一个静态方法。在启动程序还没有任何对象时，静态的main方法将执行并构造程序所需要的对象<br>
static含义：`属于类而不属于任何类对象的变量和函数`<br>


4、静态工厂方法<br>
静态工厂方法与构造器对比优势<br>
1、静态工厂方法有名称（可通过不同方法名区分，而构造器限定为类名，通过参数进行区分，可能产生冲突）
2、静态工厂方法不用在每次调用的时候都创建一个新的对象......待补充<br>
3、静态工厂方法可以返回原返回类型的任何子类型对象（在构造器中只能返回当前类对象，而在静态工厂方法中可以返回当前类对象和`该类的任何子类`）<br>
4、静态工厂方法可通过参数值改变所返回的对象<br>
5、静态工厂方法返回的对象所属的类，在编写包含该静态工厂方法的类时可以不存在......待补充


三、方法参数和对象构造
--
java对方法参数的操作：<br>
1、方法不能修改基本数据类型的参数->`java总是使用按值传递`<br>
2、方法可以改变对象参数的状态，但不能让对象参数引用一个新的对象<br>
`对象引用是按值传递的`（对象引用实际上为一个副本，但与实际值引用同一对象，因此可以改变对象参数的状态）<br>
（但对于引用一个新的对象这类操作，改变的只是副本的引用，而不影响对象参数）<br>
3、方法的签名指方法名和参数类型<br>
4、`方法中的局部变量必须明确初始化`,但在类中若没有初始化类中的字段，将会自动初始化为默认值<br>
Java 中的变量分为类变量（即静态变量，有static）-> JVM的方法区<br>
成员变量（无static,类里方法外）-> 随着对象的建立而建立，随着对象的消失而消失，存在于`对象所在的堆内存`中。<br>
局部变量-> 栈内存<br>
5、显式字段初始化（类定义直接为字段赋值（先执行）--构造器赋值（后））<br>
6、this关键字使用(1、同c++this指针，指示隐式参数  2、使用this(相应参数),可在构造器中调用同一个类的另一个构造器<br>


四、异常
---
1、异常概述与异常体系结构<br>
一场对象都是派生自Throwable类（异常类中最大的父类）的一个类实例<br>
Error类:java虚拟机无法解决的严重问题,一般不编写针对性的代码解决 eg.堆溢出(outofMemoryError),栈溢出(StackMemory)<br>
Exception类:分支为RuntimeException(运行时错误）--其他异常（编译时错误）<br>
派生于Error类或RuntimeException类的所有异常称为`非检查类异常`，其他异常为`检查类异常`(进行相应处理)<br>
RuntimeException类：NullPointerException（空指针异常）<br>
ArrayIndexOutofBoundsException（数组越界异常）<br>
ClassCastException（强制类型转换异常）<br>
NumberFormatException（数字格式化异常）<br>
InputMismatchException（输入不匹配异常）<br>
ArithmeticException（数学错误）<br>


