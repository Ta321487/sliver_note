# Mybatis

## 1、简介

### 1-1.什么是[Mybatis]

![在这里插入图片描述](https://img-blog.csdnimg.cn/949379db04eb46e696bda52e3c00eeda.png#pic_center)

Mybatis是一款优秀的**持久层框架**，它支持定制化SQL、存储过程以及高级映射。
  Mybatis避免了几乎所有的JDBC代码和手动设置参数以及获取结果集。
  MyBatis 可以通过简单的 XML 或注解来配置和映射原始类型、接口和 Java POJO（Plain Old Java Objects，普通老式 Java 对象）为数据库中的记录。
  MyBatis 本是apache的一个开源项目iBatis, 2010年这个项目由apache software foundation 迁移到了google code，并且改名为MyBatis 。2013年11月迁移到Github。

官网

```tex
https://mybatis.org/mybatis-3/zh/index.html
```



github地址

```tex
https://github.com/mybatis/mybatis-3

```



依赖

```xml
<!-- https://mvnrepository.com/artifact/org.mybatis/mybatis -->
<dependency>
    <groupId>org.mybatis</groupId>
    <artifactId>mybatis</artifactId>
    <version>3.5.7</version>
</dependency>

```



### 1-2.持久化

**数据持久化**

- 持久化就是将程序的数据在持久状态和瞬时状态转化的过程
- 内存：**断电即失**
- 数据库（jdbc）、io文件持久化
- 生活：冷藏，罐头。
  **为什么需要持久化？**
- 有一些对象，不能让他丢掉。
- 内存太贵了



### 1-3.持久层（名词，概念）

- Dao层，Service层，Controller层…
- 完成持久化工作的代码块
- 层界限十分明显。



### 1-4.为啥需要Mybatis？

- 帮助程序员将数据存入到数据库中。
- 方便
- 传统的JDBC代码太复杂了。简化。框架。自动化。
- 不用Mybatis也可以。更容易上手。技术没有高低之分



**特点**

**简单易学**：只要两个jar文件+配置几个sql映射文件易于学习

**灵活**： sql写在xml里，便于统一管理和优化。

**解除sql与程序代码的耦合：将业务逻辑和数据访问逻辑分离**，使系统的设计更清晰，。**sql和代码的分离，提高了可维护性。**

提供映射标签，支持对象与**数据库的orm字段关系映射**

提供对象关系映射标签，支持对象关系组建维护

提供xml标签，**支持编写动态sql。**

**最重要的一点：使用的人多！**



## 2、第一个Mybatis程序

思路：搭建环境——》导入Mybatis——》编写代码——》测试

### 2-1.搭建环境

```xml
<!--mysql依赖-->
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>5.1.49</version>
</dependency>
<!--mybatis依赖-->
<dependency>
    <groupId>org.mybatis</groupId>
    <artifactId>mybatis</artifactId>
    <version>3.5.3</version>
</dependency>
<!--junit 单元测试-->
<dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <version>4.13</version>
    <scope>test</scope>
</dependency>

```



### 2-2.创建模块

**1.编写mybatis核心配置文件**

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<!--configuration 核心配置文件-->
<configuration>
    <environments default="development">
        <environment id="development">
            <!--事务管理-->
            <transactionManager type="JDBC"/>
            <!--配置数据源-->
            <dataSource type="POOLED">
                <property name="driver" value="com.mysql.jdbc.Driver"/>
                <property name="url" value="jdbc:mysql://localhost:3306/mybatis?useSSL=true&amp;useUnicode=true&amp;characterEncoding=UTF-8"/>
                <property name="username" value="root"/>
                <property name="password" value="123"/>
            </dataSource>
        </environment>
    </environments>
    <mappers>
        <mapper resource="org/mybatis/example/BlogMapper.xml"/>
    </mappers>
</configuration>

```



**2.编写mybatis工具类**

```java
package cn.bloghut.dao.utils;

import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;

import java.io.IOException;
import java.io.InputStream;

/**
 * 获取SQLSessionFactory对----》sqlSession
 */
public class MybatisUtils {
    private static SqlSessionFactory factory;
    static {
        try {
            //使用mybatis第一步
            String resource = "mybatis-config";
            InputStream in = Resources.getResourceAsStream(resource);
            factory = new SqlSessionFactoryBuilder().build(in);

        } catch (IOException e) {
            e.printStackTrace();
        }

    }
    /**
     * 既然有了SqlSessionFactory，顾名思义，我们就可以从中获得SQLSession实例了
     * SQLSession 完全包含了面向库执行 SQL 命令所需的所有方法
     * @return
     */
    public static SqlSession getSqlSession(){
        return factory.openSession();
    }

}

```



**3.编写代码**

1. 实体类
2. Dao接口
3. 接口实现类

```xml
public class User implements Serializable {
    private int id;
    private String name;
    private String pwd;
    //省略toString ，get/set
} 

public interface UserDao {
    List<User> getUser();
} 
    
<!--绑定一个对应的Dao接口-->
<mapper namespace="cn.bloghut.dao.UserDao">
    <select id="getUser" resultType="cn.bloghut.pojo.User">
        select * from  users
    </select>
</mapper>   

```



**4.测试**

```java
@Test
public void test(){
    //第一步，获得SQLSession对象
    SqlSession sqlSession = MybatisUtils.getSqlSession();
    //执行SQL
    //方式一
    //UserDao userDao = sqlSession.getMapper(UserDao.class);
    //List<User> users = userDao.getUser();

    //方式二
    List<User> users = sqlSession.selectList("cn.bloghut.dao.UserDao.getUser");

    for (User user : users){
        System.out.println(user);
    }
    //关闭SQLSession
    sqlSession.close();
}

```





## 3、CRUD

### 3-1.namespace

namespace中的包名要和Dao/Mapper 接口的包名一致！

### 3-2.select

选择、查询语句
id ：就是对应的**namespace**接口中的方法名；
resuleType ：SQL语句执行的**返回值**
parameterType ：**参数类型**

**1.编写接口**

```java
/**
 * 根据id查询用户
 * @param id
 * @return
 */
User getUserById(int id);

```



**2.编写对应的mapper中的sql语句**

```xml
<select id="getUserById" resultType="cn.bloghut.pojo.User" parameterType="int">
    select * from users  where id = #{id}
</select>

```



**3.测试**

```java
@Test
public void t1() {
    SqlSession sqlSession = MybatisUtils.getSqlSession();
    UserMapper userMapper = sqlSession.getMapper(UserMapper.class);
    User user = userMapper.getUserById(1);
    System.out.println(user);

    sqlSession.close();
}

```



### 3-3.insert

```xml
<insert id="insert" parameterType="cn.bloghut.pojo.User">
    insert into users(name,pwd) values(#{name},#{pwd})
</insert>

```



### 3-4.update

```xml

<update id="update" parameterType="cn.bloghut.pojo.User">
    update users set name=#{name},pwd=#{pwd} where id = #{id}
</update>

```



### 3-5.delete

```xml
<delete id="delete" parameterType="int">
    delete from users where id = #{id}
</delete>

```

注意：增删改需要提交事务



### 3-6万能Map

  假设，我们的实体类，或者数据库中的表，字段或者参数过多，我们应当考虑使用Map！

```java
@Test
public void t5() {
    SqlSession sqlSession = MybatisUtils.getSqlSession();
    UserMapper userMapper = sqlSession.getMapper(UserMapper.class);
    Map<String, Object> map = new HashMap<>();
    map.put("username", "闲言");
    map.put("password", "111");
    userMapper.addUser2(map);
    sqlSession.commit();
    sqlSession.close();
}


void addUser2(Map<String,Object> map);

<insert id="addUser2" parameterType="Map">
    insert into users(name,pwd) values(#{username},#{password})
</insert>

```



- **Map** 传递参数，直接在sql中取出**key** 【parameterType=“Map”】
- **对象**传递参数，直接在sql中取对象的**属性**即可 【parameterType=“Object”】
- 只有一个基本类型参数的情况下，可以直接在sql中取到
- 多个参数用Map或注解



### 3-7模糊查询

1.Java代码执行的时候，传递通配符 %%

```java
List<User> userLike = userMapper.getUserLike("%闲%");

```



2.在sql拼接中使用通配符

```sql
select * from users where  name  like "%"#{value}"%"

```



## 4、配置解析

### 4-1、核心配置文件

```xml
mybatis-config.xml
configuration（配置）
properties（属性）
settings（设置）
typeAliases（类型别名）
typeHandlers（类型处理器）
objectFactory（对象工厂）
plugins（插件）
environments（环境配置）
environment（环境变量）
transactionManager（事务管理器）
dataSource（数据源）
databaseIdProvider（数据库厂商标识）
mappers（映射器）

```





### 4-2.environments（环境配置）

- MyBatis 可以配置成适应多种环境
  **不过要记住：尽管可以配置多个环境，但每个 SqlSessionFactory 实例只能选择一种环境。**
- 学会使用配置多套运行环境！
- Mybatis默认的事务管理器就是JDBC，连接池：**POOLED**



### 4-3.属性[properties](https://so.csdn.net/so/search?q=properties&spm=1001.2101.3001.7020)

  这些属性可以在外部进行配置，并可以进行动态替换。你既可以在典型的 Java 属性文件中配置这些属性，也可以在 properties 元素的子元素中设置。【**db.properties**】

编写一个配置文件

db.properties

```properties

driver=com.mysql.jdbc.Driver
url=jdbc:mysql://localhost:3306/mybatis?useSSL=false&useUnicode=true&characterEncoding=UTF8
username=root
password=123

```

在核心配置文件中映入

```xml
 <!--引入外部配置文件-->
    <properties resource="db.properties" />
<!--可以增加一些属性-->
    <properties resource="db.properties">
        <propertie name="username" value="root"/>
        <propertie name="password" value="123456"/>
    </properties>
```

- 可以直接在外部文件引入
- 可以在其中增加一些属性配置
- 如果两个文件有同一个字段，优先使用外部配置文件的



### 4-4.类型别名typeAliases

  存在别名的是为Java类型**设置一个短的名字**
  存在的意义仅用来**减少类完全限定的冗余**

```xml
<typeAliases>
    <typeAlias type="cn.bloghut.pojo.User" alias="user"/>
</typeAliases>

```



也可以**指定一个包名**，Mybatis会在包名下面搜索java Bean ，比如：
扫描实体类的包，它的默认别名**就是为这个类的类型**，首字母小写！

```xml
<typeAliases>
    <package name="cn.bloghut.pojo"/>
</typeAliases>

```



在实体类比较少的时候，使用第一种方式
  如果实体类十分多，建议使用第二种
  第一种可以DIY别名，第二种则不行，如果非要改，需要在实体上增加注解

```java
@Alias("user")
public class User implements Serializable {

```



### 4-5.映射器

MapperRegistry：注册绑定我们的**Mapper文件**；
方式一：【推荐使用】

```xml
<mappers>
    <mapper resource="cn/bloghut/dao/UserMapper.xml"/>
    <!--通配方式-->
    <mapper resource="cn/bloghut/dao/*Mapper.xml"/>
</mappers>

```



方式二：使用**class文件**绑定注册

```xml
<!--每一个Mapper.xml都需要在Mybatis核心配置文件中注册！-->
<mappers>
    <mapper class="cn.bloghut.dao.UserMapper"/>
</mappers>

```

注意点：
  接口和他的mapper文件都需要在Mybatis核心配置文件中注册
  接口和他的mapper文件配置文件必须再同一包下！



方式三：使用**扫描包注册**

```xml
<!--每一个Mapper.xml都需要在Mybatis核心配置文件中注册！-->
<package name="cn.bloghut.dao"/>
<mappers>
    <package name="cn.bloghut.dao"/>
</mappers>

```

注意点：
  接口和他的Mapper配置文件**必须同名**！
  接口和他的mapper文件配置文件**必须再同一包下**！



### 4-6[生命周期](https://so.csdn.net/so/search?q=生命周期&spm=1001.2101.3001.7020)和作用域

  不同作用域和生命周期类别是至关重要的，因为错误的使用会导致非常严重的并发问题。

![在这里插入图片描述](https://img-blog.csdnimg.cn/b9c55881c2054b27acaac8775de67d4d.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)



**SqlSessionFactoryBuilder**

- 一旦创建了 **SqlSessionFactory**，就不再需要它了。

- 局部变量

**SqlSessionFactory**

- SqlSessionFactory 一旦被创建就应该在应用的运行期间一直存在，**没有任何理由丢弃它或重新创建另一个实例。**
- SqlSessionFactory 的最佳作用域是应用作用域。
- 最简单的就是使用单例模式或者静态单例模式

**SqlSession**（相当于从连接池中获取一个连接）

- 连接到连接池的请求！
- 关闭
- SqlSession 的实例不是线程安全的，因此是不能被共享的，它的最佳的作用域是请求或方法作用域
- 用完之后需要赶紧关闭，
- 一个SQLSession 可以多次使用它的getMapper方法，获取多个mapper接口实例

打个比方：

1. SqlSessionFactoryBuilder 是造车公司
2. 造了100台车，然后买给租车公司（SQLSessionFactory），然后倒闭
3. SQLSession 用户 租车，使用车
4. mapper 用户的使用，用户租到车之后可以开去这，开去那，任凭使用
5. 用户（SQLSession） 执行完想做的事之后，必须归还“汽车” 给租车公司（SQLSessionFactory）

![在这里插入图片描述](https://img-blog.csdnimg.cn/3f86297314614d5791ec830002d6f8cb.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)

这里面的每一个**mapper** 就代表一个具体的**业务**。



## 5、解决属性名和字段名不一致的问题

数据库中的字段和JavaBean不一致的情况

```java
public class User {
    private int id;
    private String name;
    private String password;

```

![在这里插入图片描述](https://img-blog.csdnimg.cn/198aebe337c34d0e9ea97accf7cf9cb7.png#pic_center)

```xml
<select id="getUser" resultType="user">
    select id,name,pwd from  users
</select>

```



解决办法
起别名

```xml
<select id="getUser" resultType="user">
    select id,name,pwd as password from  users
</select>

```





**2、ResultMap 结果集映射**
resultMap 元素是 MyBatis 中最重要最强大的元素。
  ResultMap 的设计思想是，对简单的语句做到零配置，对于复杂一点的语句，只需要描述语句之间的关系就行了。
  MyBatis 会在幕后自动创建一个 ResultMap，再根据属性名来映射列到 JavaBean 的属性上。

![在这里插入图片描述](https://img-blog.csdnimg.cn/425f9324c77a4acfad1efba76328670b.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)

```xml
<resultMap id="UserMap" type="user">
    <id property="id" column="id"/>
    <!--column 数据库的字段，property JavaBean中的属性-->
    <result property="name" column="name"/>
    <result property="password" column="pwd"/>
</resultMap>

```



![在这里插入图片描述](https://img-blog.csdnimg.cn/e5f9e7f410354961bebd91ec2cd82e15.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)





## 6、日志

### 6-1.日志工厂

如果一个数据库操作出现了异常，我们需要排错。日志就是最好的助手！
曾经：debug、 sout
现在：日志工厂

![在这里插入图片描述](https://img-blog.csdnimg.cn/f60e644d44784c79ad0dc61e30798b5e.png#pic_center)



- SLF4J
- LOG4J 【掌握】
- LOG4J2
- JDK_LOGGING
- COMMONS_LOGGING
- STDOUT_LOGGING
- NO_LOGGING

**STDOUT_LOGGING标准日志输出**

```xml
<!--设置日志-->
<settings>
    <setting name="logImpl" value="STDOUT_LOGGING"/>
</settings>

```



![在这里插入图片描述](https://img-blog.csdnimg.cn/28b3ff1ab37e4b6fafd1bfdd81bf3033.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)



### 6-2.LOG4J

**什么是LOG4J**

- Log4j是Apache的一个开源项目
- 通过使用Log4j，我们可以控制日志信息输送的目的地是控制台、文件、GUI组件
- 我们可以控制每一条日志的输出格式；
- 通过定义每一条日志信息的级别，我们能够更加细致地控制日志的生成过程。
- 通过一个配置文件来灵活地进行配置，而不需要修改应用的代码。

**1.先导入LOG4J的依赖**

```xml
<dependency>
            <groupId>log4j</groupId>
            <artifactId>log4j</artifactId>
            <version>1.2.17</version>
</dependency>

```



**2.编写log4j.properties文件**

```tex
### 配置根 ###
log4j.rootLogger = debug,console ,fileAppender,dailyRollingFile,ROLLING_FILE,MAIL,DATABASE

### 设置输出sql的级别，其中logger后面的内容全部为jar包中所包含的包名 ###
log4j.logger.org.apache=debug
log4j.logger.java.sql.Connection=debug
log4j.logger.java.sql.Statement=debug
log4j.logger.java.sql.PreparedStatement=debug
log4j.logger.java.sql.ResultSet=debug

### 配置输出到控制台 ###
log4j.appender.console = org.apache.log4j.ConsoleAppender
log4j.appender.console.Target = System.out
log4j.appender.console.layout = org.apache.log4j.PatternLayout
log4j.appender.console.layout.ConversionPattern =  %d{ABSOLUTE} %5p %c{1}:%L - %m%n

### 配置输出到文件 ###
log4j.appender.fileAppender = org.apache.log4j.FileAppender
log4j.appender.fileAppender.File = logs/log.log
log4j.appender.fileAppender.Append = true
log4j.appender.fileAppender.Threshold = DEBUG
log4j.appender.fileAppender.layout = org.apache.log4j.PatternLayout
log4j.appender.fileAppender.layout.ConversionPattern = %-d{yyyy-MM-dd HH:mm:ss}  [ %t:%r ] - [ %p ]  %m%n

### 配置输出到文件，并且每天都创建一个文件 ###
log4j.appender.dailyRollingFile = org.apache.log4j.DailyRollingFileAppender
log4j.appender.dailyRollingFile.File = logs/log.log
log4j.appender.dailyRollingFile.Append = true
log4j.appender.dailyRollingFile.Threshold = DEBUG
log4j.appender.dailyRollingFile.layout = org.apache.log4j.PatternLayout
log4j.appender.dailyRollingFile.layout.ConversionPattern = %-d{yyyy-MM-dd HH:mm:ss}  [ %t:%r ] - [ %p ]  %m%n

### 配置输出到文件，且大小到达指定尺寸的时候产生一个新的文件 ###
log4j.appender.ROLLING_FILE=org.apache.log4j.RollingFileAppender 
log4j.appender.ROLLING_FILE.Threshold=ERROR 
log4j.appender.ROLLING_FILE.File=rolling.log 
log4j.appender.ROLLING_FILE.Append=true 
log4j.appender.ROLLING_FILE.MaxFileSize=10KB 
log4j.appender.ROLLING_FILE.MaxBackupIndex=1 
log4j.appender.ROLLING_FILE.layout=org.apache.log4j.PatternLayout 
log4j.appender.ROLLING_FILE.layout.ConversionPattern=[framework] %d - %c -%-4r [%t] %-5p %c %x - %m%n

4j.appender.A1.layout=org.apache.log4j.xml.XMLLayout

```



**3.配置log4j为日志实现**

```xml
<!--设置日志-->
<settings>
    <setting name="logImpl" value="LOG4J"/>
</settings>

```



**4.测试**

![在这里插入图片描述](https://img-blog.csdnimg.cn/9d78bb50529f4334b8902b3e069a282c.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)



### 6-3简单使用

  **1.在要使用log4j的类中导入Apache的包**

```java
import org.apache.log4j.Logger;

```

**2.日志对象，参数为当前类的class**

```java
static Logger logger = Logger.getLogger(UserTest.class);

```

**3.使用**

```java
日志级别
info
debug
error
@Test
public void testLog4j(){
    logger.info("info:进入了testLog4j方法");
    logger.debug("debug:进入了testLog4j方法");
    logger.error("error:进入了testLog4j方法");
}

```

![在这里插入图片描述](https://img-blog.csdnimg.cn/6b870f1113c647eb957162147c14f01d.png#pic_center)





## 7、分页

**思考：为什么要分页？**
  减少数据的处理量

### 7-1.使用Limit分页

  语法：`select * from users limit startIndex,PageSize;`

**1.接口**

```java
/**
 * 分页查询用户
 * @param map
 * @return
 */
List<User> getUserByLimit(Map<String,Object> map);

```



**2.映射文件**

```xml
<select id="getUserByLimit" resultMap="UserMap" parameterType="map">
    select * from users limit #{currentPage},#{pageSize}
</select>

```



**3.测试**

```java
@Test
public void t4(){
    SqlSession sqlSession = MybatisUtils.getSqlSession();
    UserMapper userMapper = sqlSession.getMapper(UserMapper.class);
    Map<String,Object> map = new HashMap<>();
    map.put("currentPage",0);
    map.put("pageSize",2);
    List<User> users =  userMapper.getUserByLimit(map);
    for (User user : users) {
        System.out.println(user);
    }
    sqlSession.close();
}

```



### 7-2.RowBounds分页

  不再使用SQL实现分页
**1.接口**

```java
/**
 * 使用RowBounds实现分页
 * @return
 */
List<User> getUserByRowBounds();

```



**2.mapper.xml**

```xml
<select id="getUserByRowBounds" resultMap="UserMap">
    select * from users 
</select>

```



**3.测试**

```java
@Test
public void t5(){
    SqlSession sqlSession = MybatisUtils.getSqlSession();
    RowBounds rowBounds = new RowBounds(0, 2);
    //通过Java代码层实现分页
    List<User> users = sqlSession.selectList("cn.bloghut.dao.UserMapper.getUserByRowBounds", null, rowBounds);
    for (User user : users) {
        System.out.println(user);
    }
    sqlSession.close();
}

```



### 7-3.分页插件

官网

```http
https://pagehelper.github.io/

```

![在这里插入图片描述](https://img-blog.csdnimg.cn/0d2f8cc0981d46c59023cc45e4c71ac6.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)





## 8、注解开发

### 8-1.面向接口编程

  大家之前都学过面向对象编程，也学习过接口，但在真正的开发中，很多时候我们会选择面向接口编程。

  根本原因:**解耦，可拓展，提高复用，分层开发中，上层不用管具体的实现，大家都遵守共同的标准，使得开发变得容易，规范性更好**

  在一个面向对象的系统中，系统的各种功能是由许许多多的不同对象协作完成的。在这种情况下，各个对象内部是如何实现自己的,

**对系统设计人员来讲就不那么重要了**;

  而各个对象之间的协作关系则成为系统设计的关键。**小到不同类之间的通信，大到各模块之间的交互，在系统设计之初都是要着重考虑的，这也是系统设计的主要工作内容。**面向接口编程就是指按照这种思想来编程。

关于接口的理解
  接口从更深层次的理解，应是**定义(规范，约束)**与**实现(名实分离的原则）的分离**。
  接口的本身反映了系统设计人员**对系统的抽象理解**。

接口应有两类:
    第一类是对**一个个体的抽象**，它可对应为一个抽象体(abstract class);
    第二类是对**一个个体某一方面的抽象**，即形成一个抽象面(interface) ;
一个体有可能有多个抽象面。抽象体与抽象面是有区别的。

三个面向区别
  面向对象是指，我们考虑问题时，**以对象为单位**，考虑它的属性及方法．
  面向过程是指，我们考虑问题时，**以一个具体的流程**（事务过程)为单位，考虑它的实现.
  接口设计与非接口设计是针对复用技术而言的，与面向对象（过程)不是一个问题.更多的体现就是对系统整体的架构

### 8-2.使用注解开发

**1.注解在接口上实现**

```java
@Select("select * from users")
List<User> getUsers();

```



**2.需要在核心配置文件中绑定接口！**

```xml
<!--绑定接口-->
<mappers>
    <mapper class="cn.bloghut.dao.UserMapper"/>
</mappers>

```



**3.测试**

  本质：反射机制实现
  底层：动态代理！



### 8-3.Mybatis详细的执行流程！

![在这里插入图片描述](https://img-blog.csdnimg.cn/3df5c8d6304c498d9279d324e8f0a6c1.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_17,color_FFFFFF,t_70,g_se,x_16#pic_center)



### 8-4.CRUD

在配置文件绑定Mapper接口位置

```xml
<mappers>
    <mapper class="cn.bloghut.dao.UserMapper"/>
</mappers>

```



我们可以在工具类创建的时候实现自动提交事务！

```java
/**
 * 既然有了SqlSessionFactory，顾名思义，我们就可以从中获得SQLSession实例了
 * SQLSession 完全包含了面向库执行 SQL 命令所需的所有方法
 * @return
 */
public static SqlSession getSqlSession(){
    return factory.openSession(true);
}

```



接口

```java
public interface UserMapper {

    @Select("select * from users")
    List<User> getUsers();

    /**
     * 方法存在多个参数，所有的参数前面必须加上 @Param 注解
     * @param id
     * @return
     */
    @Select("select * from users where id = #{id}")
    User getUserById(@Param("id") int id);

    @Insert("insert into users(name,pwd) values(#{name},#{password})")
    int insert(User user);

    @Update("update  users  set name=#{name},pwd=#{password} where id = #{id}")
    int update(User user);

    @Delete("delete from users where id = #{id}")
    int delete(@Param("id")int id);
}

```



测试

```java
public class T {

    @Test
    public void t1() {
        SqlSession sqlSession = MybatisUtils.getSqlSession();
        //底层主要应用反射
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        List<User> users = mapper.getUsers();
        for (User user : users) {
            System.out.println(user);
        }
        sqlSession.close();

    }

    @Test
    public void t2() {
        SqlSession sqlSession = MybatisUtils.getSqlSession();
        //底层主要应用反射
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        User user = mapper.getUserById(1);
        System.out.println(user);
        sqlSession.close();

    }

    @Test
    public void t3() {
        SqlSession sqlSession = MybatisUtils.getSqlSession();
        //底层主要应用反射
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        User user = new User();
        user.setName("xian");
        user.setPassword("321");
        int flag = mapper.insert(user);
        System.out.println(flag);
        sqlSession.close();

    }
    @Test
    public void t4() {
        SqlSession sqlSession = MybatisUtils.getSqlSession();
        //底层主要应用反射
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        User user = new User();
        user.setId(12);
        user.setName("xy");
        user.setPassword("321");
        int flag = mapper.update(user);
        System.out.println(flag);
        sqlSession.close();
    }
    @Test
    public void t5() {
        SqlSession sqlSession = MybatisUtils.getSqlSession();
        //底层主要应用反射
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        int flag = mapper.delete(12);
        System.out.println(flag);
        sqlSession.close();
    }
}

```



关于@**Param**注解

1. **基本类型**的参数或者String类型，**需要加上**
2. 引用类型不需要加
3. 如果只有一个基本类型的话，可以忽略，但是**建议都加上**
4. 我们在SQL中引用的就是我们这里的@Param(“uid”)中设定的属性名



**\#{} 和 ${} 区别**

```http
https://blog.csdn.net/weixin_41231928/article/details/105120292

```



## 9、Lombox

**1.安装插件方便使用的第三方工具**

![在这里插入图片描述](https://img-blog.csdnimg.cn/87edfaa8fa09431fb3976c78812facb6.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)



**2.导入依赖**

```xml
<!--Lombox 依赖-->
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>1.16.16</version>
</dependency>

```



**3.在实体类上使用**

```java
@Data
@AllArgsConstructor
@NoArgsConstructor
public class User {
    private int id;
    private String name;
    private String password;
}

```

```java
@Getter and @Setter
@FieldNameConstants  
@ToString
@EqualsAndHashCode
@AllArgsConstructor    全参构造方法
@RequiredArgsConstructor and 
@NoArgsConstructor     无参构造方法
@Log, @Log4j, @Log4j2, @Slf4j, @XSlf4j, @CommonsLog, @JBossLog, @Flogger, @CustomLog
@Data
@Builder
@SuperBuilder
@Singular
@Delegate
@Value
@Accessors
@Wither
@With
@SneakyThrows
@val
@var
experimental @var
@UtilityClass
Lombok config system

```



加@Data注解之前

![在这里插入图片描述](https://img-blog.csdnimg.cn/26729c3b6a2f4cde9fdd03120c295d88.png#pic_center)



![在这里插入图片描述](https://img-blog.csdnimg.cn/b2bf801eaf6f4a3f96f7144dfebaa824.png#pic_center)



加@Data注解之后

![在这里插入图片描述](https://img-blog.csdnimg.cn/ef8e587188514de2bc55a3c142bba749.png#pic_center)

![在这里插入图片描述](https://img-blog.csdnimg.cn/ee1d237b0e90401f94344fc518b7a5ad.png#pic_center)



**常见注解说明**

```java
@Data：无参构造、get、set、toString、equals、hashCode
@AllArgsConstructor：有参构造
@NoArgsConstructor：无参构造
@toString：toString()方法

```



## 10、多对一处理

![在这里插入图片描述](https://img-blog.csdnimg.cn/5d7bbf68133c43a68a21957464baa5bf.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)

多个学生，对应一个老师
  对于学生这边而言，关联…多个学生，关联一个老师【多对一】
  对于老师而言，集合，一个老师，有很多学生【一对多】



### 10-1.按照结果嵌套处理

```xml
<!--自定义返回值-->
<resultMap id="StudentTeacher" type="Student">
    <id column="id" property="id"/>
    <result column="name" property="name"/>
    <!--复杂的属性，我们需要单独处理
        对象：association
        集合：collection
    -->
    <association property="teacher" column="tid" javaType="Teacher" select="getTeacherById"/>
</resultMap>

<!--查询所有学生-->
<select id="getStudents" resultMap="StudentTeacher">
    select * from student
</select>

<!--根据教师id查询教师信息-->
<select id="getTeacherById" resultType="Teacher">
    select * from teacher where id = #{id}
</select>

```



### 10-2.按照查询嵌套处理

```xml
<select id="getStudents2" resultMap="StudentTeacher2">
    select
           student.id as sid,
           student.name as sname,
           teacher.name as tname
    from student,teacher
    where student.tid = teacher.id
</select>

<resultMap id="StudentTeacher2" type="Student">
    <id column="id" property="sid"/>
    <result column="name" property="sname"/>
    <association property="teacher" javaType="Teacher">
        <result property="name" column="tname"/>
    </association>
</resultMap>

```

**mybatis多对一查询方式
子查询
连表查询**



## 11、一对多处理

比如：一个老师拥有多个学生！
对于老师而言，就是一对多关系

实体类

```java
@AllArgsConstructor
@NoArgsConstructor
@Data
public class Teacher {
    private int id;
    private String name;
    private List<Student> students;
}

```



区别

```java
@Data
@AllArgsConstructor
@NoArgsConstructor
public class Student {
    private int id;
    private String name;
    private int tid;
}

```



### 11-1.按照查询嵌套处理

```xml
<resultMap id="TeacherStudent" type="Teacher">
    <id column="tid" property="id"/>
    <result column="tname" property="name"/>
    <!--
        复杂的属性，我们需要单独处理
        对象：association
        集合：collection
        javaType：指定的属性类型
        ofType：集合中的泛型信息
    -->
    <collection property="students" ofType="Student">
        <result property="id" column="sid"/>
        <result property="name" column="sname"/>
        <result property="tid" column="tid"/>
    </collection>
</resultMap>

<!--获取指定老师下的所有学生信息-->
<select id="getTeacherById" resultMap="TeacherStudent" parameterType="int">
   select t.id tid,t.name tname,s.id sid,s.name sname
    from teacher t,student s
    where  s.tid = t.id and  t.id = #{id}
</select>

```



### 11-2按照结果嵌套处理

```xml
<select id="getTeacherById2" resultMap="TeacherStudent2" parameterType="int">
    select * from teacher where id = #{id}
</select>

<resultMap id="TeacherStudent2" type="Teacher">
    <id property="id" column="id"/>
    <result property="name" column="name"/>
    <collection property="students" javaType="ArrayList" ofType="Student" select="cn.bloghut.dao.StudentMapper.getStudentsByTid" column="id"/>
</resultMap>

<!--这个方法是在Student mapper文件中的-->
<select id="getStudentsByTid"  resultType="Student">
    select * from student where tid = #{id}
</select>

```



**小结**
  关联-**association **【多对一】
  集合-**collection** 【一对多】
  JavaType & ofType
    **JavaType** 用来指定**实体类中的类型**的
    **ofType** 用来指定映射到**List 集合中的pojo类型 ，泛型中的约束类型**



**注意点：**

- 保证SQL的可读性，尽量保证通俗易懂
- 注意一对多和多对一中，属性名和字段的问题！
- 如果问题不好排查，可以使用日志，建议使用log4j

**面试高频**

1. Mysql引擎
2. InnoDB底层原理
3. 索引
4. 索引优化！



## 12、动态SQL

  什么是动态SQL：动态SQL就是**根据不同的条件生成不同的SQL语句**

```java
if
choose (when, otherwise)
trim (where, set)
foreach

```





### 12-1.if标签

这里需要用到1 = 1，因为1=1 这个条件无论如何都满足的 后面的条件 and 拼接才能成功。

```xml
<select id="queryBlogIF" resultType="Blog" parameterType="map">
    select * from blog where 1 = 1
    <if test="title != null">
        and title = #{title}
    </if>
    <if test="author != null">
        and author = #{author}
    </if>
</select>

```



### 12-2.where标签

  使用where标签可以排除掉 1= 1，如果我们没有设置查询条件，mybatis自动把 where标签去掉。

 where 元素只会**在子元素返回任何内容的情况下才插入** “WHERE” 子句。而且，若子句的开头为 “AND” 或 “OR”，where 元素也会将它们去除。

```xml
<select id="queryBlogWhere" resultType="Blog" parameterType="map">
    select * from blog
    <where>
        <if test="title != null">
            title = #{title}
        </if>
        <if test="author != null">
            and author = #{author}
        </if>
    </where>
</select>

```



### 12-3.Choose标签

  类似Java中的switch，**只满足一个**，如果都不满足，则执行outherwise

```xml
<select id="queryBlogChoose" resultType="Blog" parameterType="map">
    select * from blog
    <where>
        <choose>
            <when test="title != null">
                title = #{title}
            </when>
            <when test="author != null">
                and author = #{author}
            </when>
            <otherwise>
                and views = #{views}
            </otherwise>
        </choose>
    </where>
</select>

```



### 12-4.set标签

  set 元素会**动态地在行首插入 SET 关键字**，并会**删掉额外的逗号**。

```xml
<update id="updateBlog" parameterType="map">
    update blog
    <set>
        <if test="title != null">
            title=#{title},
        </if>
        <if test="author != null">
            author = #{author}
        </if>
    </set>
    where id = #{id}
</update>

```



 **所谓动态SQL，本质还是SQL语句，只是我们在SQL层面，去执行一个逻辑代码**



### 12-5.SQL片段

有时候，我们可能会将一些功能的部分抽取出来，方便复用

1.使用SQL标签抽取公共的部分

```xml
    <sql id="if-title-author">
        <if test="title!=null">
            title=#{title}
        </if>
        <if test="author!=null">
            and author=#{author}
        </if>
    </sql>
```

2.在需要使用的地方使用include标签引用即可

```xml
  <select id="queryBlogIF" parameterType="map" resultType="Blog">
        select * from blog
        <where>
        <include refid="if-title-author"></include>
        </where>
    </select>
```

注意事项：

- 最好基于单表来定义SQL片段！
- 不要存放where标签



### 12-6.foreach

  foreach 元素的功能非常强大，它允许**你指定一个集合**，声明可以在元素体内使用的**集合项（item）和索引（index）变量**。它也允许你指定开头与结尾的字符串以及集合项迭代之间的**分隔符**。这个元素也不会错误地添加多余的分隔符，看它多智能！

  提示 你可以将任何可迭代对象（如 **List**、**Set** 等）、**Map 对象**或者**数组对象**作为集合参数传递给 foreach。当使用可迭代对象或者数组时，**index 是当前迭代的序号，item 的值是本次迭代获取到的元素**。当使用 Map 对象（或者 Map.Entry 对象的集合）时，index 是键，item 是值。

**官方例子**

```xml
<select id="selectPostIn" resultType="domain.blog.Post">
  SELECT *
  FROM POST P
  WHERE ID in
  <foreach item="item" index="index" collection="list"
      open="(" separator="," close=")">
        #{item}
  </foreach>
</select>

```



- **in**： 类似一个区间
- **item**： 当前元素
- **index**： 当前迭代号，类似数组下标
- **open**：开头
- **separator**：分割
- **close**：结尾



**例：**

```xml
<select id="blogIds" parameterType="list" resultType="Blog">
    select * from blog
    where id in
    <foreach collection="list" item="blog" index="index"  open="(" separator="," close=")">
         #{blog}
    </foreach>
</select>

```

**或者**

```xml
<select id="blogIds2" resultType="Blog" parameterType="map">
    select * from blog
    <where>
        <foreach collection="list" item="id" open=" (" separator="or" close=")">
            id = #{id}
        </foreach>
    </where>
</select>

```



**动态SQL就是在拼接SQL语句，我们只要保证SQL的正确性，按照SQL的格式，去排列**组合就可以了

建议：

- 先在Mysql中写出完整的SQL，再对应的去修改成为我们的动态SQL实现通用即可！



## 13、缓存

### 13-1.简介

查询 ： 连接数据库 ：耗资源！
**一次查询的结果，给他暂存到一个可以直接取到的地方！—》内存 ： 缓存**

我们再次查询相同数据的时候，直接走缓存，就不用走数据库了

#### 1.什么是缓存(Cache)？

- **存在内存中的临时数据**
- 将用户经常查询的数据放在缓存（内存)，用户去查询数据就不用从磁盘上的（关系型数据库数据文件）查询，从缓存中查询，从而提高程序效率，解决了高并发的性能问题。

#### 2.为什么使用缓存？

- 减少和数据库的**交互次数**，减少系统**开销**，提高**系统效率**

#### 3.什么样的数据能使用缓存？

经常**查询**且**不改变**的数据。

**缓存的重要性是不言而喻的。 使用缓存， 我们可以避免频繁的与数据库进行交互， 尤其是在查询越多、缓存命中率越高的情况下， 使用缓存对性能的提高更明显。**



### 13-2.Mybatis 缓存

  MyBatis 包含一个非常强大的查询缓存特性,它可以非 常方便地配置和定制。缓存可以极大的提升查询效率。

- MyBatis系统中默认定义了**两级缓存**。 **一级缓存和二级缓存**。
- **默认**情况下，只有**一级缓存**（SqlSession级别的缓存， 也称为本地缓存）**开启**。
- 二级缓存需要手动开启和配置，他是基于namespace级 别的缓存。
- 为了提高扩展性。MyBatis定义了缓存接口Cache。我们可以通过实现Cache接口来自定义二级缓存，将缓存数据保存到三方缓存里。





### 13-3.一级缓存（本地缓存）

- 与数据库同一次会话期间查询到的数据会放在本地缓存中
- 以后如果需要获取相同的数据，直接从缓存中取，没必要再去查询数据库。
- 一级缓存是sqlSession级别的缓存，默认一直是开启的。

**测试步骤：**

- 开启日志
- 测试在一个Session中查询两次相同记录
- 查看日志输出

![在这里插入图片描述](https://img-blog.csdnimg.cn/1da099a1ff4646168a06cd8713b366aa.png#pic_center)



**缓存失效情况**

- 查询不同的东西
- 增删改操作，可能会改变原来的数据，所以必定会刷新缓存
- 查询不同的Mapper.xml
- 手动清理缓存

```java
@Test
public void  t2(){
    SqlSession sqlSession = MybatisUtils.getSqlSession();
    UserMapper mapper = sqlSession.getMapper(UserMapper.class);
    User user = mapper.getUserById(1);
    System.out.println("==================");

    User user1 = new User();
    user1.setId(2);
    user1.setName("咸鱼");
    user1.setPwd("123456");
    mapper.update(user1);

    User user2 = mapper.getUserById(1);
    System.out.println(user == user2);
    sqlSession.close();
}

```

![在这里插入图片描述](https://img-blog.csdnimg.cn/09f740f1583d41c184eb6302849fc662.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)





查询不同的Mapper.xml
手动清除

```java
@Test
public void  t2(){
    SqlSession sqlSession = MybatisUtils.getSqlSession();
    UserMapper mapper = sqlSession.getMapper(UserMapper.class);
    User user = mapper.getUserById(1);
    System.out.println("==================");
    sqlSession.clearCache();//手动清理缓存
    User user2 = mapper.getUserById(1);
    System.out.println(user == user2);
    sqlSession.close();
}

```

![在这里插入图片描述](https://img-blog.csdnimg.cn/e11fea2445e2497fbedf7a94447f7e85.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)

**小结：一级缓存默认是开启的，只在一次SQLSession中有效，也就是拿到连接 到关闭连接这个区间有效。**

一级缓存就是一个map。



### 13-4.二级缓存（全局缓存）

  基于**namespace**级别的缓存，一个namespace对应一个二级缓存。

工作机制：

1. 一个会话，查询一条数据，这个数据就会被放在当前的一级缓存中。
2. 如果会话关闭，一级缓存中的数据会被保存到二级缓存中，新的会话查询信息，就可以参照二级缓存。
3. sqlSession即通过EmployeeMapper查询Employee，也通过DepartmentMapper查询Department，不同namespace查出的数据会放在自己对应的缓存中（map）。



使用步骤：
开启全局缓存

```xml
<!--显示的开启全局缓存-->
<setting name="cacheEnabled" value="true"/>

```



在要使用二级缓存的Mapper.xml中开启

```xml
<!--在当前Mapper.xml中使用二级缓存-->
<cache/>

```

也可以自定义参数

```xml
<cache
     eviction="FIFO"
     flushInterval="6000"
     size="512"
     readOnly="true"/>
```

各个属性意义如下：

- eviction：缓存回收策略
  - LRU：最少使用原则，移除最长时间不使用的对象
  - FIFO：先进先出原则，按照对象进入缓存顺序进行回收
  - SOFT：软引用，移除基于垃圾回收器状态和软引用规则的对象
  - WEAK：弱引用，更积极的移除移除基于垃圾回收器状态和弱引用规则的对象
- flushInterval：刷新时间间隔，单位为毫秒，这里配置的100毫秒。如果不配置，那么只有在进行数据库修改操作才会被动刷新缓存区
- size：引用额数目，代表缓存最多可以存储的对象个数
- readOnly：是否只读，如果为true，则所有相同的sql语句返回的是同一个对象（有助于提高性能，但并发操作同一条数据时，可能不安全），如果设置为false，则相同的sql，后面访问的是cache的clone副本。



xml文件

```xml
<select id="queryUsersById" resultType="user" useCache="true">
    select * from `users` where id=#{id}
</select>
```

如果没有去配置flushCache、useCache，那么默认是启用缓存的

- flushCache默认为false，表示任何时候语句被调用，都不会去清空本地缓存和二级缓存。
- useCache默认为true，表示会将本条语句的结果进行二级缓存。
- 在insert、update、delete语句时： flushCache默认为true，表示任何时候语句被调用，都会导致本地缓存和二级缓存被清空。 useCache属性在该情况下没有。update 的时候如果 flushCache="false"，则当你更新后，查询的数据数据还是老的数据。



**测试**
我们需要将实体类序列化！否则就会报错！

**如果使用的是<cache/>没有配置参数的情况下，需要给实体类开启序列化**

```java
public class User implements Serializable
```



小结：

1. 只要开启了二级缓存，在同一个Mapper下就有效
2. 所有的数据都会先放在一级缓存中；
3. 只有当会话提交，或者会话关闭的时候，才会提交到二级缓存中



### 13-5.缓存原理

![在这里插入图片描述](https://img-blog.csdnimg.cn/4a6c77d9369a49349b657ca154dab5c2.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)



### 13-6.自定义缓存-ehcache

Ehcache是一种广泛使用的开源Java分布式缓存。

**1.导入依赖**

```xml
<!--ehcache-->
<dependency>
    <groupId>org.mybatis.caches</groupId>
    <artifactId>mybatis-ehcache</artifactId>
    <version>1.1.0</version>
</dependency>

```



**2.在mapper文件中设置**

```xml
<cache type="org.mybatis.caches.ehcache" />
```



**3.编写ehcache配置文件**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<ehcache xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:noNamespaceSchemaLocation="http://ehcache.org/ehcache.xsd"
         updateCheck="false">
    <!--
       diskStore：为缓存路径，ehcache分为内存和磁盘两级，此属性定义磁盘的缓存位置。参数解释如下：
       user.home – 用户主目录
       user.dir  – 用户当前工作目录
       java.io.tmpdir – 默认临时文件路径
     -->
    <diskStore path="java.io.tmpdir/Tmp_EhCache"/>
    <!--
       defaultCache：默认缓存策略，当ehcache找不到定义的缓存时，则使用这个缓存策略。只能定义一个。
     -->
    <!--
      name:缓存名称。
      maxElementsInMemory:缓存最大数目
      maxElementsOnDisk：硬盘最大缓存个数。
      eternal:对象是否永久有效，一但设置了，timeout将不起作用。
      overflowToDisk:是否保存到磁盘，当系统宕机时
      timeToIdleSeconds:设置对象在失效前的允许闲置时间（单位：秒）。仅当eternal=false对象不是永久有效时使用，可选属性，默认值是0，也就是可闲置时间无穷大。
      timeToLiveSeconds:设置对象在失效前允许存活时间（单位：秒）。最大时间介于创建时间和失效时间之间。仅当eternal=false对象不是永久有效时使用，默认是0.，也就是对象存活时间无穷大。
      diskPersistent：是否缓存虚拟机重启期数据 Whether the disk store persists between restarts of the Virtual Machine. The default value is false.
      diskSpoolBufferSizeMB：这个参数设置DiskStore（磁盘缓存）的缓存区大小。默认是30MB。每个Cache都应该有自己的一个缓冲区。
      diskExpiryThreadIntervalSeconds：磁盘失效线程运行时间间隔，默认是120秒。
      memoryStoreEvictionPolicy：当达到maxElementsInMemory限制时，Ehcache将会根据指定的策略去清理内存。默认策略是LRU（最近最少使用）。你可以设置为FIFO（先进先出）或是LFU（较少使用）。
      clearOnFlush：内存数量最大时是否清除。
      memoryStoreEvictionPolicy:可选策略有：LRU（最近最少使用，默认策略）、FIFO（先进先出）、LFU（最少访问次数）。
      FIFO，first in first out，这个是大家最熟的，先进先出。
      LFU， Less Frequently Used，就是上面例子中使用的策略，直白一点就是讲一直以来最少被使用的。如上面所讲，缓存的元素有一个hit属性，hit值最小的将会被清出缓存。
      LRU，Least Recently Used，最近最少使用的，缓存的元素有一个时间戳，当缓存容量满了，而又需要腾出地方来缓存新的元素的时候，那么现有缓存元素中时间戳离当前时间最远的元素将被清出缓存。
   -->
    <defaultCache
            eternal="false"
            maxElementsInMemory="10000"
            overflowToDisk="false"
            diskPersistent="false"
            timeToIdleSeconds="1800"
            timeToLiveSeconds="259200"
            memoryStoreEvictionPolicy="LRU"/>
  
    <cache
            name="cloud_user"
            eternal="false"
            maxElementsInMemory="5000"
            overflowToDisk="false"
            diskPersistent="false"
            timeToIdleSeconds="1800"
            timeToLiveSeconds="1800"
            memoryStoreEvictionPolicy="LRU"/>
  
</ehcache>

```

