# eMybatis-plus

## 1. 什么是 Mybatis-plus?

官网地址：https://baomidou.com/

1.1**MyBatis-Plus**（简称 MP）是一个 MyBatis 的增强工具，在 **MyBatis 的基础上只做增强不做改变**，**为简化开发**、**提高效率而生**。

Mybatis-plus 的愿景成为 Mybatis 的最好拍档，就跟魂斗罗里面的 P1、P2 一样

![image-20220501093546790](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220501093546790.png)

![image-20220501093833173](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220501093833173.png)

## 2.MyBatis-plus 的特性

- **无侵入**：只做增强不做改变，引入它不会对现有工程产生影响，如丝般顺滑
- **损耗小**：启动即会自动注入基本 CURD，性能基本无损耗，直接面向对象操作
- **强大的 CRUD 操作**：内置通用 Mapper、通用 Service，仅仅通过少量配置即可实现单表大部分 CRUD 操作，更有强大的条件构造器，满足各类使用需求
- **支持 Lambda 形式调用**：通过 Lambda 表达式，方便的编写各类查询条件，无需再担心字段写错
- **支持主键自动生成**：支持多达 4 种主键策略（内含分布式唯一 ID 生成器 - Sequence），可自由配置，完美解决主键问题
- **支持 ActiveRecord 模式**：支持 ActiveRecord 形式调用，实体类只需继承 Model 类即可进行强大的 CRUD 操作
- **支持自定义全局通用操作**：支持全局通用方法注入（ Write once, use anywhere ）
- **内置代码生成器**：采用代码或者 Maven 插件可快速生成 Mapper 、 Model 、 Service 、 Controller 层代码，支持模板引擎，更有超多自定义配置等您来使用
- **内置分页插件**：基于 MyBatis 物理分页，开发者无需关心具体操作，配置好插件之后，写分页等同于普通 List 查询
- **分页插件支持多种数据库**：支持 MySQL、MariaDB、Oracle、DB2、H2、HSQL、SQLite、Postgre、SQLServer 等多种数据库
- **内置性能分析插件**：可输出 SQL 语句以及其执行时间，建议开发测试时启用该功能，能快速揪出慢查询
- **内置全局拦截插件**：提供全表 delete 、 update 操作智能分析阻断，也可自定义拦截规则，预防误操作

### 支持数据库

> 任何能使用 `MyBatis` 进行 CRUD, 并且支持标准 SQL 的数据库，具体支持情况如下，如果不在下列表查看分页部分教程 PR 您的支持。

- MySQL，Oracle，DB2，H2，HSQL，SQLite，PostgreSQL，SQLServer，Phoenix，Gauss ，ClickHouse，Sybase，OceanBase，Firebird，Cubrid，Goldilocks，csiidb
- 达梦数据库，虚谷数据库，人大金仓数据库，南大通用（华库）数据库，南大通用数据库，神通数据库，瀚高数据库

### 框架结构

![framework](https://baomidou.com/img/mybatis-plus-framework.jpg)

## 3. 开发环境

开发工具：IDEA 2020.1、Navicat 15

Java 版本：jdk8

SpringBoot: 2.6.7

mybatis-plus: 3.5.1

MySQL：5.7

## 4. 入门

### 4.1 新建数据库

在 Navicat 15 中新建一个数据库

![image-20220501101834925](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220501101834925.png)

在 mp 数据库中新建一张为 user 的表

![image-20220501102259903](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220501102259903.png)

新建查询，复制以下 SQL 添加数据

```sql
insert into user(id,`name`,age,email)
values (1,'张三',18,'test1@qq.com'),
(2,'李四',19,'test2@qq.com'),
(3,'王五',20,'test3@qq.com'),
(4,'刘六',28,'test4@qq.com'),
(5,'武七',24,'test5@qq.com')
```

![image-20220501113005603](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220501113005603.png)

### 4.2 我们打开 IDEA 新建一个 SpringBoot 项目

![image-20220501113253792](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220501113253792.png)

导入 MyBatis-plus 依赖

```xml
        <!--mybatis-plus-->
        <dependency>
            <groupId>com.baomidou</groupId>
            <artifactId>mybatis-plus-boot-starter</artifactId>
            <version>3.5.1</version>
        </dependency>
```

配置 application.yml 文件

```yaml
spring:
  #MySQL数据源配置
  datasource:
    #数据源类型配置
    type: com.zaxxer.hikari.HikariDataSource
    driver-class-name: com.mysql.cj.jdbc.Driver
    url: jdbc:mysql://localhost:3306/mp?serverTimezone=UTC&useUnicode=true&characterEncoding=utf-8
    username: root
    password: 123456


mybatis-plus:
  #实体类别名配置
  type-aliases-package: com.xiaoliu.mybatisplus.pojo
  #日志配置
  configuration:
    log-impl: org.apache.ibatis.logging.stdout.StdOutImpl
```

新建四个包

![image-20220501143949655](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220501143949655.png)

在 pojo 包中新建一个 User 的类

```java
package com.xiaoliu.mybatisplus.pojo;

import lombok.Data;

import java.io.Serializable;

/**
 * 用户实体类
 * @author xiaoliu
 */
@Data
public class User implements Serializable {
    private Integer id;
    private String name;
    private Integer age;
    private String email;
}

```

再到 mapper 包中新建一个 UserMapper 的接口（注意：要继承 BaseMapper，并且填上泛型）

```java
package com.xiaoliu.mybatisplus.mapper;

import com.baomidou.mybatisplus.core.mapper.BaseMapper;
import com.xiaoliu.mybatisplus.pojo.User;

/**
 * 用户Mapper层接口
 * @author xiaoliu
 */
public interface UserMapper extends BaseMapper<User> {

}
```

随后我们在 SpringBoot 主启动类上添加 @MapperScan 注解

```java
package com.xiaoliu.mybatisplus;

import org.mybatis.spring.annotation.MapperScan;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

/**
 * @author xiaoliu
 */
@MapperScan("com.xiaoliu.mybatisplus.mapper")
@SpringBootApplication
public class MybatisPlusApplication {

    public static void main(String[] args) {
        SpringApplication.run(MybatisPlusApplication.class, args);
    }

}
```

### 4.3 测试

在 test 目录下的测试类中进行测试是否成功，注意这里使用 @Autowired 注解发生红线时，像我一样换成 @Resource 就不会报错了

```java
package com.xiaoliu.mybatisplus;

import com.xiaoliu.mybatisplus.mapper.UserMapper;
import com.xiaoliu.mybatisplus.pojo.User;
import org.junit.jupiter.api.Test;
import org.springframework.boot.test.context.SpringBootTest;

import javax.annotation.Resource;
import java.util.List;

@SpringBootTest
class MybatisPlusApplicationTests {

    @Resource
    private UserMapper userMapper;

    @Test
    void contextLoads() {
        //通过条件构造器查询一个list集合
        List<User> list = userMapper.selectList(null);
        list.forEach(System.out::println);
    }

}

```

![image-20220501164159191](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220501164159191.png)

## 5. 开启日志功能

在刚刚配置 Mybatis-plus 配置时，我们已经开启了日志功能了，现在我们来详细讲解一下这个功能

![image-20220503160253696](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220503160253696.png)

里面有多套 log 日志信息打印，它们都会打印出执行的 SQL 语句，查询到的结果信息，这里的配置默认推荐使用 StdOutImpl 这个日志功能

![image-20220503160447042](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220503160447042.png)

开启 Log 之后，会帮我们打印出对应的 SQL 语句，数据库中对应的行列信息，但是 Mybatis-plus 再我们刚刚写的这些代码中，并没有去写 SQL 语句，那他是怎么知道我们要操纵的是哪一张表中的信息呢？

其实在我们写 UserMapper 接口时就已经指定了使用哪一张表的 SQL 了

![image-20220503160847839](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220503160847839.png)

然后它会根据你指定的实体类中的成员变量查询对应的字段。

## 6.BaseMapper

BaseMapper 中封装了很多对单表的增删改查操作的方法，点进源码我们可以发现有各种各样的方法，什么 inset，delete。等等

![image-20220503161603868](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220503161603868.png)

这些执行的操作都是通过你在 Mapper 层 extens BaseMapper<T>泛型中指定的实体类进行对应表的操作，前提是你数据库中的表名要与实体类名一样对应。

刚刚我们已经对查询进行了一下简单的操作，现在我们再做一个简单的示范，这里只示范一下增加操作，其余的可以自己去试试

```java
    /**
     * 增加操作
     */
    @Test
    void add(){
        User user = new User();
        user.setId(6);
        user.setName("小刘");
        user.setAge(21);
        user.setEmail("1234567890@qq.com");
        int result = userMapper.insert(user);
        System.out.println("result:"+ result);
    }
```

![image-20220503163112214](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220503163112214.png)

**Mybatis-plus 解决了单表查询的问题，但是对于多表还是建议手写 SQL 语句进行查询**

自定义多表 SQL 的话，在 Mybatis 的时候要配置 xxxMapper.xml 的文件路径进行映射，在 Mybatis-plus 中默认配置了一个 Mapper 文件的路径，**这个路径是在 resources 路径下建立一个 mapper 文件**, 当然你如果想要自定义路径的话可以进行编写配置

![image-20220503193549465](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220503193549465.png)

## 7.Service

在 Mybatis-plus 中，在 service 层给我们进一步封装了很多较为复杂的业务逻辑层的功能方法。这些方法其实也是基于 BaseMapper 接口中的功能做进一步的增强操作

### 7.1 准备工作

创建一个 Service 接口

![image-20220503194817487](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220503194817487.png)

源码：

![image-20220503194926969](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220503194926969.png)

我们可以看见在这个接口中封装了更多的方法，对应不同的业务逻辑，比如增加和修改操作直接调用一个 saveOrUpdate 方法即可实现

**我们再创建一个 Service 接口的实现类**（注意：这里还是需要指定**@Service 把它加入组件中**的）

![image-20220503195242634](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220503195242634.png)

源码：

![image-20220503195657775](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220503195657775.png)

在这个类中，我们可以看见也有很多的方法可以进行调用，平时的话我们大部分都是调用 IService 接口中的方法就可以实现很多功能了！

### 7.2 使用

 在测试类中，我们进行一些方法的操作

查询数据总条数：count();

```java
package com.xiaoliu.mybatisplus;

import com.xiaoliu.mybatisplus.mapper.UserMapper;
import com.xiaoliu.mybatisplus.pojo.User;
import com.xiaoliu.mybatisplus.service.UserService;
import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;

import javax.annotation.Resource;
import java.util.List;

@SpringBootTest
class MybatisPlusApplicationTests {

    @Resource
    private UserService userService;

    /**
     * 查询数据总条数
     */
    @Test
    void count(){
        long result = userService.count();
        System.out.println("result:" + result);
    }

}

```

![image-20220503200643007](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220503200643007.png)

批量添加：saveBatch(); 这里做一个模拟的批量添加功能，具体功能实现看你自己的业务

```java
package com.xiaoliu.mybatisplus;

import com.xiaoliu.mybatisplus.mapper.UserMapper;
import com.xiaoliu.mybatisplus.pojo.User;
import com.xiaoliu.mybatisplus.service.UserService;
import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;

import javax.annotation.Resource;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

@SpringBootTest
class MybatisPlusApplicationTests {

    @Resource
    private UserService userService;

    /**
     * 批量添加
     */
    @Test
    void adds(){
        List<User> list = new ArrayList<>();
        for (int i = 0; i <= 10 ; i++) {
            User user = new User();
            user.setName("ybc"+i);
            user.setAge(20+i);
            list.add(user);
        }
        boolean batch = userService.saveBatch(list);
        System.out.println(batch);
    }

}

```

![image-20220503201306972](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220503201306972.png)

这里批量添加的时候 Id 主键是 Mybatis-plus 中利用雪花算法给我们生成的一个 Id，后面再告诉你如何利用主键的自动递增实现

总结：IService 中的方法使用就到这了，以上只是演示了两种方法，其他的方法各位可以好好自己去试试

## 8.Mybatis-plus 中的注解

### 1.@TableName

在真实业务中，会存在多个 xx_xxx 的表名，这时候如果直接使用泛型就会找不到对应的表了。所以我们在写实体类的时候，需要加上

@TableName 这个注解指定数据库中对应的表。这样即使是有下划线直接指定实体类也能找到对应的表了。

```java
/**
 * 用户实体类
 * @author xiaoliu
 */
@Data
@TableName("user")
public class User implements Serializable {
    private Integer id;
    private String name;
    private Integer age;
    private String email;
}
```

当然你也可以在 yaml 配置文件中去配置 Mybatis-plus 的全局配置，它会为每个实体类都加上一个前缀

```yaml
mybatis-plus:
  #实体类别名配置
  type-aliases-package: com.xiaoliu.mybatisplus.pojo
  #日志配置
  configuration:
    log-impl: org.apache.ibatis.logging.stdout.StdOutImpl
  #设置Mybatis-plus全局配置
  global-config:
    db-config:
      #设置实体类对应表的统一前缀
      table-prefix: t_
```

当然我不建议这么去使用，因为如果说你的表名不是你指定的前缀开头的，它会匹配不上，从而报错，最好还是选择注解进行使用

![image-20220504121442480](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220504121442480.png)

### 2.@TableId

该注解是表示将该属性所对应的字段指定为主键

```java
/**
 * 用户实体类
 * @author xiaoliu
 */
@Data
@TableName("user")
public class User implements Serializable {

    @TableId
    private Integer id;

    private String name;

    private Integer age;

    private String email;
```

使用 @TableId 里面的 value 属性，如果只是指定一个字段名，当然这个 value = " " 也可以不用写，直接在括号中写入" "即可

```java
/**
 * 用户实体类
 * @author xiaoliu
 */
@Data
@TableName("user")
public class User implements Serializable {
    //指定数据库中对应主键字段名
    @TableId(value = "id")
    private Integer id;

    private String name;

    private Integer age;

    private String email;
}
```

使用 @TableId 中的 Type 属性，上面设置了 value 属性，当然这样是不够的，如果你的主键是自动递增的，那么还是使用的雪花算法进行生成主键 ID，但是加上 Type =  IdType.xxx 后是自动递增的，当然这个**设置自动递增在你的数据库中也要进行对应设置**

```java
/**
 * 用户实体类
 * @author xiaoliu
 */
@Data
@TableName("user")
public class User implements Serializable {
    //设置成自动递增
    @TableId(value = "id",type = IdType.AUTO)
    private Integer id;

    private String name;

    private Integer age;

    private String email;
}
```

当然你也可以在 yaml 配置文件中进行一个设置，但是具体的话也是要根据你业务进行设置，因为这个配置的话是全局配置，如果你的数据库主键不是自增的，那么还是会出错的

```yaml
mybatis-plus:
  #实体类别名配置
  type-aliases-package: com.xiaoliu.mybatisplus.pojo
  #日志配置
  configuration:
    log-impl: org.apache.ibatis.logging.stdout.StdOutImpl
  #设置Mybatis-plus全局配置
  global-config:
    db-config:
      #设置全局实体类表名加上前缀
      table-prefix: t_
      #设置全局实体类主键Id自增
      id-type: auto
```

### 3. 雪花算法

![image-20220504131721770](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220504131721770.png)

### 4.@TableField

该注解设置属性所对应的字段名，如果说你实体类中的属性名与数据库中的字段名不一致，使用该注解进行一个指定即可

```java
/**
 * 用户实体类
 * @author xiaoliu
 */
@Data
@TableName("user")
public class User implements Serializable {

    @TableId(value = "id",type = IdType.AUTO)
    private Integer id;

    @TableField("name")
    private String name;

    @TableField("age")
    private Integer age;

    @TableField("email")
    private String email;
}
```

### 5.@TableLogic

在数据库中新增一个字段，is_delete 默认值设置为 0

![image-20220504133508303](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220504133508303.png)

在实体类中添加对应属性，假删除的属性上加上 @TableLogic 注解

```java
/**
 * 用户实体类
 * @author xiaoliu
 */
@Data
@TableName("user")
public class User implements Serializable {

    @TableId(value = "id",type = IdType.AUTO)
    private Integer id;

    @TableField("name")
    private String name;

    @TableField("age")
    private Integer age;

    @TableField("email")
    private String email;

    @TableLogic
    private Integer isDelete;
}
```

这时我们再执行删除的方法会发现，它的语句变成了 update 修改的 SQL 了，我们再看数据库 is_delete 这个字段变成了 1

![image-20220504134231337](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220504134231337.png)

![image-20220504134330083](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220504134330083.png)

以前我们删除都是直接物理删除，把对应条件的都进行了删除，它就不再存在了这条数据。而用了 @TableLogic 这个注解可以实现逻辑删除，只要再数据库中新增一个假删除的字段，再该字段对应的实体类属性上加上该注解，再使用删除方法就会进行逻辑删除，而该数据库依旧保存再该数据库中，0 表示未删除，1 表示已删除。

这时我们再进行查询所有数据时，就不会查询到已经进行逻辑删除的数据了。它会自动的在查询后面加上条件查询未逻辑删除的字段。

![image-20220504135419190](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220504135419190.png)

## 9. 条件构造器

#### 1.wapper 介绍

![image-20220504135940404](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220504135940404.png)

#### 2.QueryWrapper

我们使用 QueryWrapper<T> 进行一些条件查询

```java
    /**
     * 条件构造器
     */
    @Test
    void selectWrapper(){
        //查询name中包含'刘',age在20-30之间，邮箱信息不为Null的用户信息
        QueryWrapper<User> wrapper = new QueryWrapper<>();
        //column为数据库中的字段名而非实体类的属性名，后面是条件
        wrapper.like("name","刘")
                .between("age",20,30)
                .isNotNull("email");
        List<User> list = userService.list(wrapper);
```

![image-20220504142746953](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220504142746953.png)

我们会发现它的 SQL 语句会根据我们使用的条件构造器去进行相同条件的查询结果。

该类还有很多的方法可以进行尝试，这里只做部分演示啦，剩下的自己去探索哦！

#### 3.Condition

使用带有该参数的方法进行条件组装，它是个布尔类型的参数，如果为 true 则表示组装，如果为 false 则表示不组装该条件

```java
    /**
     * 条件构造器
     */
    @Test
    void selectWrapper(){
        String name = "刘";
        Integer ageBegin = null;
        Integer ageEnd = 30;
        QueryWrapper<User> wrapper = new QueryWrapper<>();
        wrapper.like(StringUtils.isNotBlank(name),"name",name)
                .ge(ageBegin != null,"age",ageBegin)
                .le(ageEnd != null,"age",ageEnd);
        List<User> list = userService.list(wrapper);
        list.forEach(System.out::println);
    }
```

![image-20220504165852087](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220504165852087.png)

由条件我们可以看出，如果为条件不成立，则不会执行该条件构造进行拼接操作。

#### 4.LambdaQueryWrapper

该表达式里面的指定数据库字段名的参数可以用实体类的 lambda 表达式进行表示

```java
    /**
     * 条件构造器
     */
    @Test
    void selectWrapper(){
        String name = "刘";
        Integer ageBegin = null;
        Integer ageEnd = 30;
        LambdaQueryWrapper<User> queryWrapper = new LambdaQueryWrapper<>();
        queryWrapper.like(StringUtils.isNotBlank(name),User::getName,name)
                .ge(ageBegin != null,User::getAge,ageBegin)
                .le(ageEnd != null,User::getAge,ageEnd);
        List<User> list = userService.list(queryWrapper);
        list.forEach(System.out::println);
    }
```

![image-20220504170911587](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220504170911587.png)

使用起来基本与上面没太大区别

## 10.Mybatis-plus 分页插件

使用 Mybatis-plus 分页插件之前我们要对 Mybatis-plus 进行配置

```java
package com.xiaoliu.mybatisplus.config;

import com.baomidou.mybatisplus.annotation.DbType;
import com.baomidou.mybatisplus.extension.plugins.MybatisPlusInterceptor;
import com.baomidou.mybatisplus.extension.plugins.inner.PaginationInnerInterceptor;
import org.mybatis.spring.annotation.MapperScan;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

/**
 * Mybatis-Plus配置类
 * @author xiaoliu
 */
@MapperScan("com.xiaoliu.mybatisplus.mapper")
@Configuration
public class MybatisPlusConfig {

    @Bean
    public MybatisPlusInterceptor mybatisPlusInterceptor(){
        MybatisPlusInterceptor mybatisPlusInterceptor = new MybatisPlusInterceptor();
        mybatisPlusInterceptor.addInnerInterceptor(new PaginationInnerInterceptor(DbType.MYSQL));
        return mybatisPlusInterceptor;
    }
}

```

随后使用分页插件功能

```java
    @Test
    void Page(){
        //分页插件
        Page<User> page = new Page<>(1,3);
        userService.page(page,null);
        System.out.println(page);
    }
```

结果

![image-20220505100654410](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220505100654410.png)

使用分页插件，如果查询的是第一页的参数，那么它的语句如上图结果所示，LIMIT ？ 只有一个参数

#### 10.1 获取分页数据的方法

常用的一些方法：

```java
    @Test
    void Page(){
        //分页插件
        Page<User> page = new Page<>(1,3);
        userService.page(page,null);
        // 获取当前分页数据
        System.out.println(page.getRecords());
        // 获取总条数
        System.out.println(page.getTotal());
        // 获取每页的数据条数
        System.out.println(page.getSize());
        // 当前在第几页
        System.out.println(page.getCurrent());
        // 获取总页数
        System.out.println(page.getPages());
    }
```

![image-20220505102319203](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220505102319203.png)

## 11. 乐观锁和悲观锁

简述一下乐观锁和悲观锁，个人理解，详情还请自行百度

**悲观锁**：在执行语句时，我们就认为这个语句它就是会失败，它就是会报错，我们就提前给它加上锁机制，让它出现错误就回滚。这种悲观的加锁机制就被叫做悲观锁，通常使用 for update 来进行实现。

**乐观锁**：与悲观锁相反，通常使用加 version 字段的方法进行实现。

#### 11.1 模拟冲突

新建一张表为 product

![image-20220505111102878](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220505111102878.png)

在表中添加一条商品数据

![image-20220505111143288](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220505111143288.png)

新建实体类 Product

```java
/**
 * 商品表实体类
 * @author xiaoliu
 */
@Data
@TableName("product")
public class Product implements Serializable {

    @TableId(value = "id",type = IdType.AUTO)
    private Integer id;

    @TableField("name")
    private String name;

    @TableField("price")
    private Integer price;


    @TableField("version")
    private Integer version;
}
```

在 idea 中编辑代码模拟冲突

```java
    @Test
    void testProduct01(){
        // 小李查询商品价格
        Product productLi = productService.getById(1);
        System.out.println("小李查询的商品价格：" + productLi.getPrice());

        // 小王查询商品价格
        Product productWang = productService.getById(1);
        System.out.println("小王查询的商品价格：" + productWang.getPrice());

        // 小李将商品价格+50
        productLi.setPrice(productLi.getPrice()+50);
        productService.updateById(productLi);

        // 小王将商品价格-30
        productWang.setPrice(productWang.getPrice()-30);
        productService.updateById(productWang);

        // 老板查询商品价格
        Product productBoss = productService.getById(1);
        System.out.println("老板查询的商品价格：" + productBoss.getPrice());

    }
```

小李查询出来的价格

![image-20220505111344299](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220505111344299.png)

小王查询出来的价格

![image-20220505111420633](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220505111420633.png)

结果：我们可以发现，小李和小王都是对原有价格进行了操作，但是最终结果确为小王操作的 70，这是因为两边同时拿到的都是 100，而小王是最后执行的覆盖掉了小李的数据，才会导致最终老板拿到的价格应该为 150-30 =120，但是老板拿到的是小王最终修改的 70 元价格，这就发生了冲突了。

![image-20220505111634935](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220505111634935.png)

#### 11.2Mybatis-plus 乐观锁插件

为了解决刚刚这个冲突，我们使用 Mybatis-plus 提供的乐观锁插件进行加锁处理

**在实体类上进行修改**：在版本号字段上加上 @Version 注解

```java
/**
 * 商品表实体类
 * @author xiaoliu
 */
@Data
@TableName("product")
public class Product implements Serializable {

    @TableId(value = "id",type = IdType.AUTO)
    private Integer id;

    @TableField("name")
    private String name;

    @TableField("price")
    private Integer price;

    /**
     * 该注解标识乐观锁版本号字段
     */
    @Version
    private Integer version;
}
```

在 config 配置类中加入乐观锁插件

```java
/**
 * Mybatis-Plus配置类
 * @author xiaoliu
 */
@MapperScan("com.xiaoliu.mybatisplus.mapper")
@Configuration
public class MybatisPlusConfig {

    @Bean
    public MybatisPlusInterceptor mybatisPlusInterceptor(){
        MybatisPlusInterceptor mybatisPlusInterceptor = new MybatisPlusInterceptor();
        // 新增分页插件
        mybatisPlusInterceptor.addInnerInterceptor(new PaginationInnerInterceptor(DbType.MYSQL));
        // 新增乐观锁插件
        mybatisPlusInterceptor.addInnerInterceptor(new OptimisticLockerInnerInterceptor());
        return mybatisPlusInterceptor;
    }
}
```

接下来我们再去执行刚刚的代码：为什么是 150？

因为小李先进行了修改，以版本号 0 为条件进行修改，这时修改成功，版本号也变成了。在后来小王进行修改时，他也是以版本号为 0 进行修改，但这时小李已经修改了版本号把它变成 1 了，所以这时小王的条件失效了，修改失败了。老板查询结果为 150

![image-20220505123947930](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220505123947930.png)

![image-20220505124243231](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220505124243231.png)

但是这也不正确，按照常理来说，这时应该为 120 才正确吧。所以我们进行一步小小的优化

```java
@Test
    void testProduct01(){
        // 小李查询商品价格
        Product productLi = productService.getById(1);
        System.out.println("小李查询的商品价格：" + productLi.getPrice());

        // 小王查询商品价格
        Product productWang = productService.getById(1);
        System.out.println("小王查询的商品价格：" + productWang.getPrice());

        // 小李将商品价格+50
        productLi.setPrice(productLi.getPrice()+50);
        productService.updateById(productLi);

        // 小王将商品价格-30
        productWang.setPrice(productWang.getPrice()-30);
        boolean result = productService.updateById(productWang);
        if (result == false){
            // 操作失败重试
           Product productNew = productService.getById(1);
           productNew.setPrice(productNew.getPrice() - 30);
           productService.updateById(productNew);
        }

        // 老板查询商品价格
        Product productBoss = productService.getById(1);
        System.out.println("老板查询的商品价格：" + productBoss.getPrice());

    }

```

结果：

![image-20220505125817874](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220505125817874.png)

## 12. 通用枚举

在数据库中添加一个 sex 字段

![image-20220505131513684](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220505131513684.png)

我们声明一个枚举类：SexEnum

```java

/**
 * 性别枚举类
 * @author xiaoliu
 */
@Getter
public enum SexEnum {
    MALE(1,"男"),
    FEMALE(2,"女");

    //将注解所标识的属性的值存储到数据库中
    @EnumValue
    private Integer sex;
    private String sexName;

    SexEnum(Integer sex, String sexName) {
        this.sex = sex;
        this.sexName = sexName;
    }
}
```

接下来我们在 yaml 的 Mybatis-plus 配置扫描通用枚举的包

```yaml
mybatis-plus:
  #实体类别名配置
  type-aliases-package: com.xiaoliu.mybatisplus.pojo

  #日志配置
  configuration:
    log-impl: org.apache.ibatis.logging.stdout.StdOutImpl

  #扫描通用枚举的包
  type-enums-package: com.xiaoliu.mybatisplus.enums
```

编写测试代码：

```java
    @Test
    void TestEnum(){
        User user = new User();
        user.setName("admin");
        user.setAge(33);
        user.setSex(SexEnum.MALE);
        boolean save = userService.save(user);
        System.out.println("save = " + save);
    }
```

![image-20220505131926888](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220505131926888.png)

![image-20220505132000905](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220505132000905.png)

## 13. 代码生成器

#### 13.1 导入依赖

```xml
    <!--代码生成器-->
        <dependency>
            <groupId>com.baomidou</groupId>
            <artifactId>mybatis-plus-generator</artifactId>
            <version>3.5.2</version>
        </dependency>
        <dependency>
            <groupId>org.freemarker</groupId>
            <artifactId>freemarker</artifactId>
            <version>2.3.31</version>
        </dependency>
```

#### 13.2 代码

这里选择最新版

![image-20220505132509039](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220505132509039.png)

```java
package com.xiaoliu.mybatisplus.generator;

import com.baomidou.mybatisplus.generator.FastAutoGenerator;
import com.baomidou.mybatisplus.generator.config.OutputFile;
import com.baomidou.mybatisplus.generator.engine.FreemarkerTemplateEngine;

import java.util.Collections;

/**
 * 代码生成器
 * @author xiaoliu
 */
public class Generator {
    public static void main(String[] args) {
        //要操作的数据库
        FastAutoGenerator.create("jdbc:mysql://localhost:3306/mp?serverTimezone=UTC&useUnicode=true&characterEncoding=utf-8",
                "root","123456")
                .globalConfig(builder -> {
                    builder.author("xiaoliu") // 设置作者
                            .enableSwagger() // 开启 swagger 模式
                            .fileOverride() // 覆盖已生成文件
                            .outputDir("D:\\dbsk\\mybatis-plus\\src\\main\\java"); // 指定输出目录
                })
                .packageConfig(builder -> {
                    builder.parent("com.xiaoliu.mybatisplus") // 设置父包名
                            .moduleName(null) // 设置父包模块名
                            .pathInfo(Collections.singletonMap(OutputFile.xml, "D:\\dbsk\\mybatis-plus\\src\\main\\resources\\mapper")); // 设置mapperXml生成路径
                })
                .strategyConfig(builder -> {
                    builder.entityBuilder().enableLombok();//添加Lombok
                    builder.controllerBuilder().enableHyphenStyle(). //开启驼峰转连注解
                            enableRestStyle();//开启@RestController注解
                    builder.addInclude("") // 设置需要生成的表名
                            .addTablePrefix("t_", "c_"); // 设置过滤表前缀
                })
                // 使用Freemarker引擎模板，默认的是Velocity引擎模板
                .templateEngine(new FreemarkerTemplateEngine())
                .execute();
    }
}

```

#### 13.3 执行代码生成器

新建一个 Teacher 表

![image-20220505134728648](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220505134728648.png)

执行代码生成器的 main 方法，会先弹出文件夹，然后看输出台打印结果

![image-20220505135024392](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220505135024392.png)

![image-20220505134924237](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220505134924237.png)

检查一下生成的类和接口，我这里没有用 Swagger 所以爆错了。

![image-20220505135136314](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220505135136314.png)

![image-20220505135233882](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220505135233882.png)

![image-20220505135252884](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220505135252884.png)

![image-20220505135307945](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220505135307945.png)

![image-20220505135325708](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220505135325708.png)

如果你自己想 div 一个代码生成的模板， 你可以如下图去进行修改，把源码中的模板复制到你的 resource-->templates 下进行修改里面的内容即可，修改完成后每次执行就是你自己 div 的模板啦

![image-20220505140048531](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220505140048531.png)

## 14. 多数据源

新建一个数据库：mp-2, 把 product 复制粘贴过去

![image-20220505145953477](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220505145953477.png)

再新建一个 SpringBoot 项目

#### 14.1 导入依赖

```xml
<dependency>
  <groupId>com.baomidou</groupId>
  <artifactId>dynamic-datasource-spring-boot-starter</artifactId>
  <version>3.5.1</version>
</dependency>
```

#### 14.2Yml 配置数据源

```yaml
spring:
  datasource:
    dynamic:
      primary: master #设置默认的数据源或者数据源组,默认值即为master
      strict: false #严格匹配数据源,默认false. true未匹配到指定数据源时抛异常,false使用默认数据源
      datasource:
        master:
          url: jdbc:mysql://xx.xx.xx.xx:3306/dynamic
          username: root
          password: 123456
          driver-class-name: com.mysql.jdbc.Driver # 3.2.0开始支持SPI可省略此配置
        slave_1:
          url: jdbc:mysql://xx.xx.xx.xx:3307/dynamic
          username: root
          password: 123456
          driver-class-name: com.mysql.jdbc.Driver
        slave_2:
          url: ENC(xxxxx) # 内置加密,使用请查看详细文档
          username: ENC(xxxxx)
          password: ENC(xxxxx)
          driver-class-name: com.mysql.jdbc.Driver
       #......省略
       #以上会配置一个默认库master，一个组slave下有两个子库slave_1,slave_2
```

```yaml
# 多主多从                      纯粹多库（记得设置primary）                   混合配置
spring:                               spring:                               spring:
  datasource:                           datasource:                           datasource:
    dynamic:                              dynamic:                              dynamic:
      datasource:                           datasource:                           datasource:
        master_1:                             mysql:                                master:
        master_2:                             oracle:                               slave_1:
        slave_1:                              sqlserver:                            slave_2:
        slave_2:                              postgresql:                           oracle_1:
        slave_3:                              h2:                                   oracle_2:
```

#### 14.3 使用代码生成器生成 User 和 Product 实体类

![image-20220505145054611](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220505145054611.png)

别忘了在启动类加上 @MapperScan() 注解开启扫描

#### 14.4 使用数据源

在 ServiceImpl 类上加上 @DS() 注解，指定数据源

```java
@DS("master")
@Service
public class UserServiceImpl extends ServiceImpl<UserMapper, User> implements IService<User> {
}
```

```java
@DS("slave_1")
@Service
public class ProductServiceImpl extends ServiceImpl<ProductMapper, Product> implements IProductService {

}
```

#### 14.5 测试多数据源

```java
package com.xiaoliu.mybatisplus;

import com.xiaoliu.mybatisplus.service.IProductService;
import com.xiaoliu.mybatisplus.service.IUserService;
import org.junit.jupiter.api.Test;
import org.springframework.boot.test.context.SpringBootTest;

import javax.annotation.Resource;

@SpringBootTest
class MybatisPlusDatasourceApplicationTests {
    @Resource
    private IUserService userService;

    @Resource
    private IProductService productService;


    @Test
    void contextLoads() {
        System.out.println(userService.getById(2));
        System.out.println(productService.getById(1));

    }

}

```

![image-20220505151024605](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220505151024605.png)

结果表示我们可以从配置多数据源中获取数据

## 15.MybatisX 插件

MybatisX 是一款基于 IDEA 的快速开发插件，为效率而生。

安装方法：打开 IDEA，进入 File -> Settings -> Plugins -> Browse Repositories，输入 `mybatisx` 搜索并安装。

官网地址：https://baomidou.com/pages/ba5b24/
