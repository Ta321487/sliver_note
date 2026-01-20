# C# 笔记

### 第一章 概述

Microsoft .NET的组成部分：①Microsoft .NET平台；②Microsoft .NET产品和服务；③第三方.NET服务

“C#是为.NET Framework量身定做的。”

C#的特点：①语法简洁；②彻底的面向对象设计；③与Web应用紧密结合；④强大的安全性机制；⑤完善的错误、异常处理机制；⑥灵活的版本控制技术；⑦兼容性

第一个C#控制台程序：

```c#
Using System;
Using System.Collection.Generic;
Using System.Linq;
Using System.Text;
Using System.Threading.Tasks;
namespace helloworld				//命名空间
{
	class Program
{
	static void Main(string[] args)	
//Java：public static void main(String[] args)
	{
		Console.WriteLine(“Hello C#!”);
	}
}
}

```

### 第二章 输出与数据类型

关于输出：

①Console.WriteLine输出换行；Console.Write输出不换行

②可以采用Java形式的并置符号进行输出，如下面的例子：

```java
int age = 10;
string name = “张三”;
Console.WriteLine(“年龄是：” + age + “,姓名是：” + name); 
```

<em>控制台输出：年龄是：10,姓名是：张三</em>

③C#输出：

```c#
Console.WriteLine(“age = {0:d}”,name = “{1:s}”,age,name);
```

其中，若删除后面的变量age，则会抛出异常(System.FormatException)；而删除age={0:d}则不会抛出异常。

{0:d}中的“0”，表示要输出的第一个变量，若为“1”为第二个变量，以此类推…

{0:d}中的“d”，表示输出一个整型数据。f/F为浮点型类型，s/S为字符串类型

d后面若有数字，表示共有n位数字，不够该位数则左补0

d前面有数字则不会按格式输出，只会原样输出。

{0,5:d}的含义：形式为{y,x:d}。y表示下标第一个元素，x表示一共占用的位数，若x为正数则右对齐，不够位数左补空格；x为负数则左对齐，不够位数右补空格

字符串不受该规则的影响。

标识符的命名：字母、数字、下划线、@ 构成。第一个字符不能是数字；@ 只能放在首位

快捷键：Ctrl+K+C：设置多行注释；Ctrl+K+U：取消多行注释

快速输入：“cw” →Console.WriteLine();

f/F的默认小数位数为两位。若f后面有数字，表示保留的小数位数（四舍五入）

c有两种格式：①字符类型；②货币类型

字符类型：要在输出的变量前声明字符类型

例：

```C#
char b = (char)98;
	Console.WriteLine(“{0:c}”,b);
//输出为：b
```



货币类型：cn表示小数保留n位

例：

```C#
double m = 84.256;
	Console.WriteLine(“{0:c2}”),m);
//控制台输出：￥84.26
```



int.parse()：将字符串转换为int

Console.ReadLine();：从键盘上读取字符，返回该字符的ASCII值，只接收第一个字符

Console.Read();：防止控制台闪退（若不闪退则不用加此语句）。一般放在程序的最后面。

double的精度为15位。

| abstract | as      | base     | bool       | break    | byte     | case      | catch     | char     |
| -------- | ------- | -------- | ---------- | -------- | -------- | --------- | --------- | -------- |
| checked  | class   | const    | continue   | decimal  | defalut  | delegate  | do        | double   |
| else     | enum    | event    | explicit   | extern   | false    | finally   | fixed     | float    |
| for      | foreach | goto     | if         | implicit | in       | int       | interface | internal |
| is       | lock    | long     | namespace  | new      | null     | object    | operator  | out      |
| override | params  | private  | protected  | public   | readonly | ref       | return    | sbyte    |
| sealed   | short   | sizeof   | stackalloc | static   | string   | struct    | switch    | this     |
| throw    | true    | try      | typeof     | uint     | ulong    | unchecked | unsafe    | ushort   |
| using    | virtual | volatile | void       | while    |          |           |           |          |



C#数据结构：

1. 值类型
   1. 简单类型
      1. 小数类型
      2. 字符类型
      3. 布尔类型
   2. 结构类型（struct）
   3. 枚举类型（enum）
2. 引用类型
   1. 类类型
   2. 数据类型
   3. 结构类型
   4. 委托类型

整数类型：                                 

sbyte/byte：有符号8位整数/无符号8位整数（1个字节）

short/ushort：有符号16位整数/无符号16位整数（2个字节）

int/uint：有符号32位整数/无符号32位整数（4个字节）

long/ulong：有符号64位整数/无符号64位整数（8个字节）

浮点类型：

float：7位或8位浮点（4个字节）

double：15位或16位浮点（8个字节）

小数类型：

decimal：128位（16个字节），末尾加m

字符类型：用单引号括起的一个字符

布尔类型：true(真)、false(假)

引用类型：object是所有类型的基类

C#支持以下两种形式的字符串常数：

常规字符串常数：放在双引号之间的一串字符，解析出现的转义字符

逐字字符串常数：以@开头，不解析出现的转义字符

例：

```c#
String s1 = “hello\nworld”;
String s2 = @“hello\nworld”;
Console.WriteLine(s1);
Console.WriteLine(s2);
/*输出：
hello

world

hello\nworld
*/
```



类型转换：

低精度赋值给高精度，不需要强转；高到低赋值，需要强转

装箱与拆箱：

装箱：将基本类型赋值给引用类型

例：

```c#
int x = 20;
Object obj = x;
```

拆箱：将引用类型赋值给基本类型

例：

```C#
object obj2 = 30;
int d = (int)obj2;
```

 随机数：

Random r=new Random(); r是类类型

随机数的取值范围：左侧可取到，右侧取不到

表达式的值：

整型/整型 = 整型

整型/浮点型 = 浮点型

整型/负整型 = 负整型

### 第三章 运算符

1. 关系运算符（ < <= > >= != ==）：返回值是bool类型

   ```c#
    Console.WriteLine(3 > 8); //False
   	int x = 6;
   	Console.WriteLine(5 != 6); //True
    	Console.WriteLine(5 == x--);
   ```

   ​	<b>这种写法在C#中不识别！</b>

   ```c#
   Console.WriteLine(4<>5);
   ```

2. 逻辑运算符（ ! && ||）：表达式必须是bool类型

   <b>C#没有这种写法</b>

   ```c#
   Console.WriteLine(!5);
   ```

   短路效应：当做逻辑与运算时，第一个表达式False，第二个表达式则不再做运算；

   ​				    当做逻辑非运算时，第一个表达式True，第二官网表达式则不再做运算

   ```c#
   	int a = 5, b = 8;
   	 Console.WriteLine((a++ == 6) && (--b == 7)); //先带值再做++运算 false 右侧被短路了
        Console.WriteLine("a={0},b={1}", a, b);
        Console.WriteLine((a++ == 6) || (--b == 7));//经过上面的计算 a=6 true 右侧未被短路
        Console.WriteLine("a={0},b={1}", a, b); //6,7
   ```

3. 位运算（ &  |  ^  ~）

   1. 按位与 & ：对应的两个二进制位都为1，结果就为1

      ```C#
      	Console.WriteLine(3 & 4);
      /*运算过程
      	3 ->		0 0 1 1
      	4 ->		0 1 0 0
      			--------------
      				0 0 0 0
      */
      //结果为：0
      ```

   2. 按位或 | ：对应的两个二进制位有一个为1，结果就为1

      ```c#
      Console.WriteLine(3 | 4);
      /*运算过程
      	3 ->		0 0 1 1
      	4 ->		0 1 0 0
      			--------------
      				0 1 1 1
      */
      //结果为：7
      ```

   3. 按位异或 ^：对应的二进制位同为1（或同为0），结果为0，不同为1

      ```c#
      Console.WriteLine(4 ^ 5);
      /*运算过程
      	4 ->		0 1 0 0
      	5 ->		0 1 0 1
      			--------------
      				0 0 0 1
      */
      //结果为：1
      ```

   4. 按位反 ~ ：对应的二进制位为0就为1，为1就为0

      最高位：为左侧，是符号位，1为负数，0为正数

      ```c#
      Console.WriteLine(~2);
      /*运算过程
      	2 ->		0 0 1 0
      	取反		1 1 0 1
      */
      ```

      补充：负数的二进制

      ①先将该数的正数转为二进制，转后，再左补0（到8位）；

      ②取反再加1
      
      例：-3 的二进制？
      
      ① 3的二进制为11，左补6个0，即00000011
      
      ② 取反 00000011 ->11111100  再加1
      
      ```c#
      				1 1 1 1 1 1 0 0
                   +
                      0 0 0 0 0 0 0 1
                   --------------------
              		1 1 1 1 1 1 0 1
      ```

   5. 移位运算 <<  >>

      ```c#
      Console.WriteLine(4 << 3);
      Console.WriteLine(4 >> 3);
      /*运算过程
      	a << n 向左移 是乘法 数字变大 a*2^n
      	a >> n 向右移 是除法 数字变小 a/2^n
      */
      //结果为：32 0
      ```

      两个bool类型做位运算：

      ```c#
      Console.WriteLine(true & false);
      Console.WriteLine(true ^ true); 
      //结果为：false false
      ```

4. 条件运算符 ? :

   ```c#
   string city = 5 > 3 ? "大连" : "鞍山";
   Console.WriteLine(s);
   //执行过程：先判断"5>3"的值，为真执行"?"后的值，为假执行":"后的值。此处为真，输出"大连"
   ```

   程序：从键盘输入两个数，比较大小，按从大到小的顺序输出

   ```c#
   Console.Write("请输入第一个数字：");
   int num1 =int.Parse(Console.ReadLine());
   
   Console.Write("请输入第二个数字：");
   int num2 = int.Parse(Console.ReadLine());
   Console.WriteLine(num1>num2?(num1 + "，" +num2) : (num2 + "，" +num1));
   ```

5. 其他运算符(is sizeof typeof new checked unchecked)

   is：判断某变量是否满足某数据类型，返回bool类型

   ```c#
   int m = 20;
   Console.WriteLine(m is int); 
   Console.WriteLine(m is float); 
   //结果：true
   //    false (数据类型不符)
   ```

   sizeof：返回某值类型的字节数

   ```c#
    Console.WriteLine(sizeof(int));  //4
    Console.WriteLine(sizeof(Int16));//2
    Console.WriteLine(sizeof(Int64));//8
    Console.WriteLine(sizeof(Int32));//4
    Console.WriteLine(sizeof(char)); //2 char在Java和C#中占两个字节
   //Console.WriteLine(sizeof(m));  错误：参数只能是类型名，不能是变量名
   ```

   typeof：返回某类型在system中的对象

   ```c#
   Console.WriteLine(typeof(int)); //返回Int32
   Console.WriteLine(typeof(double)); //返回Double
   Console.WriteLine(typeof(long)); //返回Int64
   Console.WriteLine(typeof(float)); //返回System.Single
   ```

   checked与unchecked：检测溢出

   ```c#
    byte n = checked((byte)k);      //checked检测溢出
   Console.WriteLine(n); //抛出异常：System.OverflowException
   byte n = unchecked((byte)k);	//默认不检测溢出
   ```

### 第四章 结构化程序设计

1. 程序设计有三种基本结构：顺序，选择，循环

   定义两个变量，x , y，取值范围：随机数[1,100]，判断大小及输出最大值及平均值

   ```c#
   int x, y , max;
   double avg;
   Random r = new Random();
   x= r.Next(1,101);
   y= r.Next(1,101);
   if(x>y)
   {
       max = x;
   }
   else{
       max = y;
   }
   avg = (x+y)/2;
   Console.WriteLine("{0},{1},{2},{3}",x,y,max,avg);
   ```

   

2. if...else

从键盘输入一个成绩，为成绩划分等级：A优 B良 C中 D及格 E不及格

```c#
if(){
    
}else if(){
    
}else if(){
    
}else{
    
}
```

```c#
Console.WriteLine("input score:");
int score = int.Parse(Console.ReadLine());
if(score >=90 &&score<=100){
    Console.WriteLine("A");
}else if(score>=80){
    Console.WriteLine("B");
}else if(score>=70){
    Console.WriteLine("C");
}else if(score>=60){
    Console.WriteLine("D");
}else{
    Console.WriteLine("E");
}
```

3. switch开关语句（多条件分支结构）

   switch表达式可以是哪些类型？
   
   答：byte,short,int,long,char,bool,string,enum(枚举)
   
   ```c#
   int x = 2;
   switch(x){
       case 2:Console.WriteLine("one");break; //C#中 break不能省略
       case 3: //case后是常量,case后不能有重复值
       case 4:Console.WriteLine("four");break; 
       default://不是必须有的
           Console.WriteLine("end");
           break;
   }
   ```
   
4. 常用的循环：for,while,do...while,foreach(遍历集合和数组)

for循环(循环初值;循环条件;循环步进)

1. 可以在循环体外面声明变量类型及初始值，即下面的`int i = 1;`   但是分号不能省

   ```c#
   for(int i = 1; i < 101; i++)
           {
               sum += 1;
           }
           Console.WriteLine("i={0},sum={1}",i,sum);
   ```

   若省略了第二个分号，则程序进入死循环

2. do...while循环

   ```c#
   do{
   
   
   
   }while;
   ```

   循环条件开始不成立的话，循环体执行一次  <b>do...while的while后的分号不可省</b>

用循环来解决鸡兔同笼问题：笼子里一共有35头，94足，问鸡兔有几只。

```c#
int chicken, rabbits;
for (chicken = 0; chicken < 36; chicken++)   
{
    rabbits = 35 - chicken;
    if(chicken + rabbits == 35 && 2 * chicken + 4 * rabbits == 94)
   {
       Console.WriteLine("鸡有{0}只,兔子有{1}只",chicken,rabbits);
   }
}
```

循环实现从键盘上输入数字，求出该数的阶乘

```c#
 Console.WriteLine("请输入数字：");
        int num = 1;
        int x = int.Parse(Console.ReadLine());
        for(int i = 2; i <= x; i++)
        {
            num*=i;
        }
        Console.WriteLine("{0}的阶乘为{1}",x,num);
```

### 第五章 面向对象程序设计

1. 面向对象三大特征：封装、继承、多态

   ```c#
   Student s = new Student();
   ```

2. 命名空间(namespace)：相当于Java中的包(package)，不同工程下不可以导入其他命名空间。

3. class类

   修饰符可以有：internal、public、abstract，private（私有）

   public：公有的。只要是在同一个工程下，都可以访问

   internal：权限与public一样

   protected：受保护的。只能在本类内及子类中应用，其他类无权使用

   文件名可以和类名不同（ <b>这点和Java是不一样的</b>）

   受保护的(protected)不可应用，运行会出错（语义错误、逻辑错误）
密封类（sealed）静态（static）不可被继承 抽象类（父类）不能和sealed放在一起声明
   static一般用于修饰成员变量和方法
   
   类体中只有属性、方法

   方法：默认为私有的

4. 启动不同项目（在同一个解决方案下）：选中解决方案，在下方的属性选择”启动项目“

   

或者，右键解决方案，选择属性，选定”当前选定内容“

5. 继承：用" : "表示

6. 方法的重载：函数返回值类型不参与比较

7. 如何初始化成员变量？

   1. 通过自定义函数（方法）来实现初始化成员变量

      ```c#
      int sno,age; //成员变量（全局变量）
      string name; //系统会为成员变量赋初始值
      public void SetInfor() //不带参数的自定义方法
        {
          sno = 2;
          age = 48;
          name = "冬泳怪鸽";
        }
      public void SetInFor(int sno,int age,string name) //带参数的自定义方法
        {
        this.sno = sno;
        this.name= name;
        this.age = age;
        }
      ```

   2. 通过封装字段的方式，定义一系列的set和get方法，实现对成员变量的初始化

   ```c#
      int sno, age; 
      string name;
      public int Sno {  		 //属性名，对sno进行封装
      	get => sno;  		 //当调用属性名进行输出时，系统自动调用get方法
      	set => sno = value;  //当调用属性名进行赋值时，系统自动调用set方法
          }
      public int Age {  		 //属性名，对age进行封装
          get => age; 
          set => age = value;
          }
      public string Name{     //属性名，对age进行封装 
          get => name; 
          set => name = value; 
          }
   ```

选中```int sno, age;```和```string name;```，右键“快速操作和重构”→“封装字段（并使用属性）”

通过构造函数进行初始化成员变量 。选中变量，快速操作和重构，封装字段（并使用属性）

```c#
int sno, age; //成员变量（全局变量）
        string name;  //ctor：生成构造函数（两次tab）  
        public Student() //public 或 internal都可以
        {  //不带参数的构造函数，初始化成员变量
            sno = 8;
            age = 22;
            name = "jack";
        }
        public Student(int sno, int age, string name)
        {
            this.sno = sno;
            this.name = name;
            this.age = age;
        }
        public void Show()
        {
            Console.WriteLine("", sno, this.name, this.age); //可以省略this（本类中）
            Console.WriteLine("{0},{1},{2}", sno, age, name);
        }
```

方法重载：函数返回值类型不参与比较

当类中没有显式的定义过构造函数时，系统会提供一个不带参数的构造函数
但是，当类中已经显示的定义了构造函数，系统不会再默认提供不带参数的构造函数

析构函数

定义：在函数前加上波浪线```~Student()```

不允许使用访问权限修饰符，无返回值类型，不带参数；不允许重载，一个类最多有一个析构函数

功能：与构造函数相反。

​	构造函数：是一个入栈操作。创建对象，开辟空间，占用内存

​	析构函数：是一个出栈操作。删除对象，释放空间，节省内存。

执行顺序：

​	构造函数：先父后子，在创建对象时系统自动调用

​	析构函数：先子后父，在程序结束时系统自动调用

当子类定义了与父类同名的变量，且父类的同名的变量能被继承。若子类变量没有加new，表示隐式隐藏父类同名的变量；若显式的加new，表示显式隐藏父类同名的变量（可以理解为子类新定义的变量）

调用函数：传值（值传递），不改变实参大小

引用(ref)：传址（地址）

out输出参数一定要初始化

```c#
public int age, sno;//实例变量（没有使用static修饰）
public static string sname;//类变量（使用static修饰的变量：静态变量）
```

```c#
<summary>
"///"是摘要的缩写
实例变量可以由this或者对象名调用，不能用类名调用
静态变量可以由类名直接调用，但是不能被this或对象名调用
实例方法可以调用外部的实例变量、静态变量、静态方法、实例方法
静态方法可以调用外部的静态变量、静态方法，不能调用实例变量或实例方法
1. 实例变量是否会被所有对象共享？。2. 静态变量是否会被所有对象共享
1. 不会 各用各自的              2. 会，所有对象共享静态变量
</summary>
```

委托：

1. 声明委托

   ```c#
   public delegate void Del1();
   public delegate int Del2(int x);
   public delegate int Del3(int x, int y);
   ```

2. 定义方法（与委托类型相似的方法）

   ```c#
   
           public void M1()
           {
               Console.WriteLine("hi");
           }
           public int M2(int x)
           {
               Console.WriteLine("miss you");
               return x;
           }
           public int M3(int x,int y)
           {
               return x+y;
           }
   ```

3. 创建委托对象

   ```c#
   Del1 d1 = new Del1(t.M1);
   Del2 d2 = new Del2(t.M2);
   Del3 d3 = new Del3(t.M3);
   ```

   通过委托调用类中的方法
   
   ```c#
   d1();
   d2(5);
   Console.WriteLine(d2(6));
   d3(3, 5);
   ```
   

C#中常用的基础类库：

1. 数学类：Math()

   ```c#
   Console.WriteLine(Math.Abs(-3)); //求绝对值
               Console.WriteLine(Math.Ceiling(3.5)); //向上取整，值=4
               Console.WriteLine(Math.Ceiling(-3.8));//向上取整，值=-3
               Console.WriteLine(Math.Floor(2.8)); //向下取整，值=2
               Console.WriteLine(Math.Floor(-2.8));//向下取整，值=-3
               Console.WriteLine(Math.Pow(4,3)); //4的3次幂
               Console.WriteLine(Math.Sqrt(441));//开根号
               Console.WriteLine(Math.Sqrt(1.96)); //开根号 1.4
               Console.WriteLine(Math.Max(-5,-4)); //求最大值 -4
              //只能接受两个数据
               Console.WriteLine(Math.Min(-5, -4)); //求最小值 -5
               Console.WriteLine(Math.Round(1.5)); //=2
               //Round()：一个参数，若整数部分是奇数，四舍五入取整
               //         一个参数，若整数部分是偶数，五舍六入取整
               Console.WriteLine(Math.Round(2.156789,3));
               //         两个参数，第二个参数表示小数部分保留的位数。无论整数部分是奇数/偶数，小数部分保留相应的位数
               //函数可以嵌套使用
               Console.WriteLine(Math.Max(Math.Min(2, 5), 8));
   ```

2. 日期类：DateTime()，DateSpan()

   ```c#
   DateTime time = DateTime.Now; //获取系统实时时间（年月日小时分秒）
               Console.WriteLine(time);
               Console.WriteLine("今天是：{0}年{1}月{2}日",time.Year,time.Month,time.Day);
               Console.WriteLine("此刻是：{0}时{1}分{2}秒", time.Hour, time.Minute, time.Second);
               DateTime before = new DateTime(2008,8,8); //创建对象,三个参数（年月日）
               Console.WriteLine(before);
               DateTime ago = new DateTime(2008, 8, 8,19,56,0); //创建对象,六个参数（年月日时分秒）
               Console.WriteLine(ago);
               TimeSpan t = time - ago; //时间间隔
               Console.WriteLine(t.Days); //相差的天数
               //H:24小时制 h:12小时值
               Console.WriteLine("{0:yyyy-M-d  H:m:s}",time); //格式化输出日期时间（yyyy：四位年）
               Console.WriteLine("{0:yy-M-d  H:m:s}", time); //格式化输出日期时间（yyyy：两位年）
               
   ```

### 第六章 抽象类、多态和接口

定义抽象类：父类，模板，抽取出公共的属性及行为（一般是抽象的方法
必须定义子类，重写父类中的抽象方法
抽象类不允许实例化（不允许用抽象类创建对象）

定义抽象类：类体中可以定义抽象方法，也可以有非抽象方法，可以有成员变量
抽象方法：只允许声明，不允许有方法体，等待子类重写所有的抽象方法
非抽象子类中要实现父类所有抽象方法
抽象子类可以实现父类部分抽象方法或者不实现，可以在他的子孙后代在实现

```c#
 LittleDog d = new LittleDog();
Animal a = new LittleDog();  //a：上转型对象（父类声明一个变量，实体是子类对象
//LittleDog ld = new Animal(); //不允许
//上转型对象：能调用子类重写的方法以及继承的成员，但是不能调用子类新增加的成员
a.Cry();
a.Eat();
d.age = 20;
LittleDog se = a as LittleDog; //as：将上转型对象强制转换成子类对象
se.age = 25;

Dog dog = new LittleDog(); //dog：上转型对象
dog.Cry();
dog.Eat();
```

定义接口，接口内不允许定义变量。常量等
接口中所有方法默认，省略public abstract

一个类可以继承多个抽象类。virtual，abstract不可同时存在，某类继承某接口时，必须重写接口中所有的方法。不能对接口及抽象类实例化

一个抽象类继承某接口时，必须实现接口中的所有抽象方法

不能对接口实例化

接口回调：可以调用类中重写的或继承的方法，不能调用类中新增加的成员

### 第七章 字符串与数组、枚举

一、字符串

1. 字符串比较：Compare，CompareTo

   ```c#
          string s1 = "hello";
          string s2 = "he";
   ```

   1. Compare()

   string.Compare(s1, s2) ; s1<s2 →-1

   string.Compare(s1, s2) ; s1<s2 →  1

   string.Compare(s1, s2) ; s1==s2 → 0

   2. 比较的顺序：aAbBcC...xXyYzZ

      string.Equals：字符串比较方法

      ```c#
       Console.WriteLine(string.Equals("one","two")); //False
       Console.WriteLine(string.Equals("one", "ONE")); //False
       Console.WriteLine("ONE".Equals("one")); //False
      ```

      不能对string进行实例化（不能new）

   3. Compare.To()：可以是任意两个类型相同的比较

      ```Console.WriteLine('a'.CompareTo('A'));   //输出32 ASCII的差值```

      ```Console.WriteLine(12.CompareTo(11));```
      ```Console.WriteLine(true.CompareTo(false));```

2. 定位字符串

   StartsWith()：某串以谁为首

   ``` Console.WriteLine("love China".StartsWith("love"));```

   EndWith()：某串以谁为尾

   ``` Console.WriteLine("the same world".EndsWith("word"));```

   Indexof()：返回第一次出现该字符的索引号（从零开始）

   Indexof(“”,start,end)：返回第一次出现该字符的索引号（从start开始） 找不到返回-1

   ```Console.WriteLine("I like China".IndexOf('i',4)); // 9 ``` 

   ```Console.WriteLine("I like China".IndexOf('i',4)); // -1 ```

   ```Console.WriteLine("hill".IndexOf("l")); ```

   IndexofAny()

   ```c#
    char[] a = { 'a', 'c', 'e' };  //字符数组
           string s1 = "I have an icecream";
           Console.WriteLine(s1.IndexOfAny(a)); //查找字符数组中第一个出现在字符串中的索引，找不到返回-1
           Console.WriteLine(s1.IndexOfAny(a,4)); //字符串从下标为4开始，查找字符数组中的第一个出现在字符串中的索引
           Console.WriteLine(s1.IndexOfAny(a,4,5)); //字符串从下标为4开始，连续查找5个字符，返回字符数组中第一个出现的索引
           Console.WriteLine(s1.LastIndexOfAny(a)); //自右向左查找
   ```

3. 字符串连接:concat,Join, +

   ```c#
      string[] s2 = {"one","two","three"};
      string[] s3 = { "one", "two", "three" };
      Console.WriteLine(string.Concat("one","first","three"));
      Console.WriteLine(string.Concat(s2));
      Console.WriteLine(string.Join("-","one","two","three"));
      Console.WriteLine(string.Join(",",s2));
   ```

4. 分割字符串：

   ```c#
   string str = "hello,i miss you! bye";
           char[] sep = { ',', ',', ',', ',' }; //定义分隔符数组
           string[] words = str.Split(sep); //分割字符串
           foreach(var item in words)
           {
               Console.WriteLine(item);
           }
           Console.WriteLine(words.Length);
   ```
   
5. 插入字符串：Insert()

   ```c#
    string s1 = "welcome";
           Console.WriteLine(s1.Insert(0," to dalian")); //第一个参数表示起始下标，第二个参数表示插入的值 
           Console.WriteLine(s1.Insert(s1.Length, " to dalian"));
           // Console.WriteLine(s1.Insert(s1.Length+1, " to dalian")); 越界
   ```


6. 删除字符串

   ```c#
   	string s2 = "miss you daring";
   	Console.WriteLine(s2.Remove(9)); //一个参数表示起始位置/下标/索引（默认删除到最后）
   	Console.WriteLine(s2.Remove(9,3)); //从下标为9处开始连续删除3个字符
   	Console.WriteLine(s2);//insert，remove不改变原串的值，返回的是一个新的串
   
   //string是一个静态字符串
   ```

7. 复制字符串

```c#
        string s4 = "honey";
        string s3 = string.Copy(s4); //复制
        Console.WriteLine(s3);
        string sourceStr = "Love you my country";
        char[] c1 = { 'd', 'e', 'a', 'r' };
        char[] cc = new char[100];
        //sourceStr.CopyTo(0, c,0,4);
        sourceStr.CopyTo(0, c, 2, 1);
        //从原串下标为0处开始复制1个字符到c数组中，并存放在数组中下标为2的地方
        Console.WriteLine(cc);

```

8. 字符串替换

```c#
        Console.WriteLine("love you".Replace("love","hate")); //第一个参数是旧参数，第二个参数是新参数
        Console.WriteLine("love you".Replace('o','i'));
```

9. 大小写转换

```c#
        Console.WriteLine("sweater".ToUpper()); //转大写
        Console.WriteLine("MISS".ToLower()); //转小写
```

10. 截取字串

```c#
		string s5 = "the same song";
        Console.WriteLine(s5.Substring(4)); //从下标为4开始截取，默认截取到最后
        Console.WriteLine(s5.Substring(4,4));//从下表为4开始截取，截取4个（第二个参数表示截取个数）
```



综合应用：

```c#
using System.Text;

namespace program{
    class Program
    {
        static void Main(string[] args)
        {
            string s = "it is a fine day";
            Console.WriteLine(s.Insert(s.Length," happy"));
            Console.WriteLine(s);
            Console.WriteLine(s.Replace("fine", "bad"));
        Console.WriteLine(s);

        s = s.Replace(" is", "");
        s = s.Substring(0, 1).ToUpper() + s.Substring(1, s.Length - 1);
        Console.WriteLine(s);
        //---------------------------
        char[] c = { 's', 'h', 'e' };
        string s1 = new string(c);
        string s2 = new string('a', 3); //第二个参数：重复的次数
        Console.WriteLine(s1);
        Console.WriteLine(s2);

```

11. 动态字符串

```c#
    StringBuilder str = "miss you"; 不正确
    StringBuilder str = new StringBuilder();
    Console.WriteLine(str);
    Console.WriteLine(str.Length); //空串的长度为0

    str.Append("one"); //在末尾插入数据
    Console.WriteLine(str);
    str.Append("two three");
    str.Append("three", "four"); //只接收一个参数
    str.Append("four");
    Console.WriteLine(str);
```

 1.  创建动态字符串方法1

     ```c#
     StringBuilder str1 = new StringBuilder();
     Console.WriteLine(str1.Capacity); //默认容量：16，超出容量会进行翻倍（16，32，64...)
     str1.Append("我们是中国人，我爱中国");//容量正好16
      Console.WriteLine(str1.Capacity); //16
     str1.Append("我们都是好人");
     ```

2. 创建动态字符串方法2

 ```c#
 StringBuilder str2 = new StringBuilder("hello");
     Console.WriteLine(str2); //直接输出hello
     Console.WriteLine(str2.Capacity); //容量16
 ```

3. 创建动态字符串方法3

   ```c#
   StringBuilder str3 = new StringBuilder("hello", 100); //100表示其容量
   Console.WriteLine(str3.Capacity);
   
   Console.WriteLine(str3.Length);
   str3.Insert(str3.Length, "honey");
   Console.WriteLine(str3);
   
   StringBuilder str4 = new StringBuilder("hello");
   str4.Capacity = 10;
   str4.Remove(2, 3); //从下标2开始，删除3个
   str4.Clear(); //清空字符串
   ```

二、数组

1. 声明数组：```int[] a;```

   声明数组时，长度不可省略。可以是常量/常量表达式/变量

   ```int[] e = new int[5] { 1, 2 }; //数量不符，错误```

   

2. 注意：这种声明方式为错误声明：``a = {1,2,3,4};``

3. 静态初始化一个数组：```int[] a = { 1, 2, 3, 4, 5 }; ```

4. 动态初始化一个数组：

   ```c#
   int[] b = new int[5]; //动态创建数组，长度为5
   b[0] = 1;
   ```

应用：随机生成1~100之间的整数，输出到屏幕上

```c#
int[] b = new int[5]; //动态创建数组，长度为5
b[0] = 1;
Random r = new Random();
for (int i = 0; i < b.Length; i++) //初始化数组
   {
    b[i] = r.Next(1, 101);
   }
for (int i = 0; i < b.Length; i++)
    {
    Console.WriteLine(b[i] + " ");
 }
```

应用：定义一个5个元素的数组，求最大值及最小值

```c#
			int[] arr = { 36, 23, 45, 64, 87, 77, 75 };
            int max = arr[0];
            for (int i = 1; i < arr.Length; i++)
            {
                if (arr[i] > max)
                {
                    max = arr[i];
                }
            }
            Console.WriteLine("最大值为：" + max);
            int min = arr[0];
            //        最小值
            for (int i = 1; i < arr.Length; i++)
            {
                if (min > arr[i])
                {
                    min = arr[i];
                }
            }
            Console.WriteLine("最小值为：" + min);
```

数组中常用的函数：(以下1至5的调用都基于本数组：```int[] a = new int[10];```)

1. 最大值与最小值

   ```c#
   Console.WriteLine("最大值："+a.Max()); 
   Console.WriteLine("最小值："+a.Min());
   ```

2. 求和与平均值

```c#
Console.WriteLine("求和："+a.Sum());
Console.WriteLine("平均值："+a.Average());
```

3. 对数组排序（正序）

```c#
Array.Sort(a); //括号内是数组名,升序排序
foreach(var item in a)
  {
  Console.Write(item + "  ");
  }
 Console.WriteLine();
```

4. 逆序排序数组

```c#
Array.Reverse(a);
foreach (var item in a)
{
Console.Write(item + "  ");
}
Console.WriteLine();
```

5. 输出数组的维数

```c#
 Console.WriteLine("数组维数："+a.Rank); //1
```

6.  二分查找法返回数组中某元素的下标

```c#
int[] b = { 5, 1, 8, 3, 12, 6, 9 };
foreach (var item in b)
 {
 Console.Write( item + "  ");
 }
 Array.Sort(b); //应用二分查找法时要先进行排序
 foreach (var item in b)
 {
  Console.Write(item + "  ");
 }
 Console.WriteLine(Array.BinarySearch(b,9));
//说明：对数组b进行二分查找法，是否存在元素9，存在返回该下标，不存在则返回负数
```

7. 判断数组中是否包含某个元素

```c#
int[] c = { 22, 3, 5, 55, 8, 9 };
Console.WriteLine(c.Contains(5));  //存在返回True，否则返回False
```

8. 返回数组中指定索引处元素的值（数组名为c）

```c#
 Console.WriteLine(c.GetValue(1));
```

9. 为数组中指定索引处元素设置取值

```c#
c.SetValue(66,0); 
Console.WriteLine(c[0]);
```

10. 返回数组某元素的下标

```c#
Console.WriteLine(Array.IndexOf(c,8)); //返回元素8在数组c的下标
Console.WriteLine(Array.IndexOf(c, 20)); //找不到返回-1
```

11. 判断数组是否具有固定长度

```c#
Console.WriteLine(c.IsFixedSize);
int n = 5;
int[] ar = new int[n];
Console.WriteLine(ar.IsFixedSize);
```

12. 返回某数组指定维数元素的个数

```c#
int[,] cc = { { 1, 2, 3 }, { 3, 4, 5 } }; //二维数组
Console.WriteLine(cc.GetLength(0)); //行数
Console.WriteLine(cc.GetLength(1)); //列数
```

13. 克隆一个数组（理解即可）

```c#
 int[] arr = { 1, 2, 4, 4 };
 int[] cloneA = arr.Clone() as int[]; //as：强制转换
```

14. 数组进行复制

```c#
int[] source = { 1, 2, 3, 4, 5 };
int[] target = new int[10];
source.CopyTo(target, 2); //
foreach (var item in target)
 {
  Console.Write(item + "  ");
 }
 int[] a1 = { 22, 11, 55, 8 };
 int[] b1 = new int[10];
 a1.CopyTo(b1, 2); //将数组a1所有元素复制到数组b1中下标为2处
 foreach (var item in b1)
   {
    Console.Write(item + "  ");
 	}
   	Console.WriteLine();

    int[] b2 = new int[10];
    Array.Copy(a1, b1, 3); //三个参数：将a1数组中3个元素复制给b1数组
    Array.Copy(a1, 1, b2, 2, 3);//五个参数：将a1数组下标为1开始的3个元素复制给b2数组下标为2处
            //foreach (var item in b2)
            //{
            //    Console.Write(item + "  ");
            //}
```

15. 二维数组

    ```c#
    int[,] num = { { 1, 2, 3 }, { 4, 5, 6 } };//静态初始化
    //int[,] num = { { 1, 2, 3 }, { 4, 5 } }; //列数目不匹配，错误
    int m = 2, n = 3;
    //int[,] n = new int[2, 3];//动态创建二维数组，长度不可以省略（因为没有初始化）
    int[,] x = new int[m, n];//长度可以是常量。变量或是表达式
    int[,] ar = new int[2, 3] { { 1, 2, 3 }, { 4, 5, 6 } };
    int[,] ar1 = new int[,] { { 1, 2, 3 }, { 4, 5, 6 } };//动态创建二维数组并初始化，长度可以省略
    Random random = new Random();
    int[,] s = new int[4, 5];
      for (int i = 0; i < 4; i++)
         {
           for (int j = 0; j < 5; j++)
              {
               s[i, j] = random.Next(1, 11);
              }
         }
     //遍历二维数组
      for (int i = 0; i < 4; i++)
      {
      for (int j = 0; j < 5; j++)
      {
       Console.Write(s[i, j] + "  ");
      }
       Console.WriteLine();
                }
      //GetLowerBound(0)：行标最小值 GetUpperBound(0)：行标最大值
     //GetLowerBound(1)：列标最小值 GetUpperBound(1)：列标最大值
     //数组名.GetLength(0); 行数
     //数组名.GetLength(1); 列数
     //数组名.Length; 所有元素个数
    ```
    
16. 动态数组

```c#
ArrayList list = new ArrayList(); //创建动态数组对象，无参
Console.WriteLine(list.Count); //获取元素个数
Console.WriteLine(list.Capacity);//获取容量。一个元素也没有
//当动态数组容量超出4个字符时，一般会翻倍
list.Add("hello");
Console.WriteLine(list.Capacity);
 // 创建动态数组对象，带一个参数（容量）
ArrayList list1 = new ArrayList(50);
Console.WriteLine(list1.Count);
Console.WriteLine(list1.Capacity);
//创建动态数组对象，带一个参数（可以是一个静态数组，也可以是动态数据）
int[] a = { 1, 2, 3 };//静态数组
ArrayList list2 = new ArrayList(a); //静态数组
ArrayList list3 = new ArrayList(list); //上一个动态数组
```

动态数组常用方法：

1. 末尾追加

   ```c#
   list3.Add("end");
   Console.WriteLine(list3[list3.Count-1]); //输出最后一个元素
   ```

2. 向指定位置添加数据

   ```c#
   list3.Insert(0,"hi,");
   ```

   （也可以在某位置插入另外一个数组）

   ```c#
   list3.InsertRange(0,list2);
   ```

3. 删除数组元素

   ```c#
   list3.Remove("end"); //删除某值
   ```

   （删除索引号对应的值）

   ```c#
   list3.RemoveAt(0);
   ```

   （删除一个范围。有两个参数：index(索引)，count(要删除的数量)）

   ```c#
    list3.RemoveRange(0, 3); 
   ```

4. 判断数组中是否包含某值。参数：某值。返回一个布尔值

   ```c#
   Console.WriteLine(list3.Contains(888)); 
   ```

5. 返回某元素索引

   ```c#
   Console.WriteLine(list3.IndexOf(22));
   Console.WriteLine(list3.IndexOf(22,1));
   ```

6. 排序

   ```c#
   int[] b = { 1, 22, 3, 8, 5 };//静态数组
   string[] c = { "one", "two", "three" };
   ArrayList list4 = new ArrayList(c);
   list4.Sort(); //不能针对各种数据类型的数组进行排序
   list4.Reverse();//反向排序
   ```

7. 清空数组内容

   ```c#
   list4.Clear();
   ```

三、枚举

1. 定义枚举

   ```c#
   enum 枚举名{
       ... //枚举成员
           //枚举成员的值默认从0开始，步长为1
   }
   ```

2. 取默认值：sun, mon, tue, wed,thu, fri, sat（0，1，2，3，4，5，6）
3. 部分赋值：sun, mon, tue=5, wed,thu, fri=10, sat
4. 成员取值可重复：sun, mon, tue=5,wed,thu.fri,,sat
5. 死循环：sun, mon, tue=5,wed,thu.fri=sat,sat
6. 未进入死循环：sun, mon, tue=5,wed,thu.fri=sat,sat=22



### 第八章 窗体应用程序设计

从本章开始，新建项目时要选择“Windows 窗体应用”

![image-20220507100320865](image-20220507100320865-16518890042741.png)

在右侧“解决方案资源管理器”中选择Program.cs文件，进入代码编写。在```Application.Run()```处写上```new 窗体应用名()```。此处的作用是启动程序时会开启哪一个窗体（需要启动哪一个就new哪一个）

单击Form.cs，会进入窗体设计界面

常用的窗体属性：

1. ```(Name)```：窗体的名字（和上面提到的```new 窗体应用名```是同一个名字）
2. ```BackColor```：窗体背景颜色
3. ```BackgroundImage```：窗体背景图片
4. ```Font```：字体
5. ```FontColor```：字体颜色
6. ```Icon```：窗体图标
7. ```Text```：与控件关联的文本

单击左侧工具箱，可以打开一系列与窗体相关的控件及控件

常见的事件

1. `Load`：加载时发生
2. `Click`：单击时发生
3. `FormClosing`：关闭时发生

跳转界面（单击事件）：

1. 创建窗体对象
2. 显示对应的窗体页面：```窗体名.Show();```
3. 隐藏当前窗体：```this.Hide();```

练习：加载时窗体大小(400,300)，设置背景颜色，在屏幕居中

1. 新建窗体

2. 直接双击窗体

3. 编写如下代码：

   ```c#
   this.Width = 400;
   this.Height = 300;
   this.BackColor = Color.Pink;
   this.ForeColor = Color.Blue;
   this.CenterToScreen();
   ```

一、单击窗体时发生的事件

消息框（在代码界面输入mbox按两次tab键，快捷输入```MessageBox.Show("Text");```）

```MessageBox.Show```共有可以带四个参数，其中：

​	带一个参数：显示对话框中的内容   ```MessageBox.Show(‘这是一个对话框’);```

![image-20220508161442911](image-20220508161442911.png)

​	带两个参数：显示对话框中的标题   ```MessageBox.Show(‘这是一个对话框’,'这是标题');```

![image-20220508161745014](image-20220508161745014.png)

​	带三个参数：对话框按钮中的类型  ```MessageBox.Show(‘这是一个对话框’,'这是标题',MessageBoxButtons.AbortRetryIgnore);```

![image-20220508162836845](image-20220508162836845.png)

```.AbortRetryIgnore```：中止 | 重试 | 忽略

```.CancelTryContinue```：取消 | 重试 | 继续

```.OK```：确定

```.OKCancel```：确定 | 取消

```.RetryCancel```：重试 | 取消

```.YesNo```：是 | 否

```YesNoCancel```：是 | 否 | 取消

​	带四个参数：对话框内部图标的样式

 ``` (‘这是一个对话框’,'这是标题',MessageBoxButtons.AbortRetryIgnore,MessageBoxIcon.Question);```

二、关闭窗体时发生的事件

1. 先使用```DIalog.Result```声明一个关闭对象：```DialogResult dr```；

2. 建立一个对话框，提示关闭信息

   ```MessageBox.Show("保存对此文件的修改？", "notice", MessageBoxButtons.YesNo, MessageBoxIcon.Question);```

3. 对单击关闭按钮时进行逻辑判断：当单击“是”时关闭该程序，单击“否”时不关闭该程序

   ```c#
   if (dr == DialogResult.Yes)
   {
   	e.Cancel = false; 
   }
   else
   	e.Cancel = true; 
   ```

实例：用户单击窗体上的【跳转】按钮，提示文字：是否需要跳转，是则跳转，否则留在本窗体

![image-20220508170332905](image-20220508170332905.png)

```c#
DialogResult dr = MessageBox.Show("确定跳转吗？", "notice", MessageBoxButtons.YesNo, MessageBoxIcon.Question);
if (dr == DialogResult.Yes)
   {
   Form2 f2 = new Form2();
   f2.Show();
   this.Hide();
 }
```

新窗体：

![image-20220508170450591](image-20220508170450591.png)

练习：新建一个窗体，绘制如下的页面。![image-20220508170822486](image-20220508170822486.png)

要求：单击【增加】按钮，计数器的值会增加；单击【递减】按钮，计数器的值会减少（步进值任意）；单击【显示】按钮，屏幕弹出对话框，将当前计数器的值显示在对话框中。

1. （绘制窗体略）
2. 在加载事件外部新建全局变量（成员变量）```int Counter;```
3. 在加载事件内部定义计数器的初值及自定义方法
4. 在自定义方法内部新建一个字符型变量，用于存放计数器内的值
5. 在【增加】按钮处双击，添加单击事件。单击事件内部为计数器自增，并调用自定义方法
6. 在【递减】按钮处双击，添加单击事件。单击事件内部为计数器自减，并调用自定义方法
7. 在【显示】按钮处双击，添加单击事件。新建对话框对应的代码，并且用并置符号将自定义方法内的字符型变量连接起来

代码如下：

```c#
public Form3()
        {
            InitializeComponent();
        }
        int Counter; //定义全局变量（成员变量）

        private void Form3_Load(object sender, EventArgs e)
        {
            Counter = 0;
            //Display();
        }
        public void Display() //自定义函数显示counter的信息
        {
            string count = Counter.ToString();
            label1.Text = "计数器的值是"+count;
            //label1.Text1 = n+"";
        }

        private void button1_Click(object sender, EventArgs e)
        {
            Counter += 5; //counter的值递增
            Display(); //调用方法，显示counter的变化
        }

        private void button2_Click(object sender, EventArgs e)
        {
            Counter -= 5; //counter的值递减
            Display(); //调用方法，显示counter的变化
        }

        private void button3_Click(object sender, EventArgs e)
        {
            MessageBox.Show("当前计数器的值为"+Counter.ToString("f"));
        }
```

