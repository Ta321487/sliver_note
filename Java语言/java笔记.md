# Java基础

## 一、Java的特点

1. 简单

2. 面向对象

3. 与平台无关

4. 多线程

5. 多态

## 二、安装与配置JDK

1. 安装与解压时，尽量不要放在中文目录中。

2. 一台电脑可以安装多个JDK。

3. 环境变量：此电脑→右键→属性→高级系统设置

4. 环境变量的名字不区分大小写。

5. Java_home：JDK解压或安装的目录

6. path：不能删除只能编辑。JDK的bin目录

7. 测试安装成功与否：开始→运行(win+r)→cmd→Java –version

## 三、JDK与JRE的关系

1. JDK：可以开发、编译以及运行Java应用程序的工具。
2. JRE：可以运行Java应用程序的工具。
3. JVM：Java虚拟机。

## 四、Java平台简介

1. JavaSE(J2SE)
2. JavaEE(J2EE)
3. JavaME(J2ME)

## 五、第一个Java示例

1. Java代码区分大小写。
2. 一个.Java文件中可以出现多个类(class)。
3. 一个.Java文件中只能出现一个公有(public)的类(class)。
4. 公有类的名字必须与文件名保持一致(包括大小写)。
5. main()方法是JavaSE程序的入口。
6. 从JDK1.4开始main()必须是公有的。
7. Java代码使用分号表示结束。
8. Java中只能直接使用半角(英文)标点符号。

## 六、编译与运行Java程序

1. Java的文件类型：

* .Java：源文件。文本文件用于保存源代码。
* .class：类文件。二进制文件用于字节码。

2. Javac命令：检查.Java中是否存在语法错误。如果没有错误则根据.Java文件编译生成对应的.class文件。

* 格式：Javac 文件名.Java

3. Java命令：运行.class文件。

* 格式：Java 类名(区分大小写)

## 七、Java的命名规范

1. 类名：首字母大写，其它均为小写。如果类名由多个单词组成，要求每个单词首字母大写，其它均为小写。如：UserMessage,OracleDriver
2. 变量名：所有字母均为小写。如果变量名由多个单词组成，从第二个单词开始，每个单词首字母大写，其它字母均为小写。如:name,userPassword
3. 方法名：与变量名一致的。如：insert(),selectByUserId()
4. 包名：均为小写。org.springframework.boot，com.mysql.jdbc.Driver
5. 泛型名：大写一个字母。
6. 常量名(static final)：均为大写。如果常量名字由多个单词组成单词之间使用下划线分隔。

## 八、注释：不参与编译与运行的内容

1. 单行注释：// 注释内容

2. 多行注释：/*注释内容*/

3. 文档注释：/** 注释内容 */

## 九、Eclipse快捷键

1. 改变字体大小：Ctrl+(非小键盘的+与-号)
2. 添加main()方法：main-->alt+/
3. 整理格式：Ctrl+Shift+F
4. 批量修改变量名：选中变量，Alt+Shift+R，回车。
5. 批量移动代码：Alt+(上/下键)

# 数据类型

## 一、Java中只有两种数据类型：基本数据类型、引用数据类型

## 二、基本数据类型：8种

1. 整数：Java中没有无符号的数字。默认情况下数字为十进制，整数使用0开头表示八进制。整数使用0X或0x开头表示十六进制。整数使用0B或0b开头表示二进制。

* byte:1个字节。-27--27-1
* short:2个字节。-215--215-1
* int:4个字节。-231--231-1，Java中整数默认为int类型。
* long:8个字节。-263--263-1，在整数后面加L或l。

2. 浮点数：Java中浮点数的运算一定会产生误差。

* float:4个字节，在浮点数后面加F或f。
* double:8个字节，Java代码中浮点数默认为double类型。

3. 字符类型：char,字符类型的值必须放在一对单引号中，并且单引号中只能出现一个字符。Java使用Unicode字符集。Unicode字符集中所有的字符都是两个字节。
4. 布尔类型：boolean,只有两个值：true/false。Java中boolean不能转换为其它类型。

## 三、变量

1. 声明变量：数据类型 变量名[=值];
2. 可以在一行中声明多个类型相同的变量。

```Java
 public static void main(String[] args) {
  int age = 20;
  double salary;
  int a,b,c = 10;
}
```

3. 变量没有赋值时不能使用，否则编译失败。

```Java
 public static void main(String[] args) {
  int age = 20;
  double salary;
  int a,b,c = 10;
  System.out.println("a"); //错误，没有赋值
  System.out.println("b"); //错误，没有赋值
  System.out.println("c");
}
```

4. Java是强类型的语言

5. 同一个范围内不能出同名的变量

```Java
public static void main(String[] args) {
  char c = 'A';
  System.out.println(c);

  c = 'B';
  System.out.println(c);

  //将Unicode字符集中第97个位置的字符赋值给变量c
  c = 97;
  System.out.println(c);
}
```

## 四、标识符

中文也可以作为标识符，但不建议使用。

1. 标识符由字母、数字、下划线、美元符组成。
2. 不能使用数字开头。
3. 不能使用关键字(Java中所有关键字均为小写)。
4. true、false、null三个不是关键字，只是Java中特殊的值。

## 五、基本数据类型的类型转换

1. 如何比较基本数据类型的大小

* 先比较精度，精度大的为大类型，精度小的为小类型
* 如果精度相同，再比较字节数

2. 小类型可以自动转换为大类型

3. 大类型必须手动转换（强制转换）才能赋给小类型

* 手动转换的格式：`(需要转换的类型)数据/变量;`

4. 为变量赋<font color="red">值(不能是变量)</font>时，如果在类型的取值范围内时，JVM会自动进行类型转换

```Java
public static void main(String[] args) {
  double salary = 5000;
  System.out.println(sasalary);

  int num = (int)100.25;
  System.out.println(num);

  short s = 100; //正确，JVM会自动进行类型转换

  s = num; //错误，需要类型转换
  System.out.println(s);
}
```

5. 输入与输出数据

* 输入数据：使用`Java.util.Scanner`类。Scanner可以接收数据

```Java
public static void main(String[] args) {
  //声明Scanner类型变量，用于接收键盘中的数据
  Scanner input = new Scanner(System.in);
  System.out.print("请输入用户编号：");
  //程序会暂停并等待用户在键盘中输入的整数，以回车符作为结束标记
  int userId = input.nextInt();
  System.out.print("请输入用户姓名：");
  //程序会暂停并等待用户在键盘中输入的字符串，以回车符作为结束标记
  String userName = input.next();

  System.out.println("你的编号为："+userId);
  System.out.println("你的姓名为："+userName);
  input.close();
}
```

* 输出数据

 `System.out.println()`与`System.out.print()`方法的区别：`System.out.println()`输出数据并换行。括号内可以没有参数；`System.out.print()`输出数据不换行，括号内必须有参数
 `System.out.printf()`：当输出的数据需要进行大量连接时，建议使用

 ```Java
 public static void main(String[] args) {
   //声明Scanner类型变量，用于接收键盘中的数据
   Scanner input = new Scanner(System.in);
   System.out.print("请输入用户编号：");
   //程序会暂停并等待用户在键盘中输入的整数，以回车符作为结束标记
   int userId = input.nextInt();
   System.out.print("请输入用户姓名：");
   //程序会暂停并等待用户在键盘中输入的字符串，以回车符作为结束标记
   String userName = input.next();

   System.out.printf("你的编号为%d,你的姓名为%d",userId,userName);
   input.close();
 }
 ```

## 六、数组

1. 数组是Java中集合的一种类型
2. Java中的数组均为引用数据类型
3. 数组是一组相同数据类型的集合
4. 一维数组

* 声明一维数组：在栈内存中开辟一个空间，用于保存数组的名字。声明数组时不能置顶数组的长度。

```Java
  int[] array; //推荐使用
  double array1[];
```

* 创建一维数组：在堆内存中开辟连续空间，用于保存数据的内容。创建数组时必须指定数组的长度。

```Java
//创建数组并赋值
  int[] array = {10,20,30};
//创建数组，但并没有赋值
double array1 = new double[10];
//通常用于重新为数组赋值
String[] array2 = new String[]{"AB"."CD","123"};
```

*<b>基本数据类型和引用数据类型的区别：

* 基本数据类型栈内存中保存的是值。
* 引用数据类型栈内存中保存的是引用。</b>

```java
  int num = 200;
  System.out.println(num);

  int[] array = {10,20,30};
  System.out.println(array);
```

* 通过下标访问/设置数组中的元素
* Java中数组的下标从0开始，最大的下标为数组长度减1
* 通过数组的.length属性获得数组的长度

```Java
public static void main(String[] args) {
  int num = 200;
  System.out.println(num);

  int[] array = {10,20,30};
  System.out.println(array);
  System.out.println(array[0]);
  System.out.println(array[1]);
  System.out.println(array[2]);
  System.out.println(array.length);
}
```

* 数组的默认值

  byte,short,int默认为0

  long默认为0L

  double默认为0.0

  float默认为0.0F

  char默认为'\u0000'

  boolean默认为false

  引用数据类型默认为null

* 数组的长度可以为0，但不能为负数，否则运行时会抛出异常
* 创建数组时，数组的长度可以是变量
* 数组的长度确定后，长度不能改变

5. 二维数组：Java中的多维数组都是由一维数组构成的

* 声明二维数组

```java
  int[][] array;//推荐使用
  double array1[][];
  String[] array2[];
```

* 创建二维数组

```java
  public static void main(String[] args) {
    int[][] array={{10,20},{30,40},{50,60}}; //推荐使用
    double array1[][] = new double[10][10];
    //创建多维数组时，高维不能省略，低维可以省略
    String[] array2[] new String[3][];
    //输出数组的“行数”
    System.out.println(array2.length);
    array2[0] = new String[1];
    array2[1] = new String[2];
    array2[2] = new array2[3];
  }
```

```Java
  //声明两个一维数组
  int[] a,b;
  a = new int[10];
  b = new int[10];
  //声明了一个一维数组与一个二维数组
  int[] a1,b1[];
  a1 = new int[10];
  b1 = new int[10][10];
  //声明了一个一维数组与一个int型的变量
  int x[],y;
  x = new int[10];
  y = 100;
```

# 运算符

## 一、算术运算符：+，-，*，/，%，++，--

* 算术运算结果的类型：

1. 当参与运算的元素类型相同时，运行结果的类型一定与参与运行的元素类型相同
2. 当参与运算的元素类型不同时，运行结果的类型一定与大类型元素的类型相同

* `short s = 1;s = s + 1;`是否存在错误。为什么？
* 存在错误。因为`s + 1`的结果为int类型，无法直接赋值给short类型的变量s。应该改为`s = (short)(s + 1);`

3. ++ / --

* ++/--可以出现在变量的前/后面
* 无论++/--出现在前/后面，当代码执行后变量一定会加1或减1

```java
  int x = 100;
  x++;
  System.out.println(x);

  ++x;
  System.out.println(x);
```

* ++/--出现在变量后面时，先取值，再运算。
* ++/--出现在变量前面时，先运算，再取值。

```Java
  int x = 100;
  int y = x++;
  //int y = x;
  //x = x - 1;
  System.out.println(y);

  y = ++x;
  //x = x + 1；
  //y = x;
  System.out.println(y);
```

## 二、比较运算符：>，>=，<，<=，==，!=

1. 比较运算的结果一定为boolean类型
2. java中不是所有的数据类型都可以进行比较运算。如boolean不能与其他类型进行比较运算。

## 三、逻辑运算符：&，|，&&，||

<table>
  <tr><td colspan = "3"><与运算（并且）</td></tr>
  <tr><td>元素1</td><td>元素2</td><td>元素3</td></tr>
  <tr><td>T</td><td>T</td><td>T</td></tr>
  <tr><td>T</td><td>F</td><td>F</td></tr>
  <tr><td>F</td><td>T</td><td>T</td></tr>
  <tr><td>F</td><td>F</td><td>F</td></tr>
</table>

<table>
  <tr><td colspan = "3">或运算（或者）</td></tr>
  <tr><td>元素1</td><td>元素2</td><td>元素3</td></tr>
  <tr><td>T</td><td>T</td><td>T</td></tr>
  <tr><td>T</td><td>F</td><td>T</td></tr>
  <tr><td>F</td><td>T</td><td>T</td></tr>
  <tr><td>F</td><td>F</td><td>F</td></tr>
</table>

* 逻辑运算结果一定为boolean类型
* 逻辑与(&)/逻辑或(|)

1. 逻辑与：当第一个表达式为false时，仍然会执行第二个表达式，再返回false，效率不高，安全性差
2. 逻辑或：当第一个表达式为true时，仍然会执行第二个表达式，再返回true，效率不高，安全性差

* 短路与(&&)/短路或(||)

1. 短路与：当第一个表达式为false时，不执行第二个表达式直接返回false。效率高，安全性高。
2. 短路或：当第一个表达式为true时，不执行第二个表达式直接返回true。效率高，安全性高。

* !：取反

```Java
  String s1 = "abc";
  String s2 = "abc";
  //判断两个字符串是否相等
  System.out.println(s1.equals(s2));
  //判断两个字符串是否不相等
  System.out.println(!s1.equals(s2));
```

## 四、赋值运算符：+=，-=，*=。/=，%=。可以自动转换结果的类型

* `short s = 1;s+=1;`是否存在错误，为什么？
* 不存在错误，+=会自动转换结果的类型。

## 五、三元运算符

1. 格式：`X?Y:Z`
2. 当X为true时返回Y的值，当X为false返回Z的值。

```java
  Scanner input = new Scanner(System.in);
  System.out.print("请输入一个整数：");
  int num = input.nextInt();
  System.out.println((num % 2 == 0) ? "偶数" :"奇数");
  input.close();
```

# 程序的结构

## 一、程序结构

1. 顺序结构
2. 选择结构
3. 循环结构

## 二、选择结构

1. if语句

```java
  if(条件){
      //代码
  }else if(条件){
      //代码
  }else if(条件){
      //代码
  }else{
      //代码
  }
```

2. if语句中条件结果的类型一定为boolean类型
3. 一个if语句中可以出现0个或多个else if块
4. 一个if语句中可以出现0个或一个else块
5. else必须出现在if语句的最后
6. 当if语句匹配到一个分支后，不再匹配其他的分支
7. if语句的大括号可以省略，如果省略if语句，作用范围只有一行代码

```java
  public static void main(String[] args) {
    Scanner input = new Scanner(System.in);
    System.out.print("请输入一个整数：");
    int num = input.nextInt();

    if(num % 2 == 0){
      System.out.printf("%d是偶数",num);
    }else{
      System.out.printf("%d是奇数",num);
    }
    input.close();
  }
```

8. 接收用户输入的两个整数，再以升序方式输出

```java
  public static void main(String[] args) {
    Scanner input = new Scanner(System.in);
    System.out.print("请输入第一个整数：");
    int num1 = input.nextInt();
    System.out.print("请输入第二个整数：");
    int num2 = input.nextInt();
    if(num1 > num2){
      //使用第三个变量交换两个变量的值
      int num3 = num1;
      num1 = num2;
      num2 = num3;
    }
    System.out.println(num1 + "\t" + num2);
    input.close();
  }
```

9. 如何不使用第三个变量交换两个整数变量的值

```
  int x = 200;
  int y = 100;
  x = x + y;
  y = x - y;
  x = x - y;
```

```java
  public static void main(String[] args) {
    Scanner input = new Scanner(System.in);
    System.out.print("请输入第一个整数：");
    int num1 = input.nextInt();
    System.out.print("请输入第二个整数：");
    int num2 = input.nextInt();
    if(num1 > num2){
      //不使用第三个变量交换两个变量的值
      num1 = num1 + num2;
      num2 = num1 - num2;
      num1 = num1 - num2;
    }
    System.out.println(num1 + "\t" + num2);
    input.close();
  }
```

10. switch语句

```java
  switch (变量) {
    case 值:
      //代码
    case 值：
      //代码
    ……
    default:
      //代码
  }
```

* switch中的变量只能为byte，short，char，int。从JDK1.5开始可以使用枚举类型。从JDK1.8开始可以开始使用String类型。
* case后面的值不能重复。
* case后面只能为字面值或表达式或常量。
* 当swtich匹配到一个分支后，会从此分支开始自顶向下执行所有的分支，直到switch的结束或遇到第一个break为止。
* default可以出现在switch的任意位置。
* 无论default出现在哪，switch都会先匹配所有的case分支。当没有匹配到任何case后，switch才会匹配default分支。

```java
public static void main(String[] args) {
  Scanner input = new Scanner(System.in);
  System.out.print("请输入月份：");
  int month = input.nextInt();

  switch (month) {
    default:
      System.out.println("月份不正确");
      break;
    case 1:
    case 3:
    case 5:
    case 7:
    case 8:
    case 10:
    case 12:
      System.out.printf("%d月有31天",month);
      break;
    case 4:
    case 6:
    case 9:
    case 11:
      System.out.printf("%d月有30天",month);
      break;
    case 2:
      System.out.printf("%d月有28天",month);
      break;
  }
  input.close();
}
```

## 三、循环结构

1. while循环：不确定循环次数时，建议使用while循环。

```java
  while(循环条件){
      //循环体
  }
```

* 循环条件必须为boolean类型
* while循环的大括号可以省略，如果省略，作用范围只有一行代码。

2. do...while循环

```java
  do {
    //循环体
  } while (循环条件);
```

* while与do...hwile的区别：
  * while循环：先判断，再循环
  * do...while循环：先循环，再判断

3. for循环：当确定循环次数时，建议使用for循环

```java
  for(循环变量初始化;循环条件;循环变量自增/自减){
    //循环体
  }
```

* for循环的三部分都可以省略
* 在循环中声明的变量，只能在循环内使用，在循环外不能访问
**for循环工作步骤：**

```java
  for(int i = 0; i < 4 ; i++){
    System.out.println(i);
    /*
    * 第一次循环：执行第一部分。声明循环变量i=0
                 再执行第二部分判断i<4，返回true。进入循环输出0
    * 第二次循环：执行第三部分i++。i=1
                 再执行第二部分判断i<4，返回true。进入循环输出1
    * 第三次循环：执行第三部分i++。i=2
                 再执行第二部分判断i<4，返回true。进入循环输出2
    * 第四次循环：执行第三部分i++。i=3
                 再执行第二部分判断i<4，返回true。进入循环输出3
    * 第五次循环：执行第三部分i++。i=4
                 再执行第二部分判断i<4，返回false循环结束。
    */
  }
```

* for循环的第一部分可以声明多个类型相同的变量。
* for循环的大括号可以省略，如果省略作用范围只有一行代码。

4. `Math.random()`：返回大于等于0.0，但一定小于1.0的double类型的随机数

```java
  public static void main(String[] args) {
    //接收用户输入的整数，输出指定数量的1-100之间的随机数
    Scanner in = new Scanner(System.in);
    System.out.println("请输入产生随机数的数量：");
    int count = in.nextInt();
    //用于保存最大的随机数
    int max = 0;
    //用于保存每次生成的随机数
    int temp = 0;
    //用于保存最小的随机数
    int min = 101;
    //用于保存总和
    int sum = 0;
    for(int i = 1 ; i <= count; i++){
      //接收生成的随机数
      temp = (int)(Math.random() * 100 + 1);
      sum += temp;
      System.out.print(temp + "\t");
      if (max < temp) {
          max = temp;
      }
      if (min > temp) {
          min = temp;
      }
      if ( i % 5 == 0) {
        System.out.println();
      }
    }
    System.out.println("\n最大值为：" + max);
    System.out.println("最小值为：" + min);
    System.out.println("总和为：" + sum);
    in.close();
  }
```

5. break与continue

* break
  * break不能单独使用，只能出现在switch或循环语句中
  * break在循环中的作用：立即结束所在循环

  ```java
  //用于保存找到满足条件整数的个数
  int count = 0;
  for (int i = 1 ; i<=1500 ; i++) {
    if((i % 3 == 2)&&(i % 5 ==3)&&(i %% 7 ==2)){
      System.out.println(i);
      count++;
      if(count == 5){
        break;
      }
    }
  }
  ```

* continue
  * continue不能单独使用，只能出现在循环语句中。
  * continue的作用：使所在循环立即结束本次循环，直接执行下一次循环

```java
  public static void main(String[] args) {
  for (int i = 1 ; i <= 100 ; i++) {
    if(i % 3 != 0){
      continue;
    }
    System.out.println(i);
}
```

# 类与对象

## 一、java是面向对象的语言

## 二、面向对象的特征：封装、继承、多态、抽象

## 三、类(class)

1. 成员变量(属性、字段、全局变量、域、属性域)
2. 成员变量的作用：用于描述类的特征
3. new关键字的作用：在堆内存中开辟空间，创建类的实例（对象）
4. 成员变量只能通过对象调用
5. 成员变量有默认值，与数组的默认值保持一致

```java
  public class Test{
      public static void main(String[] args) {
        int num = 100;
        System.out.println(num);
        人 p = new 人();
        p.姓名 = "张三";
        p.年龄 = 25;
        p.性别 = "男";

        人 p1 = new 人();
        p1.姓名 = "赵四";
        p1.年龄 = 30;
        p1.性别 = "男";

        System.out.println(p.姓名);
        System.out.println(p1.姓名);

        人 p2 = new 人();
        System.out.println(p2.姓名);

        人 p3 = null;
        System.out.println(p3.姓名);  
      }
  }
```

```java
  public class 人{
    String 姓名;
    int 年龄;
    String 性别;
  }
```

6. 成员变量(全局变量)与局部变量的区别？
<table>
    <tr>
        <td>区别</td>
        <td>局部变量</td>
        <td>局部变量</td>
    </tr>
    <tr>
        <td>声明位置</td>
        <td>方法或块内部</td>
        <td>方法外类内部</td>
    </tr>
    <tr>
        <td>访问权限修饰符</td>
        <td>没有访问权限</td>
        <td>有访问权限</td>
    </tr>
    <tr>
        <td>默认值</td>
        <td>没有默认值</td>
        <td>有默认值</td>
    </tr>
    <tr>
        <td>使用形式</td>
        <td>直接使用</td>
        <td>对象调用</td>
    </tr>
    <tr>
        <td>作用域</td>
        <td>在方法或语句块内部</td>
        <td>整个类</td>
    </tr>
    <tr>
        <td>生命周期</td>
        <td>进入方法或语句块/创建退出方法或语句块销毁</td>
        <td>随着对象的创建而创建/随着对象的销毁而销毁</td>
    </tr>
</table>
7. `java.lang.NullPointerException`：空对象异常。因为引用类型的变量没有指向堆内存中任何对象。所以此时不能通过变量调用对象的属性或方法，否则运行时抛出异常。
8. 成员方法(方法、函数)

* 成员方法的作用：用于描述类的动作或行为
* 成员方法的基本格式

  ```java
  访问权限 返回类型 方法名([参数列表]){
    //方法体
  }
  ```

9. 当方法没有返回类型时，使用void关键字表示
10. 形参：在方法声明中的参数
11. 实参：在调用方法时传递的参数
12. 方法重载：在类中存在多个名字相同，但参数不同的方法。这些方法称为方法的重载。

* 参数不同：个数不同，类型不同，顺序不同
* 方法的重载只与方法名和参数列表有关，与其它元素无关

  ```java
  public class Person{
    String name;
    int age;
    public void run(int count){
      for(int i = 1; i <= count ; i++){
        System.out.println(name + "跑了第" + i + "圈");
      }
    }
    public void sum(int num1, double num2){
      System.out.println(num1 + num2);
    }
    public void sum(double num1, int num2){
      System.out.println(num1 + num2);
    }
  }
  ```

  ```java
    public class Test{
      public static void main(String[] args) {
        Person p = new Person();
        p.name = "张三";
        p.age = 20;

        Person p1 = new Person();
        p1.name = "赵四";
        p1.age = 30;

        p.run(10);
        p1.run(3);

        p.sum(100,200); //错误：因为找到了多个可以调用的方法
      }
    }
  ```

13. return关键字

* 返回数据
* 结束方法
* 当方法没有返回类型时，也可以使用return关键字结束方法，但不能返回数据

14. 构造方法（构造器、构造函数）

* 构造方法的特征
  * 构造方法的名字必须与类名保持一致
  * 构造方法一定没有返回类型，并且不能使用void关键字修饰
* 普通方法的名字也可以与类名相同
* 当没有在类中书写构造方法时，JVM会自动为类添加默认的构造方法
* 类一定有构造方法
* 默认构造方法的格式：

  ```java
  访问权限与类型相同 构造方法名(){

  }
  ```

* 当在类中书写了构造方法时，JVM便不再会为类添加默认的构造方法
* 构造方法的作用：为类的成员变量初始化
* 通常情况下，构造方法只能在new关键字后面调用。一个对象的构造方法不能重复调用
* 普通方法可以通过类的对象重复调用
* 构造方法可以重载

15. static关键字

* 修饰成员变量：使用static修饰的成员变量称为静态变量（类变量）。不使用static修饰的成员变量称为实例变量。类所有的对象共用一份静态变量。静态变量只有第一次使用类时声明并初始化。而实例变量每次创建对象时都会声明并初始化。
* 修饰成员方法：使用static修饰的成员方法称为静态方法（类方法）。静态方法只能直接调用当前类中静态的成员。静态方法中不能使用this与super关键字
* 静态成员可以通过雷类名（接口名）直接调用，也可以通过对象调用（不推荐）

```java
  public int User{
      static int userId;
      String userName;
      public User(){

      }
      public User(int id, String name){
        userId = id;
        userName = name;
      }
      public void print(){
        System.out.println(userId + "\t" + userName);
      }
  }
```

```java
  public class Test{
    public static void main(String[] args) {
      User user = new User(100,"AA");
      User user1 = new User(200,"BB");

      user.print();
      user1.print();
    }
  }
```

* 块（初始化块）：在类中的一对大括号
  * 块中可以出现普通Java代码
  * 创建对象时，JVM会执行块中的代码
  * 块在构造方法之前调用
* 静态块（静态初始化块）：static修饰的块
  * 静态块中只能调用当前类中静态的成员
  * 当第一次使用类时，执行静态块中的代码
* 请写出静态变量、实例变量、静态初始化块、初始化块以及构造方法的加载顺序
  * 静态变量（只有第一次使用类时加载）
  * 静态初始化块（只有第一次使用类时加载）
  * 实例变量（每次创建对象时）
  * 初始化块（每次创建对象时）
  * 构造方法（每次创建对象时）
* 封装
  * 通常情况下，类的成员变量(属性)设置为private
* 根据需求，为private的成员变量提供public的getter或setter方法
* this关键字：引用当前类的成员（成员变量或成员方法）
*可变长参数（可变参数）
  * 格式：`数据类型...参数名`
  * 可变长参数的本质：一维数组
  * 可变长参数只能用于声明形参，不能用于声明变量
  * 优点：简化传递数组时的代码
  * 当方法有多个参数时，可变长参数只能出现在最后

```java
  public class Test{
      public static void main(String... args) {
        Test t = new Test();
        //创建长度为0的数组
        int[] array = [];
        t.method(array);
        //创建长度为1的数组
        array = new int[]{100}
        t.method(array);
        //创建长度为3的数组
        array = new int[] {100,200,300};
        t.method(array);

        //传递可变长参数
        t.method1();
        t.method1(1000);
        t.method1(1000,2000,3000);
      }
      public void method1(int... array){
        if(array == null || array.length == 0){
          return;
        }
        System.out.println("**********");
        for(int i = 0 ; i < array.length; i++;){
          System.out.println(array[i] + "\t");
        }
        System.out.println("**********");
      }
      public void method(int[] array){
        if(array == null || array.length == 0){
          return;
        }
        System.out.println("**********");
        for (int i = 0; i < array.length[i]; i++) {
          System.out.println(array[i] + "\t");
        }
        System.out.println("\n**********");
      }

  }
```

* 包(package)
  *包的本质：文件夹（目录）
  *包的作用：解决类重名的问题；管理类
  * 当类位于包中时，类的首行必须为package语句（注释除外）
  * 类可以直接使用同包中的类
  * 当使用其他包中的类时，必须使用import语句导入类（导包）
  * java.lang包中的元素JVM会自动导入，不再需要手动使用import语句导入，可以直接使用
  * 直接创建在eclipse的src(default package)中的类，无法使用import语句导入
* 访问权限：java只有四种访问权限
<table>
    <tr>
        <td>类本身</td>
        <td>同包的类</td>
        <td>非同包的子类</td>
        <td>非同包的非子类</td>
        <td></td>
    </tr>
    <tr>
        <td>private</td>
        <td>Y</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
    </tr>
    <tr>
        <td>默认（友好）</td>
        <td>Y</td>
        <td>Y</td>
        <td>N</td>
        <td>N</td>
    </tr>
    <tr>
        <td>protected</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>N</td>
    </tr>
    <tr>
        <td>public</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
    </tr>
</table>

  * 类(顶层类)只能使用public或默认访问权限修饰。
  * 请写出默认权限与protected权限哪个权限大？为什么？
    * protected权限大。
    * 默认权限只有类本身与同包中的类可以访问。而protected不仅类本身与同包中的类可以访问，其它包中的子类也可以访问。
* 类之间的关系
  * 继承：A is B
  * 依赖：A has B
  * 聚合：C = A + B

* 类与对象的区别
  * 类是模板
  * 对象是类的具体实现

# 子类与继承

## 一、继承的优点

1. 提高代码重用性。
2. 降低维护的成本。

## 二、Java使用extends关键字描述继承关系

## 三、 子类可以继承父类中所有的成员变量与成员方法

## 四、 子类可以继承父类private的成员，但无法使用

## 五、 子类不能继承父类的构造方法

## 六、 方法的重写(方法的覆盖)

1. 重写的方法要与被重写的方法具有相同的方法名、参数列表、返回类型。
2. 重写方法的访问权限大于等于被重写方法的访问权限。
3. 重写方法抛出的异常小于等于被重写方法抛出的异常。
4. static不能产生重写。

## 七、super关键字

1. 引用父类中的成员。最常用的情况：在子类中引用父类同名的成员。
2. 默认情况下，子类会在自己构造方法的第一行默认使用super()调用父类无参的构造方法。
3. 当父类没有无参的构造方法，子类必须使用super()调用父类有参数的构造方法，否则编译失败。

## 八、Java是单继承：一个类只能有一个父类

## 九、final关键字

1. 修饰变量：常量，只能赋值一次。
2. 修饰形参：在方法运行的过程中，final修饰的形参是只读的。
3. 修饰方法：方法不能被子类重写。
4. 修饰类：类不能被继承。

## 十、请写出阻止类被继承有几种方法？

1. 使用final修饰类。
2. 使用private修饰类的构造方法。(子类会在自己构造方法的第一行调用父类的构造方法，如果父类的构造方法是private，子类就无法调用父类的构造方法)。

## 十一、对象的上转型对象(引用数据类型的类型转换)

1. 如何比较引用数据类型的大小。

* 父类大，子类小。

2. 当两个类没有继承关系时，不能相互转换。
3. 子类可以直接赋给父类。(父类的引用指定子类的对象，永远是安全的)。
4. 父类必须手动转换(强转)才能赋给子类。
5. 当父类引用指向的对象，不是需要的子类类型时，运行时抛出异常。
6. `java.lang.ClassCastException`：运行时，引用数据类型转换失败的异常。

## 十二、 多态

1. 运行时变量有多种状态。
2. 多态在编译时，只能看到父类的成员。
3. 多态时调用的成员变量，一定是父类的。
4. 多态时调用的方法：

* 如果子类没有重写父类的方法，调用仍然是父类的方法。
* 如果子类重写了父类的方法，程序运行时，方法的指针会动态的从父类绑定到子类的方法(方法的动态绑定)。调用子类的方法。

```java
  package com.test;
  public class Test{
    public static void main(String[] args) {
      User user1 = new User();
      user1.setUserId(100);
      user1.setUserName("AA");

      User user2 = new User();
      user2.setUserId(100);
      user2.setUserName("AA");

      int x = 100;
      int y = 100;
      System.out.println(x == y);
      System.out.println(user1 == user2);
      System.out.println(user1.equals(user2));
    }
  }
  ```

  ```java
  package com.test;

  import java.util.Objects;
   public class User{
  private int UserId;
  private String userName;

  public int getUserId() {
  return UserId;
 }
 public void setUserId(int userId) {
  UserId = userId;
 }
 public String getUserName() {
  return userName;
 }
 public void setUserName(String userName) {
  this.userName = userName;
 }
  public int hashCode(){
    return Objects.hash(userId);
  }
  public boolean equals(Obeject obj){
    if(this == obj)
      return true;
    if(obj == null)
      return false;
    if( getClass() != obj.getClass())
      return false;
    User other = (User)obj;
    return userId == other.userId;
  }
 }
```

# 抽象与接口

## 一、抽象(abstract)

1. 修饰类：抽象类。抽象类不能实例化(不能new)。只能创建抽象类子类的对象。抽象类虽然不能创建对象，但抽象类仍然有构造方法。
2. 修饰方法：抽象方法。抽象方法只有方法的声明，没有方法的实现。抽象方法所在的类必须是抽象类。普通方法可以调用当前类中抽象方法。

* 如果抽象类的子类不是抽象类，子类必须重写父类中所有的抽象方法。
* 如果抽象类的子类是抽象类，子类可以不重写父类中的抽象方法或只重写父类部分的抽象方法。
* 修饰接口
* abstract不能与哪些关键字一起使用？
  * private、static、final
  **抽象方法：只有方法头，没有方法体定义，也就是说抽象方法无需实现，抽象方法的意义在于子类实现，private意义在于其他类直接调用它已实现的方法。这两者搭配毫无意义(private修饰后为私有，子类不能继承，自然不能使用)；
  final用于类名前，表示类不可被继承；final用于变量前，表示它是只能一次赋值的变量，如果初始化了那就是常量，也不可被改变。和abstract 搭配无意义(final不能被重写，根本就不可能被abstract的实现类重写)
  static修饰的是静态方法，可以直接被类调用；而abstract修饰的类中只有方法名，无方法体，不能被直接调用，故不能同时修饰一个类或方法。*

## 二、接口(interface)

1. 接口的作用：使Java可以实现多继承。
2. 接口不是类，接口与Object类没有关系。
3. 接口是由一组常量与抽象方法的集合

* 常量：接口中的常量一定是public static final。使用static final修饰的常量必须在声明初始化。
* 抽象方法：接口中的方法一定是public abstract。
* 类可以实现(implements)接口
* 当类实现接口时：
  * 如果类不是抽象类，类必须重写接口中所有的抽象方法。
  * 如果类是抽象类，类可以不重写接口中的抽象方法或只重写接口中部分的抽象方法。
* 接口不能实例化(不能new)。只能创建接口实现类的对象。
* 一个类可以实现多个接口。
* 接口与接口之间的关系：
  * 接口之间的关系是继承(extends)
  * 一个接口可以继承多个接口。

# 异常与内部类

## 一、Java中异常的结构

1. java.lang.Throwable类：是Java中所有错误与异常的父类。
2. java.lang.Error类：是编写代码时不应该捕获的严重的问题。
3. java.lang.Exception类：是编写代码时应该捕获与处理的问题。
4. 非运行时异常：在编写代码必须处理的异常，否则程序无法编译。
5. java.lang.RuntimeExcetion类及其子类：在编写代码时可以不捕获或处理的异常，但运行时程序可能会抛出异常。

## 二、try..catch..finally

```java
try{
 // 可能发生异常的代码
}catch(异常类型){
 // 处理异常的代码
}finally{
 // 一定执行的代码
}
```

1. try块不能单独使用，必须与catch或finally一起出现。
2. 一个try语句中可以出现0个或N个catch块。
3. 当try块中的代码发生异常时，try块中的代码会中止运行。程序会跳转到对应的catch块中处理异常。
4. 可以使用Exception在catch块中捕获所有的异常。
5.  Exception必须出现在最后一个catch块中。
6.  无论程序是否抛出异常，finally块中的代码一定会执行。
7.  工作中不建议在finally块中出现return语句，因为此时try块与catch块中的return语句将全部失效。

## 三、 throw与throws关键字的区别？

1.  throw：在方法体的内部手动抛出一个异常。
2.  throws：在方法声明的最后说明调用此方法时，方法可能会发生哪些异常。

## 四、 创建自定义异常类：使类继承Exception或Exception的子类

## 五、 方法重写与异常

1. 父类方法抛出1个或多个异常，子类重写的方法可以抛出0个异常。
2. 如果子类重写的方法也抛出了异常。必须抛出与父类方法相同的异常，或父类方法抛出异常的子异常。

## 六、 构造方法与异常

1. 构造方法也可以使用throws说明抛出哪些异常。
2.如果父类构造方法使用throws抛出了异常，子类的构造方法必须抛出与父类相同或更大的异常。

## 七、 内部类：一个类内部创建的类。内部类可以使用所有的访问权限修饰，而外部类(顶层类)只能使用public与默认的访问权限修饰

1. 实例内部类：可以直接使用外部类所有的成员(包括private的成员)。

```java
  OuterClass outer = new OuterClass();
  OuterClass.InnerClass inner = outer.new InnerClass();
  inner.method();
```

2. 静态内部类：使用static修饰的内部类。外部类(顶层类)不能使用static修饰。静态内部类只能直接调用外部类静态的成员。
`OuterClass.StaticClass sclass = new OuterClass.StaticClass();`
3. 匿名内部类
4. 局部内部类：在方法中创建的内部类。不能使用访问权限修饰，可以直接使用方法中的局部变量（在局部内部类之前声明的局部变量）

# 常用类

## 一、包装类(装箱类)：8个，对应8个基本数据类型

1. Byte,Short,Long,Float,Double,Boolean,Integer,Character
2. 包装类提供了相关类型常用的属性与方法。
3. 包装类提供了parseXXX()方法用于将String转换为对应的基本数据类型。

4. 装箱与拆箱

* 装箱：将基本数据类型转换为包装类。
* 拆箱：将包装类转换为基本数据类型。
* 从JDK1.5开始，可以自动装箱与拆箱。
* 自动装箱与拆箱只会简化代码，但不会提高代码执行的效率。

## 二、日期相关的常用类

1. `java.util.Date`类：用于获得创建date对象的日期与时间。也可以用于两个日期的比较。

```java
  Date date = new Date();
  System.out.println(date);
  //返回1970-1-1 00:00:00到创建对象之间的毫秒数，返回类型long
  System.out.println(date.getTime());

  Date date1 = new Date();
  System.out.println(date.after(date1));
  System.out.println(date.equals(date1));
  System.out.println(date.before(date1));
```

2. `java.util.Calendar`类：抽象类。日历类。可以获得日期详细的信息。还可以用于日期的加减。

```java
  //获得Calendar子类的对象
  Calendar c = Calendar.getInstance();
  System.out.println(c.get(Calendar.YEAR));
  //java中的月份从0开始
  System.out.println(c.get(Calendar.MONTH) + 1);
  System.out.println(c.get(Calendar.DATE));
  System.out.println(c.get(Calendar.DAY_OF_WEEK));
  System.out.println(c.get(Calendar.DAY_OF_YEAR));

  //日期的加与减
  c.add(Calendar.MONTH, 100);
  System.out.println(c.get(Calendar.YEAR));
  System.out.println(c.get(Calendar.MONTH) + 1);
  System.out.println(c.get(Calendar.DATE));
```

3. `java.text.DateFormat`类及其子类：常用于Date与String类型的转换。

```java
  public class Test{
    public static void main(String[] args) {
      Date date = new Date();
      // SHORT,DEFAULT.LONG,FULL
      DateFormat format = DateFormat.getDateInstance(DateFormat.DEFAULT);
      //将Date转换为String
      String birthday = format.format(date);
      System.out.println(birthday);

      String s = "2020-10-1"
      //String转Date
      try{
        date = format.parse(s);
        System.out.println(date);
      }catch(ParseException e){
        System.out.println("日期格式不正确");
      }

      //------------------------------------
      Date date1 = new Date();
      SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
      //将Date转换为String
      String birthday1 = sdf.format(date1);
      System.out.println(birthday1);

      String s1 = "2020-10-1 10:21:36"
      try {
        //将String转换Date
        date1 = sdf.parse(s1);
        System.out.println(date1);
      } catch(ParseException e) {
        System.out.println("日期格式不正确");
      }
    }
  }
```

4. 大数字

* `java.math.BigInteger`：大整数。
* `java.math.BigDecimal`：大浮点数。进行浮点数运算时没有误差。

```java
  BigDecimal num1 = new BigDecimal("776543134848632135445465456577567434534.3234243534556464645");
  BigDecimal num2 = new BigDecimal("123456734893478356794274064823789467023.24749824724873458357");
  BigDecimal num3 = new BigDecimal(2);

  System.out.println(num1.add(num2)); //加
  System.out.println(num1.substract(num2)); //减
  System.out.println(num1.multiply(num2)); //乘
  System.out.println(num1.divide(num3)); //除

```

5. 字符串

* ```java
  String s = "abc";
  System.out.println(s);

  s = "def";
  System.out.println(s);

```
* String是不可变的字符序列，每次对String的修改都会产生新的String对象。如果需要大量修改字符串时，不建议使用String类型。
* String重写了Object类中的equals()方法，用于判断字符串的内容是否相等
```java
  String s1 = "abc";
  String s2 = "abc";
  String s3 = new String("abc");

  System.out.println(s1 == s2); //返回true
  System.out.println(s1 == s3); //返回false
  System.out.println(s1.equals(s2)); //返回true
  System.out.println(s1.equals(s3)); //返回true
```

* String s = new String(“abc”);这行代码创建了几个String对象？
创建了两个String对象。
* String是不可变的字符序列，所以String的方法不会改变自身的内容。

5. foreach循环：JDK1.5开始出现。

```java
  for(数据类型 变量名 : 集合名){
  // 循环体
}
```

* foreach循环的作用：遍历集合。
* foreach循环中没有下标，所以通常只能用于从集合中取数据，而不能向集合中添加数据。

6. `java.lang.StringBuffer`与`java.lang.StringBuilder`

* 都是final的类。
* StringBuffer与StringBuilder都是可变的字符序列。
* 每次对StringBuffer与StringBuilder的修改不会产生新的字符串对象，所以如果需要大量修改字符串时，建议使用StringBuffer或StringBuilder。
* StringBuffer与StringBuilder的区别？
  * StringBuffer是线程安全的。
  * StringBuilder是线程不安全的，所以StringBuilder效率更高，更推荐使用。
  * StringBuffer与StringBuilder是可变的字符序列，所以它们的方法会改变自身的内容。
  * StringBuffer与StringBuilder没有重写Object类中equals()方法，StringBuffer与StringBuilder不能使用equals()方法判断内容是否相等。

## 三、 泛型

1. 格式：`<泛型名>`
2. 泛型的作用：后期绑定数据类型。
3. 泛型只能使用引用数据类型。
4. 泛型的约束条件：
5. 如果没有设置泛型，泛型默认为Object类型。

## 四、 常用集合

1. 常用集合的结构

* `java,util.Collection`接口
  * `java.util.Set`接口
  * `java.util.List`接口
* `java.util.Map`接口
  * Map接口的实现类

2. 常用集合的特点(区别)。

* Set集合：不能保存重复值，不能保存元素加入的顺序。
* List集合：可以保存重复值，可以保存元素加入的顺序。
* Map集合：保存一个键(Key)值(Value)对。键不能重复，值可以重复。

3. Set集合：集合内元素是排序的，所以每次输出集合的数据时顺序的固定的。

* TreeSet：集合内的元素以升序排序。
* HashSet：集合内的元素根据哈希值进行排序。

```java
    public class TestSet{
    public static void main(String[] args) {
      Set<Integer> set = new HashSet<>();
      set.add(700);
      set.add(200);
      set.add(500);
      set.add(400);
      set.add(300);
      set.add(100);
      set.add(200);
      //遍历Set集合的两种方式
      //一、使用迭代器
      //将Set集合中所有的元素存入迭代器中
      Interator<Integer> it = set.iterator();

      //遍历迭代器
      //hashNext()：判断迭代器下一个位置是否存在数据，存在数据返回true，否则返回false
      while(it.hasNext()){
        //next()：将迭代器的游标向下移动一个位置，并返回游标指向的元素
        System.out.println(it.next());
      }
      System.out.println("**********");
      //方式二：使用foreach循环
      for(Integer i : set){
        System.out.println(i);
      }
    }
  }
```

4. List集合

* ArrayList：线性数据结构(数组)，查询数据时效率高，但添加与删除元素时效率低。创建集合时可以设置集合的长度，集合长度默认为10。如果集合的长度不足，根据比例自动扩展集合。
* LinkedList：链表数据结构，添加与删除数据时效率高，但查询数据时效率低。
* Vector：功能与ArrayList基本一致的。Vector是线程安全的，ArrayList是线程不安全的。

```java
//方式一：for循环遍历list（改数据推荐用此方式）
for(int i=0;i<list.size();i++) {
  System.out.println(list.get(i));
}
System.out.println("************************");
//方式二：使用foreach循环
for(String s:list) {
  System.out.println(s);
}
//方式三：迭代器
Iterator<String> it=list.iterator();
while(it.hasNext()) {
  System.out.println(it.next());
}
```

5. Map集合
1. Hashtable:是线程安全的，不允许使用null作为键或值。
2. HashMap:是线程不安全的，允许使用null作为键与值。
3. JDK1.7HashMap与JDK1.8HashMap的区别？

* JDK1.7HashMap：数组+链表
* JDK1.8HashMap：数组+链表+红黑树

```java
//方式一：用set+迭代器 将Map中所有的键存入set集合中

   Set<Integer> keys = map.keySet();
   // 将set中的所有键存入迭代器
   Iterator<Integer> it = keys.iterator();
   while (it.hasNext()) {
     Integer key = it.next();
     String value = map.get(key);
     System.out.println(key + "--" + value);
   }
   // 方式二：使用Set与foreach循环
   // 将map中所有的键存入Set集合中
   Set<Integer> keys1 = map.keySet();
   // 使用foreach循环获得Set集合中所有的键
   for (Integer key1 : keys1) {
     String value1 = map.get(key1);
     System.out.println(key1 + "----" + value1);
   }
```


# 正则表达式

## 字符：匹配单个字符

* a ：表示匹配字母 a
* \\\\：匹配转义字符 "\\"
* \\t ：匹配转义字符 "t"
* \\n ：匹配转义字符 "n"

## 一组字符：任意匹配里面的一个单个字符

* [ abc]：表示可能是字母 a ，可能是字母 b 或者是字母 c
* [ ^abc]：表示不是字母 a 、字母 b 、字母 c 的任意一个
* [ a-zA-Z]：表示全部字母中的任意一个
* [ 0-9]：表示全部数字的任意一个

## 边界匹配：在以后编写 JavaScript 的时候使用正则中要使用到

* ^^：表示一组正则的开始
* \$\$：表示一组正则的结束简写表达式：每一位出现的简写标记也只表示一位
* d：表示任意的一位数字，等价于 "\[0-9\]"
* D：表示任意的一位非数字，等价于 "\[\^0-9\]"
* w：表示任意的一位字母、数字、 \*，等价于 "\[a-zA-Z0-9*\]"
* W：表示任意的一位非字母、数字、 \*，等价于 "\[\a-zA Z0-9*\]"
* s：表示任意的一位空格，例如 n 、 t 等
* S：表示任意的一位非空格

## 数量表示：之前的所有正则都只是表示一位，如果要想表示多位，则就需要数量表示

* 正则表达式 ??：此正则出现 0 次或 1 次
* 正则表达式 **：此正则出现 0 次、 1 次或多次
* 正则表达式 ++：此正则出现 1 次或多次
* 正则表达式 { n}：此正则出现正好 n 次
* 正则表达式 { n,}：此正则出现 n 次以上
* 正则表达式 {n, m}：此正则出现 n ~ m次

## 方法

* `public boolean matches(String regex)`：与指定正则匹配
* `public String replaceAll (String regex, String replacement)`：替换满足指定正则的全部内容
* `public String replaceFirst (String regex, String replacement)`：替换满足指定正则的首个内容
* `public String[] split(String regex)`：按照指定正则全拆分
* `public String[] split(String regex, int limit)`：按照指定的正则拆分为指定个数

# 多线程

## 一、线程

1. 定义：在多任务操作系统中，每个运行的程序都是一个进程，用来执行不同的任务，而在一个进程中还可以有多个执行单元同时运行，来同时完成一个或多个程序任务，这些执行单元可以看做程序执行的一条条线索，被称为线程。

  <b>操作系统中的每一个进程中都至少存在一个线程。</b>

2. 单线程与多线程
单线程都是按照调用顺序依次往下执行，没有出现多段程序代码交替运行的效果，而多线程程序在运行时，每个线程之间都是独立的，它们可以并发执行。

3. 线程的创建（三种方式）

* 继承Thread类，重写run()方法
  * Thread类是java.lang包下的一个线程类，用来实现Java多线程。

      ①创建一个Thread线程类的子类（子线程），同时重写Thread类的run()方法；

      ②创建该子类的实例对象，并通过调用start()方法启动线程。

* 实现Runnable接口，重写run()方法

  * （Java只支持类的单继承，若已继承其他的父类，就无法再继承Thread，这时候可以实现Runnable接口。）

      ①创建一个Runnable接口的实现类，同时重写接口中的run()方法；

      ②创建Runnable接口的实现类对象；

      ③使用Thread有参构造方法创建线程实例，并将Runnable接口的实现类的实例对象作为参数传入；

      ④调用线程实例的start()方法启动线程。

* 实现Callable接口，重写call()方法，并使用Futrue来获取call()方法的返回结果
  * （由于Thread类和Runnable接口实现多线程时，需要重写run()方法，但是由于该方法没有返回值，而Callable有返回值。）

      ①创建一个Callable接口的实现类，同时重写Callable接口的call()方法；

      ②创建Callable接口的实现类对象；

      ③通过FutureTask线程结果处理类的有参构造方法来封装Callable接口实现类对象；

      ④使用参数为FutureTask类对象的Thread有参构造方法创建Thread线程实例；

      ⑤调用线程实例的start()方法启动线程。

      <img src="ThreadExtends.png" alt="FutureTask继承关系图" title="Callable接口实现多线程——FutureTask继承关系图">

>Callable接口方式实现的多线程是通过FutureTask类来封装和管理返回结果的，该类的直接父接口是RunnableFuture。
>
>FutureTask本质是Runnable接口和Future接口的实现类，而Future则是JDK 5提供的用来管理线程执行返回结果的。

* 三种创建线程方式的对比：实现Runnable接口（或者Callable接口）相对于继承Thread类实现多线程来说，有显著的好处：适合多个线程去处理同一个共享资源的情况；可以避免Java单继承带来的局限性。

* 后台线程的使用：在启动之前调用了`setDaemon(true)`语句，这个线程就变成一个后台线程。

4. 线程的生命周期及状态转换

  ① NEW（新建状态）

  ② RUNNABLE（可运行状态）

    * 就绪状态：线程对象调用start()方法之后，等待JVM的调度，此时线程并没有运行；

    * 运行状态：线程对象获得JVM调度，如果存在多个CPU，那么允许多个线程并行运行。

* 生命周期开始：Thread对象创建完成

* 生命周期结束：代码正常执行完毕或抛出一个未捕获的异常或者错误

  ③ BLOCKED（阻塞状态）：运行状态的线程因为某些原因失去CPU的执行权，会进入阻塞状态。阻塞状态的线程只能先进入就绪状态，不能直接进入运行状态。
    > 线程进入阻塞状态的两种情况：
    >
    >1) 当线程A运行过程中，试图获取同步锁时，却被线程B获取；
    >
    >2) 当线程运行过程中，发出IO请求时。

  ④ WAITING（等待状态）：调用了无时间参数限制的方法

  ⑤ TIMED_WAITING（定时等待状态）：运行状态中的线程调用了有时间参数限制的方法

  ⑥ TERMINATED（终止状态）

5. 线程的调度（两种调度模型：分时调度模型；<b>抢占式调度模型（JVM默认方式）</b>）

* 线程的优先级：①用1~10之间的整数表示，数字越大优先级越高；②还可以使用Thread类中提供的三个静态常量表示线程的优先级。

  * static int MAX_PRIORITY：表示线程的最高优先级，相当于值10

  * static int MIN_PRIORITY：表示线程的最低优先级，相当于值1

  * static int NORM_PRIORIY：表示线程的普通优先级，相当于值5

* 线程的休眠：使用静态方法sleep(long millis)。该方法会声明抛出InterruptedException异常，因此在调用该方法时应该捕获异常，或者声明抛出该异常。

* 线程让步：通过yield()方法实现。该方法不会阻塞该进程

* 线程插队：Thread类提供的join()方法。当调用其他线程的join()方法时，调用线程的将被阻塞，直到被join()方法加入的线程执行完成后它才会继续运行。Thread类中还提供了带有时间参数的线程插队方法join(long millis)。当执行带有时间参数的join(long millis)进行线程插队时，必须等待插入的线程指定时间过后才会继续执行其他线程。

6. 多线程同步

* 同步代码块

  ```java
  synchronized(lock){
  // 操作共享资源代码块
  ...
  }
  ```

  lock锁对象可以是任意类型的对象，但多个线程共享的锁对象必须是相同的。锁对象的创建代码不能放到run()方法中，否则每个线程运行到run()方法都会创建一个新对象，这样每个线程都会有一个不同的锁。

* 同步方法

    同步方法的锁是当前调用该方法的对象，就是this指向的对象

    `[修饰符] synchronized 返回值类型 方法名([参数1,……]){}`

    被synchronized修饰的方法在某一时刻只允许一个线程访问，访问该方法的其他线程都会发生阻塞，直到当前线程访问完毕后，其他线程才有机会执行。

* 同步锁

    synchronized同步代码块和同步方法使用一种封闭式的锁机制，但有限制，例如它无法中断一个正在等候获得锁的线程，也无法通过轮询得到锁，如果不想等下去，也就没法得到锁。自JDK5开始增加了Lock锁，优势在于Lock锁可以让某个线程在持续获取同步锁失败后返回，不再继续等待，另外Lock锁在使用时也更加灵活。

    ReentrantLock类是Lock锁接口的实现类。除了lock()方法和unlock()方法外，还提供了一些其他同步锁操作的方法，例如tryLock()方法可以判断某个线程锁是否可用。通常在finally{}代码块中调用unlock()方法来解锁。

    ```java
        Lock lock = new Reentrantlock();
        if(lock.trylock()){
          try{

          }finally{
              lock.unlock();
          }
        }else{

        }
    ```

* 死锁

    两个线程在运行时都在等待对方的锁，这样便造成了程序的停滞，这种现象称为死锁。

    避免死锁方式：

    ①加锁顺序（线程按照一定的顺序加锁）

    ②加锁时限（线程尝试获取锁的时候加上一定的时限，超过时限则放弃对该锁的请求，并释放自己占有的锁）

    ③死锁检测

7. 多线程通信

    Java在Object类中提供了wait()、notify()、notifyAll()等方法。其中wait()方法用于使当前线程进入等待状态，notify()和notifyAll()方法用于唤醒当前处于等待状态的线程。这三个方法的调用者都应该是同步锁，如不是Java虚拟机就会抛出IllegalMonitorStateException异常。

# I/O流

## 一、 I/O流的分类

 根据流操作数据单位的不同，分为字节流和字符流；

根据流传输方向的不同，分为输入流和输出流；

根据流的功能的不同。分为节点流和处理流

Java中的I/O流主要定义在java.io包中，该包下定义了很多类，其中有4个类为流的顶级类，分别为InputStream和OutputStream，Reader和Writer。这4个顶级类都是抽象类，并且是所有流类型的父类。
    <img src = "io.png" alt="io" title="io">

## 二、字节流

1. 所有字节输入流都继承InputStream，所有字节输出流都继承OutputStream。InputStream从源设备输入到程序，OutStream从程序输出到目标程序。

    InputStream常用方法：`int read()`、`int read(byte[] b)`、`int read(byte[] b,int off，int len)`、`void close()`

    * `int read()`：从输入流读取一个8位的字节，把它转换为0~255之间的整数，并返回这一整数。当没有可用字节时，将返回-1

    * `int read(byte[] b)`：从输入流读取若干字节，把它们保存到参数b指定的字节数组中，返回的整数表示读取字节的数目

    * `int read(byte[] b,int off，int len)`：从输入流读取若干字节，把它们保存到参数b指定的字节数组中，off指定字节数组开始保存数据的起始下标，len表示读取的字节数目

    * `void close()`：关闭此输入流并释放与该流关联的所有系统资源

    OutputStream常用方法：`void write(int b)`、`void write(byte[] b)`、`void write(byte[] b,int off,int len)`、`void flush()`、`void close()`

    * `void write(int b)`：向输出流写入一个字节

    * `void write(byte[] b)`：把参数b指定的字节数组的所有字节写到输出流

    * `void write(byte[] b,int off,int len)`：将指定byte数组中从偏移量off开始的len个字节写入输出流

    * `void flush()`：刷新此输出流并强制写出所有缓冲的输出字节

    * `void close()`：关闭此输出流并释放与此流相关的所有系统资源

2. 文件的读与写（用循环）：FileInputStream和FileOutputStream

    * 读文件：

    ```java
        import java.io.FileInputStream;
        import java.io.IOException;
        public class TestIO {
        public static void main(String[] args) throws IOException {
          FileInputStream in = new FileInputStream("G:\\idea_project\\_20220825\\src\\test.txt");
          int b = 0;
          while((b=in.read()) != -1){
          System.out.println(b);
        }
        in.close();
        }
        }
    ```

    **注意：必须保证文件在目录内存在以及可读，否则会抛出FileNotFoundException。**

    * 写文件（新写入的会覆盖原有的）

        ```java
      import java.io.FileOutputStream;
      import java.io.IOException;
      public class TestIO {
      public static void main(String[] args) throws IOException {
        FileOutputStream out = new FileOutputStream("G:\\idea_project\\_20220825\\src\\out.txt");
        String str = "hello world";
        out.write(str.getBytes());
        out.close();
        }
          }
        ```

    * 写文件（新写入的向原有的进行追加）

      ```java
      import java.io.FileOutputStream;
      import java.io.IOException;

      public class TestIO {
      public static void main(String[] args) throws IOException {
        FileOutputStream out = new FileOutputStream("G:\\idea_project\\_20220825\\src\\out.txt",true);
        String str = "hello world,hhh";
        out.write(str.getBytes());
        out.close();
      }
      }
      ```

      **注意：I/O流在进行数据读写操作时会出现异常，为了保证I/O流的close()方法一定执行来释放占用的系统资源，通常会将关闭流的操作写在finally代码块中。**

      ```java
          finally{
          try{
                if(in!=null)       in.close();
          }catch(Exception e){
           e.printStackTrace();
          }
          try{
         if(out!=null)     out.close();
          }catch(Exception e){
         e.printStackTrace();
          }
          }
      ```

3. 文件的拷贝

    I/O流通常都是成对出现的，即输入流和输出流一起使用。

    ```java
    FileInputStream in = new FileInputStream("source/src.jpg");
    FileOutputStream out = new FileOutputStream("target/dest.jpg");
    int len = 0;
    long beginTime = System.currentTimeMillis();
    while ((len = in.read()) != -1) {   
        out.write(len);
        }
    long endTime = System.currentTimeMillis();
    System.out.println("花费时间为："+(endTime-beginTime) +"毫秒");
    in.close();
    out.close();
    ```

    * 字节流的缓冲区：用字节数组定义

      优点：提高运行效率，节省程序运行时间

    ```java
      FileInputStream in = new FileInputStream("source/src.jpg");
      FileOutputStream out = new FileOutputStream("target/dest.jpg");
      int len = 0;
      byte[] buff = new byte[1024];
      long beginTime = System.currentTimeMillis();
      while ((len = in.read(buff)) != -1) {
          out.write(buff,0,len);
      }
      long endTime = System.currentTimeMillis();
      System.out.println("花费时间为："+(endTime-beginTime) +"毫秒");
      in.close();
      out.close();
    ```

    * 字节缓冲流：`BufferedInputStream`和`BufferedOutputStream`。接收`InputStream`和`OutputStream`类型的参数作为对象

      使用字节缓冲流拷贝文件：

    ```java
      BufferedInputStream bis = new BufferedInputStream(new FileInputStream("source/src.jpg"));
      BufferedOutputStream bos = new BufferedOutputStream(new FileOutputStream("target/dest.jpg"));
      int len = 0;
      long beginTime = System.currentTimeMillis();
      while ((bis.read()) != -1) {
            bos.write(len);
      }
      long endTime = System.currentTimeMillis();
      System.out.println("花费时间为："+(endTime-beginTime) +"毫秒");
      bis.close();
      bos.close();
    ```

## 三、字符流

  1. 有两个抽象的顶级父类，分别是Reader和Writer。

  <img src = "reader.png" align = "center" alt="reader" title="reader">

  <img src = "writer.png" align = "center" title="writer">

  2. 字符流操作文件（逐个字符读取文件）

  ```java
      FileReader fileReader = new FileReader("reader.txt");
      int len = 0;
      while ((len = fileReader.read()) != -1) {
          System.out.print((char)len);
      }
      fileReader.close();
  ```

  3. 字符流操作文件（逐个字符写入文件）

  ```java
      FileWriter fileWriter = new FileWriter("writer.txt");
      fileWriter.write("轻轻的我走了，\r\n");
      fileWriter.write("正如我轻轻的来；\r\n");
      fileWriter.write("我轻轻的招手，\r\n");
      fileWriter.write("作别西天的云彩。\r\n");
      fileWriter.close();
  ```

  **追加写入：调用重载的构造方法** `FileWriter fileWriter = new FileWriter("writer.txt",true);`

  > 字符流也可以使用字符流缓冲区和字符缓冲流来进行读写。字符缓冲流需要使用BufferedReader和   BufferedWriter，其中BufferedReader用于对字符输入流进行操作，BufferedWriter用于对字符输出流进行操作。在BufferedReader中有一个readLine()方法，用于一次读取一行文本。

 4. 字符流缓冲区拷贝文件

 ```java
      FileReader fileReader = new FileReader("reader.txt");
      FileWriter fileWriter = new FileWriter("writer.txt");
      int len = 0;
      char[] buff = new char[1024];
      while ((len = fileReader.read(buff)) != -1) {
          fileWriter.write(buff, 0, len);
      }
      fileReader.close();
      fileWriter.close();
 ```

5. 字符缓冲流拷贝文件

```java
    BufferedReader br = new BufferedReader(new FileReader("reader.txt "));
    BufferedWriter bw = new BufferedWriter(new FileWriter("writer.txt"));
    String str = null;
    while ((str = br.readLine()) != null) {
          bw.write(str);
          bw.newLine();
    }
    br.close();
    bw.close();
```

6. 转换流：将字节流转换为字符流

    InputStreamReader是Reader的子类，它可以将一个字节输入流转换成字符输入流，方便直接读取字符。

    OutputStreamWriter是Writer的子类，它可以将一个字节输出流转换成字符输出流，方便直接写入字符。

    * 转换流拷贝文件

    ```java
        FileInputStream in = new FileInputStream("reader.txt");
        InputStreamReader isr = new InputStreamReader(in);
        BufferedReader br = new BufferedReader(isr);
        FileOutputStream out = new FileOutputStream("writer.txt");
        OutputStreamWriter osw = new OutputStreamWriter(out);
        BufferedWriter bw = new BufferedWriter(osw);
        String line = null;
        while ((line = br.readLine()) != null) {
          bw.write(line);
          bw.newLine();
    }
        br.close();
        bw.close();
    ```

## 四、File类

1. File的常用构造方法

  `File(String pathname)`：通过指定的一个字符串类型的文件路径来创建一个新的File对象

  `File(String parent,String child)`：根据指定的一个字符串类型的父路径和一个字符串类型的子路径（包括文件名称）创建一个File对象

  `File(File parent,String child)`：根据指定的File类的父路径和字符串类型的子路径（包括文件名称）创建一个File对象

* 对当前目录下的txt文件进行操作

  ```java
      File file = new File("example.txt");   
      System.out.println("文件名称:" + file.getName());
      System.out.println("文件的相对路径:" + file.getPath());
      System.out.println("文件的绝对路径:" + file.getAbsolutePath());
      System.out.println("文件的父路径:" + file.getParent());
      System.out.println(file.canRead() ? "文件可读" : "文件不可读");
      System.out.println(file.canWrite() ? "文件可写": "文件不可写");
      System.out.println(file.isFile() ?  "是一个文件" :"不是一个文件");
      System.out.println(file.isDirectory()? "是一个目录":"不是一个目录");
      System.out.println(file.isAbsolute() ? "是绝对路径": "不是绝对路径");
      System.out.println("最后修改时间为:" + file.lastModified());
      System.out.println("文件大小为:" + file.length() + " bytes");
      System.out.println("是否成功删除文件"+file.delete());
  ```

* 遍历目录下的文件

  ```java
      File file = new File("F:\\Java基础入门\\workspace\\chapter07");
      if (file.isDirectory()) {
          String[] fileNames = file.list();
          Arrays.stream(fileNames).forEach(f -> System.out.println(f));
    }
  ```

* 筛选文件

  ```java
    File file = new File("F:\\Java基础入门\\workspace\\chapter07");
    if (file.isDirectory()) {
    String[] fileNames = file.list((dir,name) -> name.endsWith(".txt"));
    Arrays.stream(fileNames).forEach(f -> System.out.println(f));
    }
  ```

* 递归遍历目录文件

  ```java
    public static void main(String[] args){
          File file = new File(" F:\\Java基础入门\\workspace\\chapter07");
          fileDir(file);
    }
    public static void fileDir(File file) {
          File[] listFiles = file.listFiles(); //listFiles()方法返回一个File对象数组

          for (File files : listFiles) {
              if(files.isDirectory()){
                    fileDir(files); //递归调用遍历目录方法

              }
              System.out.println(files);
          }
    }
  ```

* 删除文件及目录

  ```java
  //Java中删除目录的操作是通过Java虚拟机直接删除而不走回收站的，文件一旦删除就无法恢复。
    public static void main(String[] args){
          File files = new File("D:\\test\\新建文件夹");
          deleteDir(files);
    }
    public static void deleteDir(File files) {
          File[] listFiles = files.listFiles();
          for (File file : listFiles) {
              if(file.isDirectory()){
                    deleteDir(file); //递归调用删除目录方法
              }
              file.delete(); //直接删除文件
          }
          files.delete(); //最后删除最外层目录
  }
  ```

2. RandomAccesseFile类：可以随机从文件的任何位置开始并以指定的操作权限（如只读、可读写等）执行读写数据的操作。

  RandomAccesseFile类构造方法：

* `RandomAccessFile(File file,String mode)`：使用参数file指定被访问的文件，并使用mode来指定访问模式
* `RandomAccessFile(String name,String mode)`:使用参数name指定被访问文件的路径，并使用mode来指定访问模式
  * mode的取值：
    * r：以只读的方式打开文件。如果执行写操作，会报IOException异常。
    * rw：以“读写”的方式打开文件。如果文件不存在，会自动创建该文件。
    * rws：以“读写”方式打开文件。与“rw”相比，它要求对文件的内容或元数据的每个更新都同步写入到底层的存储设备。
    * rwd：以“读写”方式打开文件。与“rw”相比，它要求对文件的内容的每个更新都同步写入到底层的存储设备。

# 单例模式

* Singleton类的三个要点
  * 构造方法是私有的或受保护的
  * 有一个保留其自身唯一实例的私有静态引用
  * 有一个返回该实例的公有静态方法

```java
public class Singleton{
 private static Singleton singleton = new Singleton();
 private Singleton()  {  }
 public static Singleton getInstance(){
  return singleton;
 }
 // 其他实例对象
}
 ```

三种形式：懒汉模式、饿汉模式、双重锁

* 懒汉模式

```java
  public class SingletonClass {
  private static SingletonClass instance = null;
  public static SingletonClass getInstance() {
    if (instance == null) {
        instance = new SingletonClass();
      }
      return instance;
        }
  private SingletonClass() {
  }
}

```

* 饿汉模式

```java
public class SingletonClass {
  private static SingletonClass instance = new SingletonClass();
  public static SingletonClass getInstance() {
  return instance;
  }
  private SingletonClass() {
  }
}
```

* 双重锁模式

```java
public class Singleton{
  private static Singleton instance = null;
  public static Singleton getInstance() {
  if (instance == null) {
    synchronized (Singleton.class) {
  if (instance == null) {
      instance = new Singleton();
      }
    }
  }
  return instance;
  }
  private Singleton ()
  }
  }
```

# Java GUI

## 一、GUI：图形用户接口

1. AWT：jdk1.0 SUN公司为GUI提供了一套基础类库。是重量级组件，使用麻烦，设计出的图形界面不够美观、功能有限
2. Swing：在原有的AWT的基础上进行了补充和改进 提供更加丰富的组件和功能。是轻量级组件，由Java语言开发，同时底层以AWT为基础。Swing包括两部分：

* 容器：实现图形化用户界面的容器
* 组件：实现向容器中填充数据、元素以及交互的组件

3. 基础类库：java.awt.*javax.swing.*

## 二、JFrame：是一个顶级容器，不能放在在其他容器中

1. 创建窗体的方法

* 直接创建窗体对象：`JFrame myframe= new JFrame();`
* 继承方式自定义窗体

```java
  class Test1 extends JFrame{
  声明组件
  构造方法（窗口的初始化）
    }
```

注意：窗体默认不可见，使用`setVisiable(true);`设置窗体可见,一定要放在最后。

* 构造方法
  * `JFrame();`：创建一个无标题的窗体
  * `JFrame(String s);`：创建一个标题为S的窗体
* 常用方法
  * `setTitle(String s);`：设置窗体标题
  * `setSize(int width,int height);`:设置窗体大小
  * `setLocation(int x, int y);`：设置窗体的位置
  * `setBounds(int x, int y, int width, int height);`：综合写法
  * `setLocationRelativeTo(null);`：设置窗体在屏幕的正中间显示
  * `setDefaultCloseOperation(功能选项);`：功能选项的值：通常设置为`JFrame.EXIT_ON_CLOSE` 关闭窗体并退出程序
  * `setResizable(boolean b);`：设置窗口是否可以调整大小
  * `dispose();`：撤销当前窗口，并释放当前窗口所用的资源

2. Swing组件

* 面板组件：中间容器，不能单独存在 只能放在顶级窗口容器中。作用：给分区设置内容
  * Jpanel：是一个无边框，不能被移动、放大、缩小、关闭的面板

    * 常用方法

    `setBackground(Color c);`：设置面板的背景色

    `add(组件对象);`:将组件添加到面板中
  * scrollPane：是一个带有滚动条的面板，只能放一个组件
* 其他组件
  * 标签组件：Jlabel：显示文本和图像

    构造方法：`Jlabel();`：创建一个无标题的标签

    * `JLabel(String s);`：创建一个指定文本s的标签
    * `JLabel(Icon image);`：创建一个具有指定图像的标签

    常用方法：
    * `setIcon(Icon image);`：设置文本图片
    * `setFont(Font f);`：设置字体，字号，是否加粗，倾斜等

  * 文本组件：用于接收用户输入的信息，包括单行文本框（JTextField)和文本域（JTextArea)、单行文本框JTextField

    构造方法：
    * `JTextField(int cols);`：指定列数的文本框
    * `JTextField(String s, int cols);`：指定文本、列数的文本框

    常用方法：
    * `setColumns(int cols);`：设置文本框的列数
    * `setText(String s);`：设置文本框的内容
    * `String getText();`获得文本框内容
    * `String getSelectedText();`获得选中内容
    * `setEditable(boolean b);`：设置文本框是否可以编辑

  * 密码框组件(JPasswordField)：用法基本与单行文本框相同

  * 文本域组件(JTextArea)
    构造方法：
    * `JTextArea();`：创建一个空的文本域
    * `JTextArea(int rows,int cols);`：创建指定行数列数的文本域
    * `JTextArea(String s);`：创建一个指定字符串s的文本域
    * `JTextArea(String s, int rows, int cols);`：综合写法
  * 按钮组件：JButton、JCheckBox、JRadioButoon
    JButton的构造方法
    * `JButton(String s);`：设置一个文本为S的按钮

3. 布局

常见的布局：

* `BorderLayout(边框布局);`:把容器分为东南西北中5个区域，当使用该布局时，要声明组件添加在哪个位置

* `FlowLayout(流布局);`:是JPanel的默认布局，组件自左向右

* CardLayout(卡片布局);``：组件彼此间重叠布局

* `GridLayout(网格布局);`：
注意：所有的容器（*）都可以通过`setbound()`方法设置布局方式

4. 菜单：菜单栏、菜单、菜单项

一个窗口中只有菜单，菜单栏中可以添加多个菜单，每个菜单可以添加若干个菜单项

* 菜单栏：JMenuBar

  设置到顶级容器：set...

* 菜单：JMenu

  构造方法：`JMenu(String s);`

* 菜单项：JMenuItem
 构造方法：`JMenuItem(String s);`

## 三、事件处理

swing组件中的事件处理专门用于响应用户的操作。如：鼠标的用户单击、按下键盘。

swing事件处理的过程中，主要涉及到三类对象

1. 事件源（event source）：事件发生的场所。通常是产生事件的组件，如按钮、菜单、窗口
2. 事件对象(event)：封装GUI组件上发生的特定事件
3. 监听器（listener）：负责监听事件源上发生的事件，并对各种事件做出相应处理（监听器对象中包含事件处理器）

事件处理机制：

1. 创建事件源：除了一些常见的按钮、键盘、菜单等组件，还可以使用JFrame窗口在内的顶级容器作为事件源
2. 自定义事件监听器：根据要监听的事件源创建指定类型的监听器进行事件处理。监听器是一个特殊的JAVA类，必须实现***ActionListener接口。根据组件触发的动作进行区分。如WindowActionListener用于监听窗口事件，ActionLIstener用于监听动作事件
3. 为事件源注册监听器：使用add***Listener()方法为指定事件源添加特定类型的监听器，当事件源发生监听事件后，就会触发绑定的事件监听器，由监听器中的方法对事件进行相应的处理。
