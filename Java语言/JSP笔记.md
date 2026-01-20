# JSP 笔记

## 1. JDBC

连接数据库：进入 MySQL->bin 目录 在地址栏输入“cmd” ，在打开的命令行中输入

”mysql -u root -p”，随后输入“root”进入数据库

### 1.1. 一、常用 Mysql 命令

1. `show databases`; 显示所有数据库名称
2. `create database 数据库名;` 创建数据库
3. `use 数据库名;`  使用数据库
4. `show tables;`  显示当前数据库中所有的表名

### 1.2. 二、使用 JDBC 操作数据库的步骤

1. 将数据库驱动导入到项目中

   J2SE 项目在 jar 文件上右键→Build Path→Add to Build Path

2. 加载数据库驱动（两种方法）

   1. 方法一：`Class.forName("包名.类名");` 将指定的类加载到内存中。

      ```java
      try{
          //MySQL5驱动
          //Class.forName("com.mysql.jdbc.Driver");
          //MySQL8驱动
          Class.forName("com.mysql.cj.jdbc.Driver");
          System.out.println("数据库驱动加载成功！！！");
      }catch(ClassNotFoundException e){
          System.out.println("数据库驱动加载失败！！！");
      }
      ```

   2. 方法二：`DriverManager.registerDriver(new 驱动());`  注册数据库驱动

      ```java
      try{
          DriverManager.registerDriver(new Driver());
          System.out.println("数据库驱动注册成功！！！");
      }catch(SQLException e){
          System.out.println("数据库驱动注册失败！！！");
      }
      ```

3. 创建<b>java.sql.Connection</b>接口类型的实例，连接数据库。

   1. 常用数据库端口号：

      1. MySQL：3306
      2. Oracle：1521
      3. SQL Server：1433

4. 创建对象，用于将 Java 中的字符串解析成数据库可以理解的 SQL 语句。

   1. 语句对象分为：```java.sql.Statement```与```java.sql.PreparedStatement```接口

   2. 当执行 select 语句时，需要调用语句对象的```executeQuery()```方法，此方法返回类型为```java.sql.ResultSet```接口类型的实例
   3. 当执行 insert，update，delete 语句时需要调用语句对象的```executeUpdate()```方法，此方法返回类型为 int 类型，表示语句执行后影响表中数据的行数。

5. 处理结果
   1. ResultSet 的 next() 方法，将结果集的游标<font color =red>向下</font>移动<font color=red>一行</font>。移动后游标找到数据返回 true，否则返回 false.
   2. ResultSet 的 getXXX() 方法，获得结果集中当前行指定列的信息。此方法的参数可以为<b>String</b>类型，也可以为<b>int</b>类型

6. 关闭与数据库相关的对象

### 1.3. 三、 <b>```java.sql.Statement```</b>接口与```java.sql.PreparedStatement```接口的关系与区别？

1. 关系：Statement 是 PreparedStatement 的父接口
2. 区别：
   1. 安全性
      1. Statement 无法防止 SQL 注入，安全性差
      2. PreparedStatement 可以防止 SQL 注入，安全性好
   2. 效率：当批量执行同一条 SQL 语句时。
      1. Statement 每执行一次 SQL 语句，都会先编译再运行，效率低。
      2. PrepareStatement 只在第一次执行 SQL 语句时编译，从第二次开始不再编译直接执行，效率高。

### 1.4. 四、使用 JDBC 向表中添加数据

1. 关闭数据库自动提交的功能，查询时因为不修改数据，所以不需要此操作

   ```java
   // 关闭数据库自动提交的功能，只在增删改需要
    conn.setAutoComit(false);
   ```

### 1.5. 五、查询数据代码

```java
package com.dao;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.util.Scanner;

public class TestSelectDao {

 public static void main(String[] args) {
  // TODO Auto-generated method stub
  //接收用户输入的编号
  Scanner sc= new Scanner(System.in);
  System.out.println("请输入查询的编号：");
  int id = sc.nextInt();
  //调用当前类中名为selectById()的方法，查询满足条件的数据
  TestSelectDao testDao = new TestSelectDao();
  testDao.selectById(id);

  sc.close();
 }

 /**
  * 根据T_ID查询TEST_TABLE中满足条件的数据
  * @param id 编号
  */
 public void selectById(int id) {
  Connection conn = null;
  //声明准备语句对象
  PreparedStatement ps= null;
  ResultSet rs = null;
  try {
   //加载数据库驱动
   Class.forName("com.mysql.cj.jdbc.Driver");
   //连接数据库

    conn = DriverManager.getConnection("jdbc:mysql://127.0.0.1:3306/test?serverTimezone=UTC&useUnicode=true&characterEncoding=utf8&useSSL=false", "root", "root");
    //创建select语句，用于查询满足条件的对象
    String sql="select t_id,t_name,t_email,t_birthday from test_table where t_id=?";
    //创建准备语句对象，并设置准备语句对将要执行的SQL语句
    ps=conn.prepareStatement(sql);
    //替换准备语句对象中的问号
    ps.setInt(1,id);
    //使用准备语句对象执行select语句，并将查询的结果存入到结果集
    rs = ps.executeQuery();
    //处理数据
    while(rs.next()) {
     System.out.print(rs.getInt("t_id")+"\t");
     System.out.print(rs.getString("t_name")+"\t");
     System.out.print(rs.getString("t_email")+"\t");
     System.out.print(rs.getString("t_birthday")+"\t");
    }

   } catch (ClassNotFoundException e) {

   System.out.println("数据库驱动加载失败！！！");
  }
  catch (SQLException e) {

   e.printStackTrace();
  }finally {
   //关闭与数据库相关的对象
   if(conn !=null)
   {
    try {
     conn.close();
    } catch (SQLException e) {

    }
   }

  }
 }

}


```

### 1.6. 六、修改数据代码

```java
package com.dao;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.SQLException;
import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.Date;
import java.util.Scanner;

public class TestUpdateDao {

 public static void main(String[] args) {
 //接收用户输入的编号与新出生日期
  Scanner sc=new Scanner(System.in);
  System.out.println("请输入编号：");
  int id = sc.nextInt();

  System.out.println("请输入出生日期：");
  String tempBirthday = sc.next();

  //将String转换为Date
  SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd");
  Date birthday = null;
  try {
   //调用名为update()的方法，修改表中的数据
   TestUpdateDao dao = new TestUpdateDao();
   birthday = sdf.parse(tempBirthday);
   int i = dao.update(id, birthday);
   System.out.println(i>0?"修改成功":"修改失败");
  } catch (ParseException e) {
   // TODO Auto-generated catch block
   System.out.println("日期格式不正确！！！");
  }
 }
 /**
  * 修改Test_table表中指定编号的出生日期
  * @param id 编号
  * @param birthday 新的出生日期
  * @return 修改成功返回大于0的整数，否则返回0
  */
 public int update(int id ,Date birthday) {
  Connection conn = null;
  PreparedStatement ps =null;
  try {
   //加载数据库驱动
   Class.forName("com.mysql.cj.jdbc.Driver");
   //连接数据库
   conn = DriverManager.getConnection("jdbc:mysql://127.0.0.1:3306/test?serverTimezone=UTC&useUnicode=true&characterEncoding=utf8&useSSL=false", "root", "root");
   //创建update语句，用于修改表中的数据
   String sql = "update test_table set t_birthday=? where t_id=?";
   //关闭数据库自动提交功能
   conn.setAutoCommit(false);
   //创建准备语句对象，并设置准备语句对象将要执行的update语句
   ps = conn.prepareStatement(sql);
   //替换准备语句对象中的问号
   //将java.util.Date转换为java.sql.date
   ps.setDate(1, new java.sql.Date(birthday.getTime()));
   ps.setInt(2, id);
   //使用准备语句对象执行update语句，并获得update语句执行后影响表中数据的行数
   int rows = ps.executeUpdate();
   //处理数据
   if(rows > 0) {
    //修改成功，提交数据
    conn.commit();
    return rows;
   }
   //修改失败，回退数据
   conn.rollback();
  } catch (ClassNotFoundException e) {
   System.out.println("数据库驱动加载失败！！！");

  }catch (SQLException e) {
   System.out.println("数据库异常！！！");
   e.printStackTrace();
  }finally {
   //关闭与数据库相关的对象
   if(conn !=null) {
    try {
     conn.close();
    } catch (SQLException e) {
     // TODO Auto-generated catch block
     e.printStackTrace();
    }
   }

  }

  return 0;

 }
}
```

### 1.7. 七、插入数据代码

```java
package com.dao;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.SQLException;
import java.util.Scanner;

public class TestInsertDao {
 public static void main(String[] args) {
  //接收用户输入的编号，姓名，邮箱
  Scanner sc = new Scanner(System.in);
  System.out.print("请输入编号");
  int id = sc.nextInt();

  System.out.print("请输入姓名");
  String name = sc.next();

  System.out.print("请输入邮箱");
  String email = sc.next();
  //调用insert()方法，向表中添加一行新数据
  TestInsertDao dao = new TestInsertDao();
  int i = dao.insert(id, name, email);
  System.out.println(i > 0 ? "添加成功":"添加失败");
  sc.close();
 }
 /**
  * 向TEST_TABLE表中添加一行新的数据
  * @param id 编号
  * @param name 姓名
  * @param email 邮箱
  * @return 添加成功返回大于0的数据，否则返回0
  */
 public int insert(int id,String name,String email) {
  Connection conn =null;
  PreparedStatement ps = null;
  try {
   //加载数据库驱动
   Class.forName("com.mysql.cj.jdbc.Driver");
   //连接数据库
   conn = DriverManager.getConnection("jdbc:mysql://127.0.0.1:3306/test?serverTimezone=UTC&useUnicode=true&characterEncoding=utf8&useSSL=false", "root", "root");
   //创建insert语句，用于向表中添加一行新数据
   String sql = "insert into test_table(t_id,t_name,t_email) values(?,?,?)";
   //关闭数据库自动提交的功能，只有增删改时需要
   conn.setAutoCommit(false);
   //创建准备语句对象，并设置准备语句对象将要执行的insert语句
   ps = conn.prepareStatement(sql);
   //替换准备语句对象中的问号
   ps.setInt(1, id);
   ps.setString(2, name);
   ps.setString(3, email);
   //使用准备语句对象执行insert语句，并获得执行的结果
   int rows = ps.executeUpdate();
   //处理数据
   if(rows > 0) {
    //添加成功，保存数据
    conn.commit();
    return rows;
   }
   //添加失败，回退数据
   conn.rollback();
  } catch (ClassNotFoundException e) {
   System.out.println("数据库驱动加载失败！！！");
  } catch (SQLException e) {
   System.out.println("数据库异常！！！");
   e.printStackTrace();
  }finally {
   //关闭与数据库相关的对象
   if(conn !=null) {
    try {
     conn.close();
    } catch (SQLException e) {
     // TODO Auto-generated catch block
     e.printStackTrace();
    }
   }
  }
  return 0;

 }
}

```

### 1.8. 八、删除数据代码

```java
package com.test.dao;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.SQLException;
import java.util.Scanner;



public class TestTableDao {

 public static void main(String[] args) {

  Scanner sc = new Scanner(System.in);  //从键盘接收编号
  System.out.println("请输入需要删除的编号：");
  int id = sc.nextInt();

  TestTableDao dao = new TestTableDao();
  int i = dao.delete(id);//调用名为delete()的方法，删除表中的数据
  System.out.println(i>0?"删除成功":"删除失败");
 }
 /**
  *
  * @param id 需要删除的用户编号
  * @return 删除成功返回大于0的整数，否则返回0
  */
 public int delete(int id) {
  Connection conn = null;  //声明连接对象
  PreparedStatement ps = null;//声明准备语句对象
  try {
   Class.forName("com.mysql.cj.jdbc.Driver"); //加载数据库驱动
   conn = DriverManager.getConnection("jdbc:mysql://127.0.0.1:3306/exe?serverTimezone=UTC&useUnicode=true&characterEncoding=utf8&useSSL=false", "root", "root");
   String sql = "delete from student where sid = ?"; //删除记录的SQL语句
   conn.setAutoCommit(false); // 关闭数据库自动提交功能
   ps = conn.prepareStatement(sql);
   ps.setInt(1, id);//替换准备语句对象中的问号
   int rows = ps.executeUpdate();//使用准备语句对象执行delete语句，并获得update语句执行后影响表中数据的行数

   if(rows >0) {
    conn.commit();
    return rows;
   }
   conn.rollback();

  } catch (ClassNotFoundException e) {
   // TODO Auto-generated catch block
   System.out.println("数据库驱动加载失败！！！");
  } catch (SQLException e) {
   // TODO Auto-generated catch block
   System.out.println("数据库连接失败！！！");
   e.printStackTrace();
  }finally {
   if(conn !=null) {
    try {
     conn.close();
    } catch (SQLException e) {
     // TODO Auto-generated catch block
     e.printStackTrace();
    }
   }
  }
  return 0;
 }

}

```

### 1.9. 九、封装查询结果的数据

 1. 在 com.test.entity 包中创建表对应的实体类，并设置 get()set() 方法

    ```java
    private Integer tId;
    private String tName;
    private String tEmail;
    private Date tBirhday;
    ```

2.

```java
   public Integer gettId() {
     return tId;
    }
    public void settId(Integer tId) {
     this.tId = tId;
    }
    public String gettName() {
     return tName;
    }
    public void settName(String tName) {
     this.tName = tName;
    }
    public String getTemail() {
     return tEmail;
    }
    public void setTemail(String temail) {
     this.tEmail = temail;
    }
    public Date getTbirhday() {
     return tBirhday;
    }
    public void setTbirhday(Date tbirhday) {
     this.tBirhday = tbirhday;
    }

   ```

 3. 封装查询方法

   ```java
   public class TestTableDao {

    public static void main(String[] args) {
     //调用selectAll()方法，查询表中所有的数据
     TestTableDao dao = new TestTableDao();
     List<TestTable> list = dao.selectAll();
     if(list != null && list.size() > 0) {
      //查询到了数据，并显示
      //使用foreach循环遍历查询结果
      for(TestTable t : list) {
       System.out.println(t.gettId() + "\t" + t.gettName() + "\t" + t.getTemail() + "\t" + t.getTbirhday());
      }

     }else {
      //没有查询到数据
      System.out.println("没有查询到数据！！");
     }

    }
    /**
     * 查询Test_table中所有数据
     * @return 查询成功返回java.util.List类型的实例，否则返回NULL
     */
    public List<TestTable> selectAll() {
     Connection conn = null;
     PreparedStatement ps = null;
     ResultSet rs = null;
     try {
      Class.forName("com.mysql.cj.jdbc.Driver");//加载数据库驱动
      conn = DriverManager.getConnection("jdbc:mysql://127.0.0.1:3306/test?serverTimezone=Asia/Shanghai&useUnicode=true&characterEncoding=utf8&useSSL=false", "root", "root");//连接数据库
      //创建select语句，查询表中所有的数据select t_id,t_name,t_email,t_birthday from test_table
      String sql = "select t_id,t_name,t_email,t_birthday from test_table";
      //创建准备语句对象，并设置准备语句对象将要执行的select语句
      ps=conn.prepareStatement(sql);
      //使用准备语句对象执行select语句，并将查询的结果存入到结果集
      rs = ps.executeQuery();

      //创建List集合，用于备份结果集中的所有的数据
      List<TestTable> list = new ArrayList<>();
      //声明实体类的变量，用于保存结果集中的一行数据
      TestTable testTable = null;
      //使用循环遍历结果集，并将结果集的数据封装到list集合中
      while(rs.next()) {
       //创建实体类的对象，保存结果集中的一行数据
       testTable = new TestTable();
       testTable.settId(rs.getInt("t_id"));
       testTable.settName(rs.getString("t_name"));
       testTable.setTemail(rs.getString("t_email"));
       testTable.setTbirhday(rs.getDate("t_birthday"));
       //将实体类的对象添加到List集合中
       list.add(testTable);

      }
      //循环结束后，返回list集合
      return list;
     } catch (ClassNotFoundException e) {

      System.out.println("数据库驱动加载失败！！！");
     } catch (SQLException e) {
      System.out.println("数据库加载失败！！！");
      e.printStackTrace();
     }finally {
      if(conn!=null) {
       try {
        conn.close();
       } catch (SQLException e) {
       }
      }
     }
     //使用准备语句对象执行select语句，并将查询的结果存入结果集中
     return null;

    }
   }
```

## 2. 程序模型

### 2.1. 一、C/S（客户端 / 服务器）模型

1. 优点：客户体验非常好
2. 缺点：如果升级包比较大，客户升级困难，对客户端 PC 配置要求高

### 2.2. 二、B/S（浏览器 /Web 服务器 应用服务器）模型

1. 优点：对客户端 PC 配置要求不高。程序升级时用户几乎感受不到。
2. 缺点：客户体验不如 C/S 模型

### 2.3. 三、Tomcat

1. Tomcat 的配置

   解压 / 安装时不要放在中文目录下。

   1. 配置环境变量
      1. 必须先配置 jdk 的环境变量

      2. home_path：JDK 的路径

      3. jre_home：JDK 的路径

2. Tomcat 常用目录

   1. bin 目录：存放与 Tomcat 运行相关的批处理文件及 Java 类库

   2. conf 目录：存放 Tomcat 的配置文件

   3. lib 目录：存放当前服务器所有站点公用的 Java 类库

   4. logs 目录：存放日志文件

   5. webapps（web-applications）目录：存放当前服务器中所有的 web 应用（站点）

   6. work 目录：存放站点生成的。class 文件

3. Tomcat 属于 Web 服务器

4. 解析 url：<http://www.baidu.com/bbs/index.html>

   1. http://：表示 http 协议，浏览器默认支持的协议，可以省略。
   2. www：表示 www 服务
   3. baidu.com：域名。通过 DNS 服务器可以将域名解析成 IP 地址或服务器名
   4. bbs：服务器中的目录
   5. index.html：服务器中的文件

5. 修改默认 Tomcat 默认的端口号

   1. Tomcat 默认端口号为 8080

   2. 在 Tomcat 目录→conf 目录→server.xml 文件，更改 port 后的数值

      ```xml
       <Connector port="8080" protocol="HTTP/1.1"
       connectionTimeout="20000"
       redirectPort="8443" />
      ```

6. 公有空间与私有空间

   1. 公有空间：WEB-INF 目录以外的空间。公有空间中的资源用户可以访问可以下载。
   2. 私有空间：WEB-INF 目录被称为私有空间。私有空间中的资源用户不能直接下载。

## 3. Servlet

### 3.1. 一、Servlet 功能

是<font color="red">Java</font>编写的存放在<font color="red">服务器</font>端的<font color="red">组件</font>。可以<font color="red">动态扩展</font>服务器的功能。

### 3.2. 二、第一个 Servlet 的示例

1. <b>务必保证 eclipse 适用于 Java EE 的开发</b>

2. 在 eclipse 中配置 Tomcat 服务器：

   Window→Preferences→Server→Runtime Envoinrments，单击 Add

   ![image-20220328074630995](C:\Users\谭政\AppData\Roaming\Typora\typora-user-images\image-20220328074630995.png)

   ![image-20220328074418546](C:\Users\谭政\AppData\Roaming\Typora\typora-user-images\image-20220328074418546.png)

3. 选择 Tomcat 版本

   ![image-20220328074454913](C:\Users\谭政\AppData\Roaming\Typora\typora-user-images\image-20220328074454913.png)

4. 选择 Tomcat 的位置

   ![image-20220328074520120](C:\Users\谭政\AppData\Roaming\Typora\typora-user-images\image-20220328074520120.png)

5. 创建 JavaEE 项目（Dynamic Web Project）

   ![image-20220328074602603](C:\Users\谭政\AppData\Roaming\Typora\typora-user-images\image-20220328074602603.png)

6. 设置项目信息

   ![image-20220328074737942](C:\Users\谭政\AppData\Roaming\Typora\typora-user-images\image-20220328074737942.png)

7. 设置生成 web.xml 文件（在上一步设置项目信息后，单击 Next→Next，勾选“Generate web.xml deployment descriptor”

   ![image-20220328074807368](C:\Users\谭政\AppData\Roaming\Typora\typora-user-images\image-20220328074807368.png)

8. 在<b>公有空间 (webapp)</b>目录下新建 index.html 文件，并写入如下内容：

   ```html
   <!DOCTYPE html>
   <html>
   <head>
   <meta charset="UTF-8">
   <title>Insert title here</title>
   </head>
   <body>
         <!--只写这里面的内容 -->
    <a href="first">第一个Servlet示例</a>
   </body>
   </html>

   ```

工作逻辑：

1. 点击超链接时，index.html 会向服务器发出请求，请求一个名为 first 的资源。
2. 服务器接收到请求后，会在私有空间中的 web.xml 文件中查找与 first 相关的配置。

9. 配置 web.xml 文件

   1. 第一次打开 web.xml 文件会出现如下的视图：

      ![image-20220328075000240](C:\Users\谭政\AppData\Roaming\Typora\typora-user-images\image-20220328075000240.png)

需要单击下方的“Source”以切换视图：

![image-20220328075026906](C:\Users\谭政\AppData\Roaming\Typora\typora-user-images\image-20220328075026906.png)

编写如下代码：

```xml
<servlet>
   <servlet-name>firstServlet</servlet-name>
   <servlet-class>com.test.controller.FirstServlet</servlet-class>
  </servlet>

  <!-- 映射请求与类的关系 -->
  <servlet-mapping>
     <servlet-name>firstServlet</servlet-name>
     <!-- 必须以斜杠开头 -->
     <url-pattern>/first</url-pattern>
  </servlet-mapping>
```

根据 web.xml 文件中，<servlet>中<servlet-class>的配置，在该项目的“src/main/java”中创建包与类（复制 com.test.controller.FirstServlet 到 Name 处，eclipse 会自动填写包名）。

![image-20220328075116790](C:\Users\谭政\AppData\Roaming\Typora\typora-user-images\image-20220328075116790.png)

并继承 HttpServlet 类，重写父类的 service() 方法。

代码如下：

```xml
<servlet>
   <servlet-name>firstServlet</servlet-name>
   <servlet-class>com.test.controller.FirstServlet</servlet-class>
  </servlet>

  <!-- 映射请求与类的关系 -->
  <servlet-mapping>
     <servlet-name>firstServlet</servlet-name>
     <!-- 必须以斜杠开头 -->
     <url-pattern>/first</url-pattern>
  </servlet-mapping>
```

	```java
package com.test.controller;

import java.io.IOException;
import java.io.PrintWriter;
import java.util.Date;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

public class FirstServlet extends HttpServlet {

 @Override
 protected void service(HttpServletRequest arg0, HttpServletResponse arg1) throws ServletException, IOException {
  //声明输出流，用于向浏览器中输出数据
  PrintWriter out = arg1.getWriter();

  out.println("<html>");
  out.println(" <body>");
  out.println(  "<div style ='color:#FF0000'>" + new Date() + "</div>");
  out.println(" </body>");
  out.println("</html>");

  //刷新缓冲区
  out.flush();
        //关闭输出流
  out.close();
 }

}
```

程序运行效果如下：

<b><font color="red">务必运行index.html文件而不是FirstServlet.java文件！</font></b>

单击该超链接：

![image-20220328075238180](C:\Users\谭政\AppData\Roaming\Typora\typora-user-images\image-20220328075238180.png)

![image-20220328075253838](C:\Users\谭政\AppData\Roaming\Typora\typora-user-images\image-20220328075253838.png)

### 3.3. 三、Servlet 的结构

<img src="C:\Users\谭政\AppData\Roaming\Typora\typora-user-images\image-20220328075447673.png" alt="image-20220328075447673" style="zoom:67%;" />

1. javax.servlet.Servlet 接口：声明了 Servlet 中最基础的方法
2. javax.servlet.GenericServlet 类：实现了 Servlet 接口，并重写了接口中的方法
3. javax.servlet.http.HttpServlet 类：对 http 协议进行了优化
4. 创建自定义的 servlet，<font color="red">直接或间接实现 servlet 接口</font>.

### 3.4. 四、servlet 生命周期

1. 当浏览器向服务器发出一个请求，请求一个 servlet 资源时；
2. 服务器接收到请求后，会在内存（缓存）中查找是否存在此 servlet 的实例
   1. 如果服务器没有在内存中找到该 servlet 实例时，服务器会创建此 servlet 的实例，并将实例加载到内存中，并调用 servlet 实例的 init() 进行初始化，再调用 service() 方法对请求做出响应
   2. 如果服务器在内存中找到了该 servlet 的实例，服务器会直接调用 servlet 实例的 service() 方法对请求做出响应
   3. 当服务器发现内存某个 servlet 实例在一段时间内没有被任何请求访问时，服务器会调用 servlet 实例的 destroy() 方法，销毁此 servlet 实例

## 4. 请求与响应

### 4.1. 一、```javax.servlet.http.HttpServletRequest```接口：请求

1. HttpServletRequest 常用方法：
   1. ```getParameter("名字")```：获得请求中指定名字的数据的数据。返回类型一定为<font color="red">String</font>。
   2. ```setCharcterEncoding("字符集")```：设置字符集
   3. ```getParameterValues("名字")```：获得请求中名字相同的一组数据。返回类型一定为<font color="red">String[] 数组</font>
   3. ```getParameterValues("资源名称")```：获得指定的资源。返回类型为 javax.RequestDispatcher 类型
   3. ```setAtrribute(“名字,数据”)```：将数据以指定的名字存入到请求中。
   3. ```getAttribute(“名字”)```：从请求中获得指定名字的数据。返回类型一定为<font color="red"><b>java.lang.Object</b></font>类型

### 4.2. 二、```java.servlet.http.HttpServletResponse```接口：响应

1. HttpServletRequest 常用方法：
   1. ```setCharacterEncoding("字符集")```：设置字符集
   2. ```setContentType("text/html;charset=字符集")```：设置目标浏览器显示的内容及字符集
   2. ```sendRedirect("资源名")```：重定向
   2. ```encodeRedirectURL(“资源名”)```：保证重定向、表单提交、超链接时不丢失 SessionID

实例（在浏览器上根据用户输入的行和列，输出表格）：

html 部分（省略`<html>`等公共标签，只写`<body>`里的部分）：

```html
<form action="table" method="post">
  <p>
  行：<input type="number" name="rows" required="required">
  </p>

  <p>
  列：<input type="number" name="cols" required="required">
  </p>

  <p>
   <button type="submit">画表格</button>
   <button type="reset">重置</button>

  </p>
 </form>
```

效果图：

<img src="C:\Users\谭政\AppData\Roaming\Typora\typora-user-images\image-20220328122356224.png" alt="image-20220328122356224" style="zoom:80%;" />

编写 xml 代码：

```xml
<servlet>
   <servlet-name>tableServlet</servlet-name>
   <servlet-class>com.test.controller.TableServlet</servlet-class>
  </servlet>
<servlet-mapping>
   <servlet-name>tableServlet</servlet-name>
   <url-pattern>/table</url-pattern>
</servlet-mapping>
```

新建 TableServlet.java 文件

```java
public class TableServlet extends HttpServlet{
 @Override
 protected void service(HttpServletRequest arg0, HttpServletResponse arg1) throws ServletException, IOException {
  //设置请求的字符集
  arg0.setCharacterEncoding("utf-8");
  //设置响应的字符集
  arg1.setCharacterEncoding("utf-8");
  //设置目标浏览器显示的内容及使用的字符集
  arg1.setContentType("text/html;charset=utf-8"); //注意是分号，如果是逗号会提示下载文件
  //获得用户在浏览器中输入的行和列
  int rows = Integer.parseInt(arg0.getParameter("rows"));
  int cols = Integer.parseInt(arg0.getParameter("cols"));

  //根据用户输入的行和列，向浏览器输出表格
  PrintWriter out = arg1.getWriter();

  out.println("<html>");
  out.println(" <body>");
  out.println(  "<table border='1'>");
  //循环行
  for(int i = 1 ; i <=rows ; i++) {
   out.println("  <tr>");
   //循环列
   for(int j = 1; j<=cols;j++ ) {
    out.println("<td>&nbsp;&nbsp;&nbsp;&nbsp;</td>");
   }
   out.println("  </tr>");
  }

  out.println(  "</table>");
  out.println(  "<br>");
  out.println("  <div><a href='index.html'>重新画表格</a></div>");
```

效果图

<img src="C:\Users\谭政\AppData\Roaming\Typora\typora-user-images\image-20220328122833034.png" alt="image-20220328122833034" style="zoom:67%;" />

<img src="C:\Users\谭政\AppData\Roaming\Typora\typora-user-images\image-20220328122845975.png" alt="image-20220328122845975" style="zoom:67%;" />

读取复选框中的数据：

html 部分：

```html
<form action="values" method="post">
  <input type="checkbox" name="v1" value="1"/>北京
  <input type="checkbox" name="v1" value="2"/>上海
  <input type="checkbox" name="v1" value="3"/>广州
  <input type="checkbox" name="v1" value="4"/>曹县
  <button type="submit">确定</button>
 </form>
```

编写 xml 代码：

```xml
<servlet>
   <servlet-name>valuesServlet</servlet-name>
   <servlet-class>com.test.controller.ValueServlet</servlet-class>
  </servlet>
<servlet-mapping>
   <servlet-name>valuesServlet</servlet-name>
   <url-pattern>/values</url-pattern>
  </servlet-mapping>
```

java 部分：

```java
public class ValueServlet extends HttpServlet{

 @Override
 protected void service(HttpServletRequest arg0, HttpServletResponse arg1) throws ServletException, IOException {
  //获得用户在浏览器中输入了哪些复选框

  String[] array=arg0.getParameterValues("v1");
  for(String s: array) {
   System.out.println(s);
  }
  System.out.println("-------------------");
 }

```

更改 web.xml 启动时的页面：

```xml
<welcome-file>select.html</welcome-file>
```

## 5. Java Bean

### 5.1. 一、JavaBean

就是 Java 类。

### 5.2. 二、JavaBean 的特征

1. JavaBean 是一个公有的类。
2. JavaBean 需要提供一个无参的构造方法。
3. JavaBean 需要为 private 的成员变量提供 public 的 getter 或 setter 方法。
4. JavaBean 需要实现序列化接口。

## 6. 线程安全

### 6.1. 一、Servlet 与线程安全

1. Servlet 中成员变量是线程不安全的。
2. Servlet 中方法的局部变量是线程安全的。

### 6.2. 二、范围对象与线程安全

## 7. 请求转发 (Forward) 与重定向 (Redirect)

### 7.1. 一、Web 资源之间只有三种关系

​ 包含、请求转发、重定向

### 7.2. 二、 Web 资源：Servlet、html 页面、JSP 页面

### 7.3. 三、请求转发与重定向的共同点

​ 两者都可以从一个资源跳转到另一个资源

### 7.4. 四、请求转发

```java
//完整代码
//1. 获得目标资源
 RequestDispatcher rd = req.getRequestDispatcher("error.html");
//2. 判断目标资源是否存在
 if(rd != null){
        //3. 进行请求转发，跳转到另一个资源
        rd.forward(req,resp);
    }
//精简代码
req.getRequestDispatcher("error.html").forward(req,resp);
```

### 7.5. 五、重定向

```java
resp.sendRedirect("error.html");
```

### 7.6. 六、请求转发与重定向的区别

1. 请求转发的特征：
   1. 在请求转发的过程中只产生一个请求和一个响应
   2. 浏览器<font color="red">地址栏</font>中的内容<b>不变</b>
   3. 请求转发的过程可以使用```HttpServletRequest```传递数据
   4. 请求转发只能在本站点内进行跳转
2. 重定向的特征
   1. 在重定向的过程中会产生两个请求和两个响应
   2. 浏览器地址栏中的内容会发生改变
   3. 重定向的过程中不能使用 HttpServletRequest 传递数据
   4. 重定向可以跳转到其他站点中

## 8. JSP(Java Server Page)

### 8.1. 一、JSP 页面与 HTML 页面的区别

1. HTML 页面：静态页面，只能出现静态元素。如：html 标签，css 代码，js 代码
2. JSP 页面：动态页面。动态页面中除了可以出现静态元素外，还可以出现动态元素。如：Java 代码，JSP 标签等

### 8.2. 二、JSP 的本质就是一个 Servlet

### 8.3. 三、JSP 在制作视图层（画页面）时，比 Servlet 效率高

### 8.4. 四、JSP 的工作原理（为什么 JSP 程序在第一次运行时比较慢）

1. 第一次运行 JSP 页面时，服务器会根据 JSP 页面生成对应的 java 文件，再根据 java 文件编译生成。class 文件，再执行。class 文件中相应的方法。
2. 从第二次开始再运行 JSP 页面时，服务器会直接调用。class 文件相应的方法，而不再编译。

### 8.5. 五、页面中的动态元素

1. JSP 页面中的指令元素。JSP 页面只有三个指令元素：page，include，taglib
   1. 指令元素的格式：```<%@指令元素名 属性="值"[属性="值"]%>```

   2. 同一个指令在一个 JSP 页面中可以重复出现。

   3. page 指令：设置 JSP 页面的属性

      1. language：设置当前 JSP 页面中可以使用 Java 代码。目前为止只能 Java
      2. import：导包。该属性是 page 指令中唯一可以重复出现的属性，也可以使用一个 import 属性导入多个类，类和类之间用逗号分隔
      2. errorPage：当前页面出现运行异常时，自动转发到的页面
      4. isErrorPage：设置当前 JSP 页面是否为错误页面，默认为 false。如果此属性为 True，则表示当前的 JSP 页面比普通的 JSP 页面多一个内置对象

      5. session：设置当前的 JSP 页面是否可以使用 session 范围对象，默认为 true

      6. pageEcoding：设置当前 JSP 页面的字符集。默认为 ISO-8859-1

      7. contentType：设置浏览器显示的内容及字符集。默认为 text/html;charset=ISO-8859-1

      4. include 指令：静态包含
           1. 格式：```<%@include file="文件名"%>```
           2. 静态包含：当服务器将 JSP 页面编译成。java 文件时，将指定的文件包含到页面中。

2. taglib 指令：在 JSP 页面中导入其他的标签库

3. JSP 页面中的 Java 代码

   1. 声明：```<%! Java代码 %>```，声明中的 Java 代码会出现在类的里面方法的外面，成为类的成员（成员变量与成员方法）。声明中可以出现：变量、方法、块、内部类。声明中的变量是线程不安全的。

   2. 脚本：```<% Java代码%>```，脚本中的代码会出现在 jspService() 方法的内部，成为方法的局部代码。脚本中可以出现：变量，判断、循环。脚本中的代码是线程安全的。

   3. 表达式：```<%=一行java代码&>```：将 Java 代码的结果显示在 JSP 页面中，表达式中的代码会出现在 out.print() 方法的括号内，所以表达式中的 Java 代码**不能用分号表示结束**。表达式中可以调用方法，但方法必须有返回数据

4. JSP 页面中的 JSP 标签

   1. JSP 标签：区分大小写

   2. ```<jsp:include>```标签：动态包含。

   3. 格式：```<jsp:include page=“页面名” flush=“true/false(默认)”></jsp:include>```

   4. 动态包含（运行时包含）：当服务器运行 JSP 页面对应的。class 文件时，页面将指定的页面包含过来一起显示。

```jsp
<!--动态包含-->
<jsp:include page = "sub_page.jsp"></jsp:include>
<div style ="color:#FF0000">这是主页面</div>
<jsp:include page = "sub_page.jsp"></jsp:include>
```

```<jsp:param>```标签：传递数据，jsp:param标签不能单独使用，必须作为jsp:include、jsp:forward、jsp:params标签的子标签。

1. ```<jsp:forward>```标签：转发。

2. 格式：```<jsp:forward page=“页面名”></jsp:forward>```

```jsp

<jsp:include page="sub_page.jsp">
 <jsp:param values="123" name="msg"/>
</jsp:include>
<div style="color:#0000FF">
    这是子页面
</div>
<%=request.getParameter("msg") %>

```

4. 注释
   1. html注释：```<!--注释内容-->```，在浏览器源码中可以看到，只能注释html标签。
   2. JSP注释：```<%--注释内容--%>```，在浏览器源码中看不到，可以注释动态元素与静态元素。

### 8.6. 六、JSP内置对象

1. JSP页面中预先声明并创建了9个对象。这些对象在JSP页面中可以直接使用，不需要再手动创建

   <table>
       <tr><td>类型</td><td>名称</td></tr>
       <tr><td>javax.servlet.HttpServletRequest</td><td>request</td></tr>
       <tr><td>javax.servlet.HttpServletResponse</td><td>response</td></tr>
       <tr><td>javax.servlet.jsp.PageContext</td><td>pageContext</td></tr>
           <tr><td>javax.servlet.http.HttpSession</td><td>session</td></tr>
       <tr><td>javax.servlet.ServletContext</td><td>application</td></tr>
          <tr><td>java.servlet.jsp.JspWriter</td><td>out</td></tr>
       <tr><td>java.lang.Throwable</td><td>exception</td></tr>
       <tr><td>javax.servlet.ServletConfig</td><td>config</td></tr>
       <tr><td>java.lang.Object</td><td>page</td></tr>
   </table>

## 9. 客户端验证与服务器端验证

### 9.1. 一、客户端验证：在浏览器中使用JS代码对数据进行验证

1. 优点：不占用网络资源、速度快
2. 缺点：存在浏览器兼容性问题

### 9.2. 二、服务器端验证：在服务器中使用Java代码对数据进行验证

1. 优点：不存在浏览器兼容性问题
2. 缺点：占用网络资源、速度慢

## 10. 范围对象（域对象）

### 10.1. 一、在javaweb项目只有4个范围对象

### 10.2. 二、四个范围对象的生命周期（从大到小）

1. ```javax.servlet.ServletContext```

   也称为application，当服务器启动时创建，当服务器关闭时销毁。一个服务器中所有的web站点共用一个application对象。通常用于保存服务器的信息

   ```java

   // 获得当前服务器 ServletContext 对象
   ServletContext application = this.getServletContext();
   // 向 ServletContext 中添加传递数据
   application.setAttribute("message","<script>alert('服务器异常，请与管理员联系');</script>");

   ```

2. ```javax.servlet.http.HttpSession```：是用于解决HTTP协议无状态的方法之一。当浏览器向服务器发出第一个请求时，服务器会为浏览器创建session对象。当session超时或关闭浏览器，或调用session的invalidate()方法都会销毁session对象。session与用户是一对一的关系，所以session通常用于保存用户的个人信息（如登录用户信息，购物车等）。

   ```java

   // 获得 session 方法一：如果浏览器有 session 对象则返回 session。如果浏览器没有 session 对象则返回 null
   //         HttpSession session1 = req.getSession();
   // 获得 session 方法二：如果浏览器有 session 对象则返回 session。如果浏览器没有 session 对象则为浏览器创建新的 session 对象（推荐使用）
      HttpSession session2 = req.getSession(true);

   ```

   ```java

   // 获得 session 的 ID
            System.out.println(session2.getId());
   // 获得 session 的创建时间，返回 long 类型
            System.out.println(session2.getCreationTime());
   // 获得 session 最后一次被访问的时间，返回 long 类型
         System.out.println(session2.getLastAccessedTime());

   ```

   ```java

            // 设置单个 session 的有效时间
            // 获得 session 的有效时间，单位为秒
            System.out.println(session2.getMaxInactiveInterval());
            // 设置 session 的有效时间
            session2.setMaxInactiveInterval(60 *60);
    System.out.println(session2.getMaxInactiveInterval());

   ```

   ```xml

     <!-- 设置当前站点中的 Session 的有效时间 -->

     <session-config>

     <!-- 单位为分钟 -->

     <session-timeout>10</session-timeout>
     </session-config>

   ```

   ```java

   // 无条件销毁 session，当销毁 session 之后再向 session 中读取数据时，程序会抛出 java.lang.IllegalStateException
            session2.invalidate();
            session2.setAttribute("message", "<script>alert('服务器宕机了，请与管理员联系');</script>");

   ```

3. ```javax.servlet.http.httpServletRequest```：当浏览器向服务器发出请求，服务器接收到请求后会创建出request对象。当服务器对请求作出响应时，request对象会随之销毁。通常用于保存资源之间临时的数据。

4. ```javax.servlet.jsp.PageContext```：当JSP页面打开时创建，当JSP页面关闭时销毁。通常用于保存JSP页面之间临时的数据。

### 10.3. 三、范围对象常用方法

1. setAttribute(“名字”,“数据”)：将数据以指定的名字存入到范围对象中。
2. getAttribute(“名字”)：从范围对象中获得指定名字的数据，返回数据的类型一定为java.lang.object类型。
3. removeAttribute(“名字”)：从范围对象中移除指定名字的数据

### 10.4. 四、在JavaWeb项目中有三种情况可能会丢失SessionID：重定向、表单提交、超链接
