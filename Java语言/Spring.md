#  Spring

### 1-1.Spring 简介

**Spring**：春天------>给软件行业带来了春天！

2002，首次推出了Spring框架的雏形：interface21框架！

Spring框架即以interface21框架为基础，经过重新设计，并不断丰富其内涵，于2004年3月24日发布了1.0正式版。

**Rod Johnson**，Spring Framework创始人，著名作者。很难想象Rod Johnson的学历，真的让好多人大吃一惊，他是悉尼大学的博士，然而他的专业不是**计算机**，而是**音乐学**。

Spring理念：使**现有的技术更加容易使用，本身是一个大杂烩，整合了现有的技术框架！**





### 1-2.Spring 的优点

1. Spring是一个开源的免费的框架（容器）！
2. Spring是一个轻量级的、非入侵式的框架！
3. 控制反转（IOC），面向切面编程（AOP）！
4. 支持事务的处理，对框架整合的支持！

总结一句话：**Spring就是一个轻量级的控制反转（IOC）和面向切面编程（AOP）的框架！**





### 1-3.Spring 组成

![在这里插入图片描述](https://img-blog.csdnimg.cn/89876ddb69bc46e9bca333c8a901ac97.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)





### 1-4.Spring 拓展

**现代化的Java开发！说白就是基于Spring的开发！**

**Spring Boot**

1. 一个快速开发的脚手架。
2. 基于SpringBoot可以快速的开发单个微服务。
3. 约定大于配置。

**Spring Cloud**

1. SpringCloud是基于SpringBoot实现的。
2. 因为现在大多数公司都在使用SpringBoot进行快速开发，学习SpringBoot的前提，需要完全掌握Spring及SpringMVC！承上启下的作用！

弊端：**发展了太久之后，违背了原来的理念！配置十分繁琐，人称：“配置地狱！”**



## 2、IOC理论推导

### 2-1.UserDao 接口

```java
public interface UserDao {

    void getUser();

}

```



### 2-2.UserDaoImpl 实现类

```java
public class UserDaoImpl implements UserDao {

    public void getUser() {
        System.out.println("获取用户数据");
    }
}

```



### 2-3.UserService 业务接口

```java
public interface UserService {

    void getUser();
}

```



### 2-4.UserServiceImpl 业务实现类

```java
public class UserServiceImpl implements UserService {

    UserDao userDao = new UserDaoImpl();

    public void getUser() {
      userDao.getUser();
    }
}

```



### 2-5.测试

```java
public class Test {
    public static void main(String[] args) {

        UserService userService = new UserServiceImpl();
        userService.getUser();

    }
}

```



在我们之前的业务中，用户的需求可能会影响我们原来的代码，我们需要**根据用户的需求去修改原代码**！如果程序代码量十分大，修改一次的成本代价十分昂贵！



![在这里插入图片描述](https://img-blog.csdnimg.cn/eb88bdd01b09449e8e65bacdbb16082a.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)



我们使用一个**Set接口实现**，已经发生了革命性的变化！

```java
UserDao userDao;

public void setUserDao(UserDao userDao){
    this.userDao = userDao;
}

```



之前，程序是**主动创建**对象！**控制权在程序员**手上！

  使用了set注入后，程序**不再具有主动性**，而是变成了**被动**的接受对象！

控制**反转了**，主动权交给用户了

![在这里插入图片描述](https://img-blog.csdnimg.cn/4421b1369e73469d8bfb36403cb31dfa.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)

这种思想，从本质上解决了问题，我们程序猿不用再去管理对象的创建了。系统的耦合性大大降低~，可以更加专注的在业务的实现上！这是IOC的原型！



## 3、IOC本质

![在这里插入图片描述](https://img-blog.csdnimg.cn/da7c8c911ac143e3839248ab1104a313.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)

![在这里插入图片描述](https://img-blog.csdnimg.cn/856e6d2a5c7b4f76a8f41ab1d40a8384.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)



控制反转IoC（Inversion of Control），是一种**设计思想**，DI（依赖注入）是**实现IoC的一种方法**，也有人认为DI只是IoC的另一种说法。没有IoC的程序中，我们使用面向对象编程，对象的创建与对象间的依赖关系完全硬编码在程序中，对象的创建由程序自己控制，控制反转后**将对象的创建转移给第三方**，个人认为所谓控制反转就是：**获得依赖对象的方式反转了。**

  采用XML方式配置Bean的时候，Bean的**定义**信息是和**实现分离**的，而采用注解的方式可以把两者合为一体，Bean的定义信息直接以注解的形式定义在实现类中，从而达到了零配置的目的。

  控制反转是一种通过描述（XML或注解）并**通过第三方去生产或获取特定对象**的方式。在Spring中实现控制反转的是**IoC容器**，其实现方法是**依赖注入**（Dependency Injection，DI）。




## 4、Spring 入门程序

### 4-1.实体类

```java
public class User {
    private String name;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    @Override
    public String toString() {
        return "User{" +
                "name='" + name + '\'' +
                '}';
    }
}

```



### 4-2.配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">

    <!--使用Spring 来创建对象，在Spring 中，这些都称为bean
    类型  变量名 = new 类型();
    User user = new User();

        bean = 对象 new User();
    id = 变量名
    class = new 的对象;
    property 相当于 给对象中的属性设置一个值！
    value 具体的值，基本数据类型
    ref 引用Spring中创建好的对象

    -->
    <bean id="user" class="cn.bloghut.domain.User">
            <property name="name" value="csdn_闲言"/>
    </bean>

</beans>

```



### 4-3.测试

```java
public static void main(String[] args) {
    //获取Spring 的上下文对象
    ApplicationContext ac = new ClassPathXmlApplicationContext("beans.xml");
    //我们的对象现在都在Spring 中管理了，我们要使用，直接去里面取出来就行了
    User user = (User)ac.getBean("user");
    //打印
    System.out.println(user.toString());
}

```



### 4-4.结果

```java
User{name='csdn_闲言'}

```





### 4-5.思考问题？

**Hello对象是谁创建的？**

Hello对象是由Spring创建的。



**Hello对象的属性是怎么设置的？**
  Hello对象的属性是由Spring容器设置的。



这个过程就叫**控制反转**：

  控制：谁来控制对象的创建，传统应用程序的对象是由程序本身控制创建的，使用Spring后，对象是由Spring来创建的。

  反转：程序本身不创建对象，而变成被动的接收对象。



**依赖注入**：就是利用**set方法来进行注入的**。

**IOC**是一种**编程思想**，由**主动的编程变成被动的接收。**

可以通过new ClassPathXmlApplicationContext去浏览一下底层源码。

到了现在，不用在程序中去改动了，要实现不同的操作，只需要在xml配置文件中进行修改，所谓的IOC，一句话搞定：**对象由Spring来创建，管理，装配！**
![在这里插入图片描述](https://img-blog.csdnimg.cn/df4eaa2a5afd4c95b036cce627649665.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)



## 5、IOC创建对象的方式

### 5-1.使用无参构造创建对象，默认！

```xml
public User() {
    System.out.println("User 空参构造方法执行了");
}

<!--注入user-->
<bean id="user" class="cn.bloghut.pojo.User">
    <property name="name" value="csdn_闲言"/>
</bean>

```



### 5-2.使用有参构造创建对象

**下标赋值**

```xml
public User(String name) {
    this.name = name;
}

<bean id="user" class="cn.bloghut.pojo.User">
    <constructor-arg index="0" value="csdn_闲言"/>
</bean>

```



### 5-3.类型

```xml
public User(String name) {
    this.name = name;
}
<!--通过类型-->
<bean id="user" class="cn.bloghut.pojo.User">
    <constructor-arg type="java.lang.String" value="csdn_闲言"/>
</bean>

参数名
<!--参数名-->
<bean id="user" class="cn.bloghut.pojo.User">
    <constructor-arg name="name" value="csnd_闲言"/>
</bean>

```



![在这里插入图片描述](https://img-blog.csdnimg.cn/5f7fde68cb144d84a743c1f8fb92f0bf.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)

**总结：在配置文件加载的时候，容器中管理的对象就已经初始化了！**

Spring 容器，就类似于婚介网站。

- 信息都注册在里面
- 你想查看（获取）的时候再拿



## 6、Spring配置

### 6-1.别名

```xml
<bean id="user" class="cn.bloghut.pojo.User">
    <constructor-arg name="name" value="csnd_闲言"/>
</bean>
<alias name="user" alias="user2"/>

ApplicationContext ac = new ClassPathXmlApplicationContext("bean.xml");
User user = (User)ac.getBean("user2");
user.show();

输出：csnd_闲言

```



### 6-2.Bean的配置

```xml
别名可以通过很多种方式分割

空格分割
逗号分割
分号分割
<bean id="user" class="cn.bloghut.pojo.User" name="user2 u2,u3;u4">
    <property name="name" value="csdn_闲言"/>
</bean>

//        User user = (User)ac.getBean("user");
//        User user = (User)ac.getBean("user2");
//        User user = (User)ac.getBean("u2");
//        User user = (User)ac.getBean("u3");
         User user = (User)ac.getBean("u4");
        user.show();

输出：csdn_闲言

```



### 6-3.import

这个import。一般**用于团队开发使用**，它可以将多个配置文件，导入合并为一个。

  假设，现在项目中有多个人开发，这三个人负责不同的类开发，不同的类需要注册在不同的bean中，我们可以利用import将所有人的beans.xml合并为一个总的！

1. 张三
2. 李四
3. 王五

![在这里插入图片描述](https://img-blog.csdnimg.cn/604e9ff7ee654defb93e62be4ed1b537.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)



**使用的时候，直接使用总的配置就可以了。**



## 7、依赖注入

### 7-1.构造器注入

前面已经说过

### 7-2.Set 注入

依赖注入：set注入

- 依赖：bean对象的创建依赖于容器！

- 注入：bean对象中的所有属性，由容器来注入！

**1.复杂类型：Address类**

```java
public class Address {
    private String address;
        省略setter
}

```



**2.真实测试对象：student类**

```java
public class Student {

    private String name;
    private Address address;
    private String[] books;
    private List<String> hobbies;
    private Map<String,String> card;
    private Set<String> games;
    private String wife;
    private Properties info;
    省略setter
}

```



**bean.xml**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">


    <bean id="address" class="cn.bloghut.domain.Address">
        <property name="address" value="csdn_闲言"/>
    </bean>

    <bean id="student" class="cn.bloghut.domain.Student">
        <!--注入address 类型-->
        <property name="address" ref="address"/>
        <!--String 类型-->
        <property name="name" value="csdn_闲言"/>
        <!--String 类型-->
        <property name="books">
            <array>
                <value>JavaSE</value>
                <value>JavaWeb</value>
                <value>Spring</value>
                <value>SpringMVC</value>
                <value>Mybatis</value>
            </array>
        </property>
        <!--List-->
        <property name="hobbies">
            <list>
                <value>唱</value>
                <value>跳</value>
                <value>rap</value>
                <value>篮球</value>
            </list>
        </property>
        <!--Map-->
        <property name="card">
            <map>
                <entry key="闲言" value="csdn——闲言"></entry>
                <entry key="闲言博客" value="csdn——闲言——博客"></entry>
            </map>
        </property>
        <!--set-->
        <property name="games">
            <set>
                <value>唱</value>
                <value>跳</value>
                <value>rap</value>
                <value>篮球</value>
            </set>
        </property>
        <!--String-->
        <property name="wife" value="xxx"></property>
        <!--Properties-->
        <property name="info">
            <props>
                <prop key="p1">v1</prop>
                <prop key="p2">v2</prop>
                <prop key="p3">v3</prop>
            </props>
        </property>
    </bean>

</beans>

```



**测试**

```java
public static void main(String[] args) {
    ApplicationContext ac = new ClassPathXmlApplicationContext("bean.xml");
    Student student = (Student)ac.getBean("student");
    System.out.println(student);
}

```



**输出**

```java
Student{
name='csdn_闲言', 
address=Address{address='csdn_闲言'}, 
books=[JavaSE, JavaWeb, Spring, SpringMVC, Mybatis], 
hobbies=[唱, 跳, rap, 篮球], 
card={闲言=csdn——闲言, 闲言博客=csdn——闲言——博客}, 
games=[唱, 跳, rap, 篮球], 
wife='xxx', 
info={p3=v3, p2=v2, p1=v1}
}

```



### 8、拓展方式注入 可以使用**p命名空间**和**c命名空间**进行注入

注意点：p命名和c命名不能直接导入，需要导入约束

```xml
  xmlns:p="http://www.springframework.org/schema/p"
  xmlns:c="http://www.springframework.org/schema/c"
```



1. p 命名空间对应 setter 方式注入（要提供set方法）
2. c 命令空间对应 构造方法 （要提供有参构造方法）

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:p="http://www.springframework.org/schema/p"
       xmlns:c="http://www.springframework.org/schema/c"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">


</beans>

```



**bean.xml**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:p="http://www.springframework.org/schema/p"
       xmlns:c="http://www.springframework.org/schema/c"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">


    <bean id="user" class="cn.bloghut.domain.User" p:name="闲言" p:age="18"/>
    <bean id="user2" class="cn.bloghut.domain.User" c:name="csdn——闲言" c:age="19" />

</beans>

```



**pojo**

```java
public class User {
    private String name;
    private int age;

    public User() {
    }

    public User(String name, int age) {
        this.name = name;
        this.age = age;
    }
    省略setter
}

```



**测试**

```java
ApplicationContext ac = new ClassPathXmlApplicationContext("userbeans.xml");
User user = (User)ac.getBean("user");
User user2 = (User)ac.getBean("user2");
System.out.println(user);
System.out.println(user2);

```



**输出**

```json
User{name='闲言', age=18}
User{name='csdn——闲言', age=19}

```



## 9、bean的作用域

![在这里插入图片描述](https://img-blog.csdnimg.cn/ed536fc239c7435686e64fc72c7444ae.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)

![在这里插入图片描述](https://img-blog.csdnimg.cn/54e50c8f886e485bbef230817ab3919e.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)

### 9-1.单例模式（Spring 默认机制）

```xml
scope="singleton"
<bean  scope="singleton" id="user2" class="cn.bloghut.domain.User" c:name="csdn——闲言" c:age="19" />

User user2 = (User)ac.getBean("user2");
User user3 = (User)ac.getBean("user2");
System.out.println(user2.hashCode());
System.out.println(user3.hashCode());

```

输出

```json
817406040
817406040

```



### 9-2.原型模式：每次从容器中get的时候，都会产生一个新对象

```xml
<bean scope="prototype" id="user" class="cn.bloghut.domain.User" p:name="闲言" p:age="18"/>

ApplicationContext ac = new ClassPathXmlApplicationContext("userbeans.xml");
    for (int i = 0;i< 5;i++){
       System.out.println(ac.getBean("user").hashCode());
}

```

输出

```json
817406040
1955915048
1270855946
2083117811
157683534

```

**单线程**—单例
**多线程**—多例



## 10.Bean的自动装配

自动装配是Spring 满足bean依赖的一种方式！
Spring 会在上下文自动寻找，并自动给bean 装配属性！

在Spring 中有三种装配的方式

1. 在**xml 中显示**的配置
2. 在**java中显示**配置
3. **隐式** 的自动装配bean【重要】



**ByName方法自动装配**

1. autowire=“byName”
2. 会自动在容器上下文中查找，和自己对象set方法后面的值对应的bean id！
3. 弊端：set 方法后面的值和 id 相同

bean.xml

```xml
<bean id="cat" class="cn.bloghut.domin.Cat"/>
<bean id="dog" class="cn.bloghut.domin.Dog"/>

<!--
    byName：会自动在容器上下文中查找，和自己对象set方法后面的值对应的bean id！

-->
<bean id="people" class="cn.bloghut.domin.People" autowire="byName">
    <property name="name" value="csdn_闲言"/>
</bean>

```

测试

```java
public static void main(String[] args) {

    ApplicationContext ac = new ClassPathXmlApplicationContext("bean.xml");
    People people = ac.getBean("people", People.class);

    people.getCat().shout();
    people.getDog().shout();

}

```



**ByType方法自动装配**

1. autowire=“byType”
2. 会自动在容器上下文中查找，和自己对象属性类型相同的bean
3. 弊端：它必须保证类型全局唯一（在IOC容器中只能由一个）。

```xml
<bean id="cat" class="cn.bloghut.domin.Cat"/>
<bean id="dog11" class="cn.bloghut.domin.Dog"/>
   <!--
    byType：会自动在容器上下文中查找，和自己对象属性类型相同的bean

-->
  <bean id="people" class="cn.bloghut.domin.People" autowire="byType">
      <property name="name" value="csdn_闲言"/>
  </bean>

```



测试

```java
public static void main(String[] args) {

    ApplicationContext ac = new ClassPathXmlApplicationContext("bean.xml");
    People people = ac.getBean("people", People.class);

    people.getCat().shout();
    people.getDog().shout();

}

```



总结：

  **byName**的时候，需要保证所有bean的id唯一，并且这个bean需要和自动注入的属性的set方法的值一致
  **byType**的时候，需要保证所有bean的class唯一，并且这个bean需要和自动注入的属性的类型一致



## 11、注解实现自动装配

1. jdk1.5支持的注解 Spring2.5支持的注解

2. The introduction of annotation-based configuration raised the question of whether this approach is “better” than XML

3. @**Autowired**

4. @**Quelifier**

5. @**Resource**

```xml
xml头文件约束
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xmlns:context="http://www.springframework.org/schema/context"
      xmlns:aop="http://www.springframework.org/schema/aop"
      xsi:schemaLocation="http://www.springframework.org/schema/beans
       https://www.springframework.org/schema/beans/spring-beans.xsd
       http://www.springframework.org/schema/context
       https://www.springframework.org/schema/context/spring-context.xsd
       http://www.springframework.org/schema/aop
       https://www.springframework.org/schema/aop/spring-aop.xsd">

   <!--开启注解支持-->
   <context:annotation-config/>
</beans>

```



### 11-1.@Autowired

1. 在属性上使用
2. 在set方式上使用
3. 使用Autowired 可以不用编写set方法了，前提是你这个自动装配的属性在IOC（Spring）容器中存在（需要通过其他方式注入进容器），且符合名字byName。

```java
public class People {
    @Autowired
    private Dog dog;
    
    @Autowired
    private Cat cat;
    private String name;

    public People() {
    }

    public People(Dog dog, Cat cat, String name) {
        this.dog = dog;
        this.cat = cat;
        this.name = name;
    }
    省略setter
}

```



Autowired 有一个个唯一的属性（ required ）

```java
@Target({ElementType.CONSTRUCTOR, ElementType.METHOD, ElementType.PARAMETER, ElementType.FIELD, ElementType.ANNOTATION_TYPE})
@Retention(RetentionPolicy.RUNTIME)
@Documented
public @interface Autowired {
    boolean required() default true;
}

```



**@Nullable**
  字段标记了这个注解，表示这个字段可以为null



**@Qualifier**

- 当我们的容器存在多个相同类型，不同名称的bean。使用@Autowired 无法完成自动装配了
- 这个时候需要使用@Qualifier 和@Autowired 注解一起使用。
- 使用@Qualifier 指定一个唯一的bean对象注入！
  例如

IOC容器中存在多个 相同类型不同id的bean

![在这里插入图片描述](https://img-blog.csdnimg.cn/516f2372c06745bc85583668e865d7e5.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)



通过@Qualifier 指定一个唯一的bean



![在这里插入图片描述](https://img-blog.csdnimg.cn/5248f5c7494d4bd2863c24c4d1c6ba0b.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)



测试

![在这里插入图片描述](https://img-blog.csdnimg.cn/f43f473b2b76416bb78cae5267063f48.png#pic_center)

![在这里插入图片描述](https://img-blog.csdnimg.cn/6e816aa7646e469dbe11a3109f1e6146.png#pic_center)



### 11-2.@Resource

  不指定name值，先去判断**byName**和**byType**，有一个能注入即成功

**根据类型查找**

![在这里插入图片描述](https://img-blog.csdnimg.cn/fbd6d82c605c44e2a9674ca6840d6f0c.png#pic_center)

![在这里插入图片描述](https://img-blog.csdnimg.cn/e34baae504864891b4c97b15d03a37c5.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)

![在这里插入图片描述](https://img-blog.csdnimg.cn/56d6be98885244f1b63fac1e4647ab93.png#pic_center)



### 11-3.根据类型和id查找

如果IOC容器中存在多个不同名称，相同类型的bean，可以通过@Resource注解的name属性指定唯一的id；

![在这里插入图片描述](https://img-blog.csdnimg.cn/0c6fc647aaf0433791d185c995569e5f.png#pic_center)

![在这里插入图片描述](https://img-blog.csdnimg.cn/793dd15272de45c3aca0e81479f9ca4b.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)

![在这里插入图片描述](https://img-blog.csdnimg.cn/8d869d647a264cfcb94bfba9ca945c13.png#pic_center)



总结：

1. 都是用来**自动装配**的，都可以放在***属性字段***上

2. **@Autowired**通过**byType**（类型）的方式实现，而且**必须要求这个对象存在**！
3. **@Resource**默认通过**byName**（id）的方式实现，如果**找不到名字**，则**通过byType**实现！如果两个都找不到的情况下，就报错！
4. 执行顺序不同：@Autowired通过**byType**的方式实现。@Resource默认通过**byName**的方式实现。



## 12、使用注解开发

在Spring4之后，要使用注解开发，必须保证aop的包导入了

![在这里插入图片描述](https://img-blog.csdnimg.cn/ef4a21a57e5542479071250324945b0a.png#pic_center)

使用注解需要导入**context约束，增加注解的支持**！

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        https://www.springframework.org/schema/context/spring-context.xsd
        http://www.springframework.org/schema/aop
        https://www.springframework.org/schema/aop/spring-aop.xsd">
    <!--开启注解扫描-->
    <context:component-scan base-package="cn.bloghut"/>

    <!--开启注解支持-->
    <context:annotation-config/>

</beans>

```

bean注入使用**@Componet**注解

**等价**于`<bean id="user" class="cn.bloghut.domain.User">`

```java
@Component
public class User {
   
}

```

属性注入使用**@Value**注解

```java
<property name="name" value="闲言">
@Component
public class User {

    private String name;

    @Value("闲言")
    public void  setName(String name){
        this.name = name;
    }
}

```

衍生注解

- **@Componet**有几个衍生注解，在web开发中，会按照mvc三层架构分层！
- **@Service**--------业务层注解
- **@Repository**—持久层注解
- **@Controller**-----控制层注解

**这四个注解功能都是一样的**，都是代表将某个类注册到Spring中，装配Bean



**自动装配**

- **@Autowired** 自动装配通过类型、名字
  如果Autowired不能唯一自动装配上属性，则需要通过**@Qualifier(value=“xxx”)**
- **@Nullable** 字段标记了这个注解，说明这个字段可以为null
- **@Resource** 自动装配通过名字，类型



作用域

```java
@Scope(“singleton”)单例

```

![在这里插入图片描述](https://img-blog.csdnimg.cn/2be3c1f092524a78a436671dfa81df69.png#pic_center)

**总结**

XML 与 注解

- xml更加万能，适用于任何场合！维护简单方便
- 注解不是自己类使用不了， **维护相对复杂**



XML 与 注解最佳实践

- xml用来管理bean
- 注解只**负责完成属性的注入**
- 我们在使用过程中，只需要注意一个问题：**必须让注解生效，就需要开启注解的支持**

```xml
<!--开启注解扫描-->
<context:component-scan base-package="cn.bloghut"/>

<!--开启注解支持-->
<context:annotation-config/>

```



## 13、java的方式配置Spring

  **JavaConfig** 是Spring的 一个子项目，在Spring 4之后，它成为了新功能

![在这里插入图片描述](https://img-blog.csdnimg.cn/5457273e17824fcba193a940fa89e617.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)

1. 首先定义一个类，在类上添加@Component注解，让它加载到Spring IOC容器（让Spring 管理）
2. 定义Java 配置类，在其类上添加@Configuration 注解，说明该类是一个配置类，这个类也会被Spring 托管，因为它本身是一个@Component
3. 在Myconfig 类中 添加getUser 方法，返回一个user对象
4. getUser 方法上的@Bean 注解 则是注册一个bean功能，相当于`<bean id="getUser" class="cn.bloghut.domain.User">`
5. 方法的名字，相当于bean 标签中的id 属性。
6. 方法的返回值，相当于bean 标签中的class属性。（因为我们导包了，Spring 知道是哪一个）
7. 如果完全使用了配置类方式去做，我们只能通过AnnotationConfigApplicationContext 上下文来获取容器，通过配置类的class 对象加载！

![在这里插入图片描述](https://img-blog.csdnimg.cn/b1e6c42105b849e48c0755b2691fef6d.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)

完整代码

- **@Configuration** 这个一个**配置类**
- **@ComponentScan** 用于**扫描包**
- **@Import** 用于**导入其他配置类**



### 13-1.主配置类

```java
@Configuration
@ComponentScan(basePackages = {"cn.bloghut.domain"})
@Import({MyConfig2.class})
public class MyConfig {

    /**
     * 返回一个User Bean
     * @return
     */
    @Bean
    public User getUser(){
        return new User();
    }

}

```



### 13-2.配置类2

```java
@Configuration
public class MyConfig2 {


}

```



### 13-3.User实体类

```java
@Component
public class User {
    private String name;

    public String getName() {
        return name;
    }
    @Value("闲言")
    public void setName(String name) {
        this.name = name;
    }

    @Override
    public String toString() {
        return "User{" +
                "name='" + name + '\'' +
                '}';
    }
}

```



### 13-4.测试类

```java
public class MyTest {
    public static void main(String[] args) {

        ApplicationContext ac = new AnnotationConfigApplicationContext(MyConfig.class);
        User user = ac.getBean("getUser", User.class);
        System.out.println(user);

    }
}

```



## 14、代理模式

### 14-1.角色分析：

1. 抽象角色：一般会使用接口或者抽象类来解决
2. 真实角色：被代理的角色
3. 代理角色：代理 真实角色，代理真实角色后，我们一般会做一些附属操作
4. 客户：访问代理对象的人



代码步骤：

### 14-2.接口

```java
public interface Rent {
    /**
     * 租房
     */
    void rent();
}

```



### 14-3.真实角色

```java
public class Host implements Rent{

    @Override
    public void rent() {
        System.out.println("房东要出租房子");
    }


}

```



### 14-4.代理角色

```java
public class Proxy implements Rent{

    private Host host;

    public Proxy() {
    }

    public Proxy(Host host) {
        this.host = host;
    }

    @Override
    public void rent() {
        seeHouse();
        host.rent();
        fare();
        hetong();
    }
    //看房
    public void seeHouse(){
        System.out.println("中介带你看房");
    }

    //收中介费
    public void fare(){
        System.out.println("收中介费");
    }
    //签合同
    public void hetong(){
        System.out.println("签合同");
    }
}

```



### 14-5.客户端访问代理角色

```java
public class Client {
    public static void main(String[] args) {

        Host host = new Host();
        //代理,中介帮房东，但是呢？代理角色一般会有一些附属操作！
        Proxy proxy = new Proxy(host);
        //你不用面对房东，直接找中介租房即可！
        proxy.rent();
    }
}

```



### 14-6.代理模式的好处：

1. 可以使**真实角色的操作更加存粹**！不用去关注一些公共的业务
   2. **公共交给了代理角色**，实现了业务的分工
2. 公共业务发生扩展的时候，**方便集中管理**



### 14-7.缺点：

- **一个真实角色就会产生一个代理角色，代码量会翻倍** 开发效率变低

![在这里插入图片描述](https://img-blog.csdnimg.cn/7b7ba59dc7654403a11dce13f90fbc26.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)



## 15、静态代理

1. 有一天，公司领导要求我为 某个类的**所有方法新增日志输出功能。**
2. 怎么做呢？
3. 在原来的类上的每一个方法添加日志输出？
4. 这就是改变原来人家的代码了。
5. 改动原有的业务代码，在公司中是大忌！
6. 有可能人家你修改了人家的代码，可能给改蹦了。
7. **新增一个类，制作成本小，职责单一。**

**原来的开发方式（纵向开发）**

![img](https://img-blog.csdnimg.cn/db022b8472644f98b7319f26bb6bc2bd.png#pic_center)

**添加日志功能（横切进去）**

![在这里插入图片描述](https://img-blog.csdnimg.cn/1abb6b2aba2c4082b78e5ffe5815ca95.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)



代码如下：
**业务接口：**

```java
public interface UserService {
    void add();

    void delete();

    void update();

    void query();
}

```



**原来业务类**

```java
public class UserServiceImpl implements UserService {
    @Override
    public void add() {
        System.out.println("新增用户");
    }

    @Override
    public void delete() {
        System.out.println("删除用户");
    }

    @Override
    public void update() {
        System.out.println("修改用户");
    }

    @Override
    public void query() {
        System.out.println("查询用户");
    }
}

```



**代理类**

```java
public class UserServiceProxy implements UserService {

    private UserService userService;

    public void setUserService(UserService userService) {
        this.userService = userService;
    }

    @Override
    public void add() {
        log("add");
        userService.add();
    }

    @Override
    public void delete() {
        log("delete");
        userService.delete();
    }

    @Override
    public void update() {
        log("update");
        userService.update();
    }

    @Override
    public void query() {
        System.out.println("query");
        userService.query();
    }

    //日志方法
    public void log(String msg){
        System.out.println("【Debug 】使用了"+msg+"方法");
    }
}

```



**测试类**

```java
public static void main(String[] args) {

    UserServiceProxy userService = new UserServiceProxy();
    userService.setUserService(new UserServiceImpl());
    userService.add();
}

```



## 16、动态代理

- 动态代理和静态代理角色一样
- **动态代理**的代理类是**动态生成**的，不是我们直接写好的
  动态代理分为两大类：**基于接口**的动态代理，**基于类**的动态代理
- 基于接口：**JDK**动态代理
- 基于类： **cglib**
- java字节码实现： javasist

需要了解两个类：**Proxy** :代理 | **InvocationHandler**：调用处理程序

```java
java.lang.reflect.Proxy

```



Proxy提供了**创建动态代理类和实例的静态方法**，它也是由这些方法创建的所有动态代理类的超类。(大白话：**这是一个静态类，类里边有方法得到代理类)**

  动态代理类 （以下简称为**代理类** ）是一个实现在类创建时在运行时指定的接口列表的类，具有如下所述的行为。 代理接口是由代理类实现的接口。 代理实例是代理类的一个实例。 每个代理实例都有一个关联的调用处理程序对象，它实现了接口

  通过其代理接口之一的代理实例上的方法调用将被分派到实例调用处理程序的invoke方法，传递代理实例， java.lang.reflect.Method被调用方法的java.lang.reflect.Method对象以及包含参数的类型Object Object的数组。 调用处理程序适当地处理编码方法调用，并且返回的结果将作为方法在代理实例上调用的结果返回。

**代理类具有以下属性：**

1. 代理类是公共的，最终的，而不是抽象的，如果所有代理接口都是公共的。
2. 如果任何代理接口是非公开的，代理类是非公开的，最终的，而不是抽象的 。
3. 代理类的不合格名称未指定。 然而，以字符串"$Proxy"开头的类名空间应该保留给代理类。
4. 一个代理类扩展了java.lang.reflect.Proxy 。
5. 代理类完全按照相同的顺序实现其创建时指定的接口。
6. 如果一个代理类实现一个非公共接口，那么它将被定义在与该接口相同的包中。 否则，代理类的包也是未指定的。 请注意，程序包密封不会阻止在运行时在特定程序包中成功定义代理类，并且类也不会由同一类加载器定义，并且与特定签名者具有相同的包。
7. 由于代理类实现了在其创建时指定的所有接口， getInterfaces在其类对象上调用getInterfaces将返回一个包含相同列表接口的数组（按其创建时指定的顺序），在其类对象上调用getMethods将返回一个数组的方法对象，其中包括这些接口中的所有方法，并调用getMethod将在代理接口中找到可以预期的方法。
8. Proxy.isProxyClass方法将返回true，如果它通过代理类 - 由Proxy.getProxyClass返回的类或由Proxy.newProxyInstance返回的对象的类 - 否则为false。
9. 所述java.security.ProtectionDomain代理类的是相同由引导类装载程序装载系统类，如java.lang.Object ，因为是由受信任的系统代码生成代理类的代码。 此保护域通常将被授予java.security.AllPermission 。
10. 每个代理类有一个公共构造一个参数，该接口的实现InvocationHandler ，设置调用处理程序的代理实例。 而不必使用反射API来访问公共构造函数，也可以通过调用Proxy.newProxyInstance方法来创建代理实例，该方法将调用Proxy.getProxyClass的操作与调用处理程序一起调用构造函数。



## 17、基于Proxy类和InvocationHandler 实现动态代理

### 17-1.真实的角色

```java
public class Host implements Rent{


    public void rent() {
        System.out.println("租房");
    }
}

```



## 17-2.被代理的接口

```java
public interface Rent {

    void rent();

}

```



### 17-3.代理 真实的角色 ProxyInvocationHandler

```java
public class ProxyInvocationHandler implements InvocationHandler {

    //被代理的接口
    private Rent rent;


    public void setRent(Rent rent){
        this.rent = rent;
    }
    //生成得到代理类
    public Object getProxy(){
        return  Proxy.newProxyInstance(this.getClass().getClassLoader(),rent.getClass().getInterfaces(),this);
    }
    /**
     * 处理代理实例，并返回结果
     * @param proxy
     * @param method
     * @param args
     * @return
     * @throws Throwable
     */
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
        //动态代理的本质，就是使用反射机制
        //在方法调用前调用
        seeHouse();
        Object result = method.invoke(rent,args);
        //在方法调用后调用
        heTong();
        return result;
    }
    public void seeHouse(){
        System.out.println("看房子");
    }
    public void heTong(){
        System.out.println("签合同");
    }

```



### 17-4.用户

```java
public class Client {
    public static void main(String[] args) {
        //创建真实角色
        Host host = new Host();
        //创建代理角色 不存在
        ProxyInvocationHandler proxyInvocationHandler = new ProxyInvocationHandler();
        //设置要代理的对象
        proxyInvocationHandler.setRent(host);
        //获取代理对象，并强制转换
        Rent proxy = (Rent)proxyInvocationHandler.getProxy();
        //调用
        proxy.rent();
    }
}

```



### 17-5.输出结果

```json
看房子
租房
签合同

```



## 18、基于Proxy类和InvocationHandler 实现动态代理 2

**Proxy**：生成动态代理实例的
**InvocationHandler**：调用处理程序并返回结果的



万能的自动生成代理类

```java
package cn.bloghut.demo3;

import java.lang.reflect.InvocationHandler;
import java.lang.reflect.Method;
import java.lang.reflect.Proxy;

/**
 * @Classname ProxyInvocationHandler
 * @Description 自动生成代理类
 * @Date 2021/5/17 15:44
 * @Created by 闲言
 */
public class ProxyInvocationHandler implements InvocationHandler {

    //1.被代理的接口
    public Object target;

    public void  setTarget(Object target){
        this.target = target;
    }

    //2.生成得到代理类（代理谁）
    public Object getProxy(){
        return Proxy.newProxyInstance(this.getClass().getClassLoader(),
                target.getClass().getInterfaces(),this);
    }

    //3.处理代理实例，并返回结果（代用代理程序）
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
        //动态获取方法名称
        log(method.getName());
        Object result = method.invoke(target, args);
        return result;
    }
    /**
     * 打印日志方法
     * @param msg
     */
    public void log(String msg){
        System.out.println("[debug]===> 执行可"+msg+"方法");
    }
}

```

测试

```java
public static void main(String[] args) {

    //真实角色
    UserServiceImpl userService = new UserServiceImpl();
    //代理角色，不存在
    ProxyInvocationHandler invocationHandler = new ProxyInvocationHandler();
    //设置要代理的对象
    invocationHandler.setTarget(userService);
    //获取代理对象
    UserService proxy = (UserService)invocationHandler.getProxy();
    //执行方法
    proxy.query();
}

```

结果

```json
[debug]===> 执行可query方法
query

```



## 19、动态代理和静态代理总结

### 19-1.静态代理

1. 由程序员创建或由特定工具自动生成源代码，再对其编译。在程序运行前，代理类的.class文件就已经存在了
2. 静态代理通常只代理一个类
3. 静态代理事先知道要代理的是什么

代码如下：

1. 如下， **HelloServiceProxy**类是代理类，**HelloServiceImpl**类是委托类，这两个类都实现了**HelloService**接口。
2. 其中**HelloServiceImpl**类是HelloService接口的真正实现者，而**HelloServiceProxy**类是通过调用**HelloServiceImpl**类的相关方法来提供特定服务的。
3. **HelloServiceProxy**类的**echo()方法和getTime()方法会分别调用被代理的HelloServiceImpl**对象的echo()方法和getTime()方法，并且在方法调用前后都会执行一些简单的打印操作。
4. 由此可见，代理类可以为委托类预处理消息、把消息转发给委托类和事后处理消息等。

**HelloService接口**

```java
public interface HelloService {
    String echo(String msg);

    Date getTime();
}

HelloServiceImpl委托类
public class HelloServiceImpl implements HelloService {
    @Override
    public String echo(String msg) {
        return "echo:" + msg;
    }

    @Override
    public Date getTime() {
        return new Date();
    }
}

```



**HelloServiceProxy代理类**

```java
public class HelloServiceProxy implements HelloService {

    //表示被代理的HelloService 实例
    private HelloService helloService;

    public HelloServiceProxy(HelloService helloService) {
        this.helloService = helloService;
    }

    public void setHelloServiceProxy(HelloService helloService) {
        this.helloService = helloService;
    }

    @Override
    public String echo(String msg) {
        //预处理
        System.out.println("before calling echo()");
        //调用被代理的HelloService 实例的echo()方法
        String result = helloService.echo(msg);
        //事后处理
        System.out.println("after calling echo()");
        return result;
    }


    public Date getTime() {
        //预处理
        System.out.println("before calling getTime()");
        //调用被代理的HelloService 实例的getTime()方法
        Date date = helloService.getTime();
        //事后处理
        System.out.println("after calling getTime()");
        return date;
    }
}

```



**测试**

```java
public class Test {
    public static void main(String[] args) {
        //创建委托类
        HelloServiceImpl helloService = new HelloServiceImpl();
        //创建代理类
        HelloServiceProxy helloServiceProxy = new HelloServiceProxy(helloService);
        //调用方法
        Date time = helloServiceProxy.getTime();
        System.out.println(time);
    }
}

```



### 19-2.动态代理

1. 在程序运行时，运用**反射机制动态创建**而成
2. 动态代理是代理**一个接口下的多个实现类**
3. 动态代理不知道要代理什么东西，只有在运行时才知道

与静态代理类对照的是动态代理类，动态代理类的字节码在程序运行时由Java反射机制动态生成，无需程序员手工编写它的源代码。动态代理类不仅简化了编程工作，而且提高了软件系统的可扩展性，因为Java反射机制可以生成任意类型的动态代理类。java.lang.reflect 包中的**Proxy**类和**InvocationHandler**接口提供了生成动态代理类的能力。

  Proxy类提供了创建动态代理类及其实例的静态方法。
代码如下：

```java
public static void main(String[] args) {

    //真实角色
    HelloServiceImpl helloService = new HelloServiceImpl();
    //代理角色  不存在
    ProxyInvocationHandler proxyInvocationHandler = new ProxyInvocationHandler();
    proxyInvocationHandler.setTarget(helloService);
    HelloService proxy = (HelloService)proxyInvocationHandler.getProxy();
    //执行方法
    String echo = proxy.echo("Proxy InvocationHandler 实现动态代理");
    System.out.println(echo);
}

```



输出

```java
代理方法执行前调用
代理方法执行后调用
echo:Proxy InvocationHandler 实现动态代理

```

```java
public class ProxyInvocationHandler implements InvocationHandler {

    //要代理的类
    private Object target;

    public void setTarget(Object target){
        this.target = target;
    }

    //获取要代理的实例
    public Object getProxy(){
        return Proxy.newProxyInstance(this.getClass().getClassLoader(),target.getClass().getInterfaces(),this);
    }

    //执行代理的方法
    @Override
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
        System.out.println("代理方法执行前调用");
        //执行方法
        Object result = method.invoke(target, args);
        System.out.println("代理方法执行后调用");

        return result;
    }
}

```



## 20、什么是Aop

  AOP（Aspect Oriented Programming）意为：**面向切面编程**，通过**预编译方式**和运行期**动态代理**实现程序功能的统一维护的一种技术，AOP是OOP的延续，是软件开发中的一个热点，也是Spring框架中的一个重要内容，是函数式编程的一种衍生泛型。利用AOP可以对业务逻辑的各个部分进行隔离，从而使得业务逻辑各部分之间的耦合度降低，提高程序的可重用性，同时提高了开发的效率。
![在这里插入图片描述](https://img-blog.csdnimg.cn/7dd0a4dcd2974316955fe9aa42dab06e.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)



### 20-1.Aop在Spring中的作用

**提供声明事务**：允许用户自定义切面

1. 横切关注点：跨越应用程序多个模块的方法或功能。即与我们的业务逻辑无关的，但是我们需要关注的部分，就是横切关注点。如日志，安全，缓存，事务等等。。。
2. 切面（ASPECT）：横切关注点 被模块化的特殊对象。即 它是一个类
3. 通知（Advice）：切面必须要完成的工作，即 他是类中的一个方法
4. 目标（target）：被通知的对象
5. 代理（Proxy）：向目标对象应用通知之后创建的对象
6. 切入点（PointCut）：切面通知 执行的"地点"的定义
7. 连接点（jointPoint）：与切入点匹配的执行点

![在这里插入图片描述](https://img-blog.csdnimg.cn/573e40d9397e414fa66b235b18777908.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)

Spring Aop中，通过Advice定义横切逻辑，Spring中支持的5种类型的Advice

![在这里插入图片描述](https://img-blog.csdnimg.cn/ec3cd615b20d4a59a6d27f13dedf5650.png#pic_center)



## 21、Aop 实现方式1-基于原生API

### 21-1.导入依赖

```xml
<dependency>
    <groupId>org.aspectj</groupId>
    <artifactId>aspectjweaver</artifactId>
    <version>1.9.4</version>
</dependency>

```



### 21-2.在执行UserService实现类的所有方法前，增加日志功能

```java
public class Log implements MethodBeforeAdvice {

    /**
     *
     * @param method 要执行的目标对象方法
     * @param args 参数
     * @param target       目标对象
     * @throws Throwable
     */
    public void before(Method method, Object[] args, Object target) throws Throwable {
        System.out.println(target.getClass().getName()+" 的 "+method.getName()+"方法执行了");
    }

}

```

### 21-3.在执行UserService实现类的所有方法后，增加日志功能

```java
public class AfterLog implements AfterReturningAdvice {

    /**
     *
     * @param returnValue 返回值
     * @param method
     * @param args
     * @param target
     * @throws Throwable
     */
    public void afterReturning(Object returnValue, Method method, Object[] args, Object target) throws Throwable {
        System.out.println("执行了"+method.getName()+"方法， 返回结果为"+returnValue);
    }
}

```

### 21-4.UserService 接口

```java
public interface UserService {
    void add();

    void delete();

    void update();

    void select();
}

```

### 21-5.UserServiceImpl 接口

```java
public class UserServiceImpl implements UserService {
    public void add() {
        System.out.println("add");
    }

    public void delete() {
        System.out.println("delete");
    }

    public void update() {
        System.out.println("update");
    }

    public void select() {
        System.out.println("select");
    }
}

```

### 21-6.bean.xml 文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       https://www.springframework.org/schema/beans/spring-beans.xsd
       http://www.springframework.org/schema/context
       https://www.springframework.org/schema/context/spring-context.xsd
       http://www.springframework.org/schema/aop
       https://www.springframework.org/schema/aop/spring-aop.xsd">


    <!--注册bean-->
    <bean id="userService" class="cn.bloghut.service.UserServiceImpl"/>
    <bean id="afterLog" class="cn.bloghut.log.AfterLog"/>
    <bean id="log" class="cn.bloghut.log.Log"/>

    <!--方式一，使用原生的Api 接口-->
    <!--配置aop-->
    <aop:config>
        <!--1.配置切入点  pointcut 切入点 expression 表达式, execution(要执行的位置!)-->
        <!-- 切入点  在什么地方执行你的代码-->
        <aop:pointcut id="pointcut" expression="execution(* cn.bloghut.service.UserServiceImpl.*(..))"/>

        <!--执行环绕增加！-->
        <aop:advisor advice-ref="log" pointcut-ref="pointcut"/>
        <aop:advisor advice-ref="afterLog" pointcut-ref="pointcut"/>

    </aop:config>

</beans>

```



### 21-7.测试类

```java
public class Test {
    public static void main(String[] args) {

        ApplicationContext ac = new ClassPathXmlApplicationContext("bean.xml");
        //动态代理 代理的是接口
        UserService userService = (UserService)ac.getBean("userService");
        userService.add();

    }
}

```



### 21-7.输出结果

```tex
cn.bloghut.service.UserServiceImpl 的 add方法执行了
add
执行了add方法， 返回结果为null

```



## 22、Aop 实现方式2-切面方式

1. 配置文件
2. 配置aop
3. 配置切入点
4. 配置自定义切面要引用的类
5. 在哪个方法配置

### 22-1.配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       https://www.springframework.org/schema/beans/spring-beans.xsd
       http://www.springframework.org/schema/context
       https://www.springframework.org/schema/context/spring-context.xsd
       http://www.springframework.org/schema/aop
       https://www.springframework.org/schema/aop/spring-aop.xsd">


    <!--注册bean-->
    <bean id="userService" class="cn.bloghut.service.UserServiceImpl"/>
    <bean id="diyPointCut" class="cn.bloghut.diy.DiyPointCut"/>

    <!--方式一，使用原生的Api 接口-->
    <!--配置aop-->
    <aop:config>
        <!--1.配置切入点  pointcut 切入点 expression 表达式, execution(要执行的位置!)-->
        <!-- 切入点  在什么地方执行你的代码-->
        <aop:pointcut id="pointcut" expression="execution(* cn.bloghut.service.UserServiceImpl.*(..))"/>

        <!--自定切面 ref 要引用的类-->
        <aop:aspect id="aspect" ref="diyPointCut">
            <!--方法执行前 method：切入的方法 pointcut：切入点 -->
            <aop:before method="before" pointcut-ref="pointcut"/>
            <!--方法执行后-->
            <aop:after method="after" pointcut-ref="pointcut"/>
        </aop:aspect>

    </aop:config>

</beans>

```

### 22-2.自定义切面

```java
package cn.bloghut.diy;

/**
 * @Classname DiyPointCut
 * @Description TODO
 * @Date 2021/5/17 17:23
 * @Created by 闲言
 */
public class DiyPointCut {

    public void  before(){
        System.out.println("=======方法执行之前===========");
    }

    public void after(){
        System.out.println("=======方法执行之后===========");
    }

}

```



### 22-3.Usersevice 接口

```java
package cn.bloghut.service;

/**
 * @Classname UserService
 * @Description TODO
 * @Date 2021/5/17 16:51
 * @Created by 闲言
 */
public interface UserService {
    void add();

    void delete();

    void update();

    void select();
}

```



### 22-4.UserServiceImpl 实现类

```java
package cn.bloghut.service;

/**
 * @Classname UserServiceImpl
 * @Description TODO
 * @Date 2021/5/17 16:51
 * @Created by 闲言
 */
public class UserServiceImpl implements UserService {
    public void add() {
        System.out.println("add");
    }

    public void delete() {
        System.out.println("delete");
    }

    public void update() {
        System.out.println("update");
    }

    public void select() {
        System.out.println("select");
    }
}

```



### 22-5.测试类

```java
package cn.bloghut.test;

import cn.bloghut.service.UserService;
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

/**
 * @Classname Test2
 * @Description TODO
 * @Date 2021/5/17 17:24
 * @Created by 闲言
 */
public class Test2 {
    public static void main(String[] args) {

        ApplicationContext ac = new ClassPathXmlApplicationContext("bean2.xml");
        UserService userService = ac.getBean("userService", UserService.class);
        userService.select();
    }
}

```



### 22-6.输出

```tex
=======方法执行之前===========
select
=======方法执行之后===========

```



## 23、Aop 实现方式3-注解方式

### 23-1.bean配置文件

- 注意开启注解aop支持
- `<aop:aspectj-autoproxy/>`

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       https://www.springframework.org/schema/beans/spring-beans.xsd
       http://www.springframework.org/schema/context
       https://www.springframework.org/schema/context/spring-context.xsd
       http://www.springframework.org/schema/aop
       https://www.springframework.org/schema/aop/spring-aop.xsd">

    <!--注册bean-->
    <bean id="userService" class="cn.bloghut.service.UserServiceImpl"/>

    <bean id="annotationPointcut" class="cn.bloghut.annotation.AnnotationPointcut"/>

    <!--开启aop 注解支持-->
    <aop:aspectj-autoproxy/>


</beans>

```





### 23-2.自定义类

- 标注这是一个切面
- `@Aspect //`标注这个类是一个切面

```java
public class AnnotationPointcut {
    /**
     * 定义切入点
     */
    @Pointcut("execution(* cn.bloghut.service.UserServiceImpl.*(..))")
    public void pointcut(){}

    @Before("pointcut()")
    public void  before(){
        System.out.println("=================方法执行前=================");
    }

    @After("pointcut()")
    public void  after(){
        System.out.println("=================方法执行后=================");
    }
}

```



### 23-3.UserService 类：

```java
public interface UserService {
    void add();

    void delete();

    void update();

    void select();
}

```



### 23-4.UserServiceImpl 类

```java
public class UserServiceImpl implements UserService {
    public void add() {
        System.out.println("add");
    }

    public void delete() {
        System.out.println("delete");
    }

    public void update() {
        System.out.println("update");
    }

    public void select() {
        System.out.println("select");
    }
}

```



### 23-5.测试类

```java
public static void main(String[] args) {

    ApplicationContext ac = new ClassPathXmlApplicationContext("bean3.xml");
    UserService userService = ac.getBean("userService", UserService.class);
    userService.delete();
}

```



### 23-6.输出结果

```tex
=================方法执行前=================
delete
=================方法执行后=================

```



## 24、Spring 整合Mybatis

### 24-1.导入依赖

```xml
<dependencies>
    <!--单元测试-->
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.13</version>
        <scope>test</scope>
    </dependency>
    <!--mysql 驱动-->
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>5.1.47</version>
    </dependency>
    <!--mybatis 包-->
    <dependency>
        <groupId>org.mybatis</groupId>
        <artifactId>mybatis</artifactId>
        <version>3.5.2</version>
    </dependency>
    <!--spring 的 context core -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-webmvc</artifactId>
        <version>5.2.0.RELEASE</version>
    </dependency>
    <!--Spring操作数据库的话，还需要一个spring-jdbc-->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-jdbc</artifactId>
        <version>5.1.9.RELEASE</version>
    </dependency>
    <!--Aop 支持-->
    <dependency>
        <groupId>org.aspectj</groupId>
        <artifactId>aspectjweaver</artifactId>
        <version>1.9.4</version>
    </dependency>
    <dependency>
        <groupId>org.aspectj</groupId>
        <artifactId>aspectjrt</artifactId>
        <version>1.8.13</version>
    </dependency>
    <!--mybatis 整合 spring 的依赖-->
    <dependency>
        <groupId>org.mybatis</groupId>
        <artifactId>mybatis-spring</artifactId>
        <version>2.0.2</version>
    </dependency>
    <!--setter 构造方法插件-->
    <dependency>
        <groupId>org.projectlombok</groupId>
        <artifactId>lombok</artifactId>
        <version>1.16.10</version>
    </dependency>
</dependencies>

```



### 24-2.编写数据源配置

```xml
<!--
    DataSource：使用Spring 的数据源 替换Mybatis 的配置 c3p0 dbcp druid
    使用Spring 提供的JDBC org.springframework.jdbc.datasource.
-->

<!--配置数据源-->
<bean id="dataSource" class="org.springframework.jdbc.datasource.DriverManagerDataSource">
    <property name="driverClassName" value="com.mysql.jdbc.Driver"/>
    <property name="url" value="jdbc:mysql://localhost:3306/mybatis"/>
    <property name="username" value="root"/>
    <property name="password" value="123"/>
</bean>

2.sqlSessionFactory
<!--配置sqlSessionFactory 工厂-->
<bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
    <property name="dataSource" ref="dataSource"/>
    <!--绑定mybatis的配置文件-->
    <property name="mapperLocations" value="classpath:cn/bloghut/mapper/*Mapper.xml"/>
    <!--配置别名-->
    <property name="typeAliases" value="cn.bloghut.domain.User"/>
</bean>

3.sqlSessionTemplate
<!--SqlSessionTemplate 就是sqlSession-->
<bean id="sqlSession" class="org.mybatis.spring.SqlSessionTemplate">
    <constructor-arg index="0" ref="sqlSessionFactory"/>
</bean>

```



### 24-3.需要给接口加实现类【】

```java
public class UserMapperImpl implements UserMapper {

    // 我们所有的操作，都使用sqlSession 来执行，在原来，现在都使用SQLSessionTemplate

    private SqlSessionTemplate sqlSession;

    public void setSqlSessionTemplate(SqlSessionTemplate sqlSession){
        this.sqlSession = sqlSession;
    }


    public List<User> findAll() {
        return sqlSession.getMapper(UserMapper.class).findAll();
    }
}

```



### 24-4.将自己写的实现类，注入到容器中

```xml
<bean id="userMapper" class="cn.bloghut.mapper.impl.UserMapperImpl">
    <property name="sqlSessionTemplate" ref="sqlSession"/>
</bean>

```



### 24-5.测试

```java
@Test
public void test1(){
    ApplicationContext ac = new ClassPathXmlApplicationContext("applicationContext.xml");
    UserMapper userMapper = ac.getBean("userMapper", UserMapper.class);
    List<User> all = userMapper.findAll();
    for (User user : all) {
        System.out.println(user);
    }
}

```



## 25、声明式事务

### 25-1.什么是事务

- 事务：**把一组业务当成一个业务来做**，要么都成功，要么都失败！
- 事务在项目开发中十分的重要，涉及到数据的一致性问题，不能马虎！
- 确保完整性和一致性



### 25-2.事务ACID 原则：

1. 原则性
2. 一致性
3. 隔离性
   **多个业务可能操作同一个资源，防止数据损坏**
4. 持久性
   **事务一旦提交，无论系统发生什么问题，结果都不会被影响，被持久化的写到存储器中！**



### 25-3.为什么需要事务？

1. 如果不配置事务，可能存在数据提交不一致的情况下；
2. 如果我们不在Spring 中去配置 声明式事务，我们就需要在代码中手动配置事务
3. 事务在项目开发中十分重要，涉及到数据的一致性和完整性问题，不容马虎！



## 26、声明式事务代码

### 26-1.spring-dao.xml

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xmlns:tx="http://www.springframework.org/schema/tx"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/aop
        https://www.springframework.org/schema/aop/spring-aop.xsd
        http://www.springframework.org/schema/tx
        http://www.springframework.org/schema/tx/spring-tx.xsd">

    <!--
        DataSource：使用Spring 的数据源 替换Mybatis 的配置 c3p0 dbcp druid
        使用Spring 提供的JDBC org.springframework.jdbc.datasource.
    -->

    <!--配置数据源-->
    <bean id="dataSource" class="org.springframework.jdbc.datasource.DriverManagerDataSource">
        <property name="driverClassName" value="com.mysql.jdbc.Driver"/>
        <property name="url" value="jdbc:mysql://localhost:3306/mybatis"/>
        <property name="username" value="root"/>
        <property name="password" value="123"/>
    </bean>

    <!--配置sqlSessionFactory 工厂-->
    <bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
        <property name="dataSource" ref="dataSource"/>
        <!--绑定mybatis的配置文件-->
        <property name="mapperLocations" value="classpath:cn/bloghut/mapper/*Mapper.xml"/>
        <!--配置别名-->
        <property name="typeAliases" value="cn.bloghut.domain.User"/>
    </bean>

    <!--SqlSessionTemplate 就是sqlSession-->
    <bean id="sqlSession" class="org.mybatis.spring.SqlSessionTemplate">
        <!--只能使用构造器注入sqlSessionFactory，因为它没有 set 方法-->
        <constructor-arg index="0" ref="sqlSessionFactory"/>
    </bean>

    <!--==============================事务配置开始==============================-->

    <!--配置声明式事务-->
    <bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
        <property name="dataSource" ref="dataSource"/>
    </bean>

    <!--结合AOP 实现事务的织入-->
    <tx:advice id="txAdvice" transaction-manager="transactionManager">
        <tx:attributes>
           <!--给哪些方法配置事务-->
            <!--配置事务的传播特性：
                propagation
                read-only="true" 只读
            -->
            <tx:method name="add" propagation="REQUIRED"/>
            <tx:method name="delete" propagation="REQUIRED"/>
            <tx:method name="update" propagation="REQUIRED"/>
            <tx:method name="find" read-only="true"/>

            <!--给所有方法配置事务-->
            <tx:method name="*" propagation="REQUIRED"/>
        </tx:attributes>
    </tx:advice>

    <!--配置事务切入-->
    <aop:config>
        <!--配置切入点-->
        <aop:pointcut id="txPointcut" expression="execution(* cn.bloghut.mapper.*.*(..))"/>
        <!--切入事务-->
        <aop:advisor advice-ref="txAdvice" pointcut-ref="txPointcut"/>
    </aop:config>

    <!--==============================事务配置结束==============================-->

</beans>

```



### 26-2.applicationContext.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:p="http://www.springframework.org/schema/p"
       xmlns:c="http://www.springframework.org/schema/c"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">

    <import resource="spring-dao.xml"/>

   <bean id="userMapper" class="cn.bloghut.mapper.impl.UserMapperImpl">
       <property name="sqlSession" ref="sqlSession"/>
   </bean>


</beans>

```



### 26-3.user 实体类

```java
@Data
@AllArgsConstructor
@NoArgsConstructor
public class User {

    private int id;
    private String username;
    private String password;
    private String perms;

}

```



### 26-4.UserMaper接口

```java
public interface UserMapper {

    List<User> findAll();

    int add(User user);

    int delete(int id);

}

```



### 26-5.UserMapper配置文件

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="cn.bloghut.mapper.UserMapper">
    <select id="findAll" resultType="cn.bloghut.domain.User">
        select * from user;
    </select>

    <insert id="add" parameterType="cn.bloghut.domain.User">
    insert into user(username,password,perms) values (#{username},#{password},#{perms})
    </insert>

    <delete id="delete" parameterType="int">
    delete form user where id = #{value}
    </delete>

</mapper>

```



### 26-6.UserMapper 实现类

```java
public class UserMapperImpl implements UserMapper {

    private SqlSessionTemplate sqlSession;

    public void setSqlSession(SqlSessionTemplate sqlSession) {
        this.sqlSession = sqlSession;
    }

    public List<User> findAll() {
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        User user = new User();
        user.setUsername("闲言");
        user.setPassword("123");
        user.setPerms("admin");

        mapper.add(user);
        int i = 1 / 0;
        mapper.delete(6);
        return mapper.findAll();
    }

    public int add(User user) {
        return sqlSession.getMapper(UserMapper.class).add(user);
    }

    public int delete(int id) {
        return sqlSession.getMapper(UserMapper.class).delete(id);
    }
}

```



### 26-7.测试

```java
public static void main(String[] args) {

    ApplicationContext ac = new ClassPathXmlApplicationContext("applicationContext.xml");
    UserMapper userMapper = ac.getBean("userMapper", UserMapper.class);
    List<User> users = userMapper.findAll();
    for (User user : users) {
        System.out.println(user);
    }
}

```

