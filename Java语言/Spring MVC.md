# Spring MVC

## 1、什么是MVC

1. MVC：**模型**（Model）+View（**视图**）+**控制器**（Controller）的简写
2. 是将 **逻辑**、**数据**、**显示 分离**的方法来组织代码。
3. MVC 主要的作用是**降低视图与业务逻辑**间的双向耦合
4. MVC不是一种设计模式，MVC**是一种架构模式**。当然不同的MVC存在差异

**Model（模型）**：数据模型，**提供要展示的数据**，因此包含数据和行为，可以认为是领域模型或JavaBean组件（包含数据和行为），不过现在一般都分离开来：Value Object（数据Dao） 和 服务层（行为Service）。也就是模型提供了模型数据查询和模型数据的状态更新等功能，**包括数据和业务**。

View（视图）：**负责进行模型的展示**，一般就是我们见到的用户界面，客户想看到的东西。

Controller（控制器）：**接收用户请求，委托给模型进行处理**（状态改变），处理完毕后把返回的模型数据返回给视图，由视图负责展示。也就是说控制器做了个**调度员的工作**。

最典型的MVC就是**JSP + servlet + javabean**的模式。

JSP ： 本质就是一个**Servlet**

![在这里插入图片描述](https://img-blog.csdnimg.cn/4a52b66c4e404efe83ae93d651fc8839.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)



### 1.1、Model1时代

在web早期的开发中，通常采用的都是Model1。
Model1中，主要分为两层，视图层和模型层。

![在这里插入图片描述](https://img-blog.csdnimg.cn/1e9893849a9f4508955c8408198d414e.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)

Model1优点：架构简单，比较适合小型项目开发；
Model1缺点：JSP职责不单一，职责过重，不便于维护；



### 1.2、Model2时代

Model2把一个项目分成三部分，包括视图、控制、模型。

![在这里插入图片描述](https://img-blog.csdnimg.cn/438edc664dd9435fa57ce2da7cc5304f.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)

1. 用户发请求
2. Servlet接收请求数据，并调用对应的业务逻辑方法
3. 业务处理完毕，返回更新后的数据给servlet
4. servlet转向到JSP，由JSP来渲染页面
5. 响应给前端更新后的页面

**职责分析：**
**Controller：控制器**

1. 取得表单数据
2. 调用业务逻辑
3. 转向指定的页面



**Model：模型**

1. 业务逻辑
2. 保存数据的状态



**View：视图**

1. 显示页面

2. Model2这样不仅提高的代码的复用率与项目的扩展性，且大大降低了项目的维护成本。

3. Model 1模式的实现比较简单，适用于快速开发小规模项目，Model1中JSP页面身兼View和Controller两种角色，将控制逻辑和表现逻辑混杂在一起，从而导致代码的重用性非常低，增加了应用的扩展性和维护的难度。Model2消除了Model1的缺点。



### 1.3、回顾[Servlet]

1.新建一个Maven工程当做父工程！pom依赖！

```xml
<dependencies>
    <!--单元测试-->
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.12</version>
    </dependency>
    <!--
        包含了：AOP，bean，context，core，web
    -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-webmvc</artifactId>
        <version>5.1.9.RELEASE</version>
    </dependency>
    <!--servlet依赖 -->
    <dependency>
        <groupId>javax.servlet</groupId>
        <artifactId>servlet-api</artifactId>
        <version>2.5</version>
    </dependency>
    <!--jsp 依赖-->
    <dependency>
        <groupId>javax.servlet.jsp</groupId>
        <artifactId>jsp-api</artifactId>
        <version>2.2</version>
    </dependency>
    <!--jstl依赖-->
    <dependency>
        <groupId>javax.servlet</groupId>
        <artifactId>jstl</artifactId>
        <version>1.2</version>
    </dependency>
</dependencies>

```



2.建立一个Moudle：springmvc-01-servlet ， 添加Web app的支持！
3.导入servlet 和 jsp 的 jar 依赖

```xml
<!--servlet依赖 -->
<dependency>
    <groupId>javax.servlet</groupId>
    <artifactId>servlet-api</artifactId>
    <version>2.5</version>
</dependency>
<!--jsp 依赖-->
<dependency>
    <groupId>javax.servlet.jsp</groupId>
    <artifactId>jsp-api</artifactId>
    <version>2.2</version>
</dependency>

```



4.编写一个Servlet类，用来处理用户的请求

```java
public class HelloServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //获取前端参数
        String method = req.getParameter("method");
        if ("add".equals(method)){
            req.getSession().setAttribute("msg","调用了add方法");
        }else if ("delete".equals(method)){
            req.getSession().setAttribute("msg","调用了delete方法");
        }
        //2.调用业务层
        //3.请求转发
        req.getRequestDispatcher("/WEB-INF/jsp/test.jsp").forward(req,resp);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req,resp);
    }
}

```



5.编写test.jsp，在WEB-INF目录下新建一个jsp的文件夹，新建test.jsp

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
    <h1>${msg}</h1>
</body>
</html>

```



6.在web.xml中注册Servlet

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">

    <servlet>
        <servlet-name>helloServlet</servlet-name>
        <servlet-class>cn.bloghut.HelloServlet</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>helloServlet</servlet-name>
        <url-pattern>/hello</url-pattern>
    </servlet-mapping>
</web-app>

```



7.配置Tomcat，并启动测试

```toml
localhost:8080/user?method=add
localhost:8080/user?method=delete

```



## 2、什么是SpringMVC

### 2.1、概述

**Spring MVC是Spring Framework的一部分，是基于Java实现MVC的轻量级Web框架。**

官方文档

```http
https://docs.spring.io/spring/docs/5.2.0.RELEASE/spring-framework-reference/web.html#spring-web

```



**我们为什么要学习SpringMVC呢?**
Spring MVC的特点：

1. 轻量级，简单易学
2. 高效 , 基于请求响应的MVC框架
3. 与Spring兼容性好，无缝结合
4. 约定优于配置
5. 功能强大：RESTful、数据验证、格式化、本地化、主题等
6. 简洁灵活

Spring的web框架围绕**DispatcherServlet** [ 调度Servlet ] 设计。

  **DispatcherServlet**的作用是将请求分发到不同的处理器。从Spring 2.5开始，使用Java 5或者以上版本的用户可以采用基于注解形式进行开发，十分简洁；

  正因为SpringMVC好 , **简单 , 便捷 , 易学** , 天生和Spring无缝集成(使用SpringIoC和Aop) , 使用**约定优于配置** . 能够进行简单的junit测试 . 支持Restful风格 .异常处理 , 本地化 , 国际化 , 数据验证 , 类型转换 , 拦截器 等等…所以我们要学习 .

**最重要的一点还是用的人多 , 使用的公司多**



### 2.2、中心控制器

Spring的web框架围绕**DispatcherServlet设计**。DispatcherServlet的**作用是将请求分发到不同的处理器**。从Spring 2.5开始，使用Java 5或者以上版本的用户可以采用基于注解的controller声明方式。
  Spring MVC框架像许多其他MVC框架一样, 以请求为驱动 , 围绕一个中心Servlet分派请求及提供其他功能，**DispatcherServlet是一个实际的Servlet (它继承自HttpServlet 基类)。**
![在这里插入图片描述](https://img-blog.csdnimg.cn/c9f4be7c502144be8f5451916048b380.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)



**SpringMVC的原理如下图所示：**
  当发起请求时被前置的控制器拦截到请求，根据请求参数生成代理请求，找到请求对应的实际控制器，控制器处理请求，创建数据模型，访问数据库，将模型响应给中心控制器，控制器使用模型与视图渲染视图结果，将结果返回给中心控制器，再将结果返回给请求者。

![在这里插入图片描述](https://img-blog.csdnimg.cn/390a3484a6f348b9bdcd61eb951ea30d.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)

![在这里插入图片描述](https://img-blog.csdnimg.cn/b8ff9f6359a7477c8506517b3833e49e.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)



### 2.3、第一个MVC程序

1、新建一个Moudle ， springmvc-02-hello ， 添加web的支持！
2、确定导入了SpringMVC 的依赖！
3、配置web.xml ， 注册DispatcherServlet

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">
    <!--配置中间处理器-->
    <servlet>
        <servlet-name>dispatcherServlet</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>classpath:springmvc.xml</param-value>
        </init-param>
        <!--启动级别-->
        <load-on-startup>1</load-on-startup>
    </servlet>
    <!--匹配所有的请求，不包括jsp -->
    <servlet-mapping>
        <servlet-name>dispatcherServlet</servlet-name>
        <url-pattern>/</url-pattern>
    </servlet-mapping>
</web-app>

```



4、编写SpringMVC 的 配置文件！名称：springmvc-servlet.xml : [servletname]-servlet.xml
说明，这里的名称要求是按照官方来的

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/mvc
        http://www.springframework.org/schema/mvc/spring-mvc.xsd
        http://www.springframework.org/schema/context
        http://www.springframework.org/schema/context/spring-context.xsd">

</beans>

```



5、添加 处理映射器

```xml
<bean class="org.springframework.web.servlet.handler.BeanNameUrlHandlerMapping"/>

```



6、添加 处理器适配器

```xml
<bean class="org.springframework.web.servlet.mvc.SimpleControllerHandlerAdapter"/>

```



7、添加 视图解析器

```xml
<!--配置视图解析器对象-->
<bean id="internalResourceViewResolver" class="org.springframework.web.servlet.view.InternalResourceViewResolver">
    <!--配置文件所在的目录-->
    <property name="prefix" value="/WEB-INF/jsp/"/>
    <!--配置文件的后缀名-->
    <property name="suffix" value=".jsp"/>
</bean>

```



8、编写我们要操作业务Controller ，要么实现Controller接口，要么增加注解；需要返回一个ModelAndView，装数据，封视图；

```java
public class HelloController implements Controller {
    @Override
    public ModelAndView handleRequest(HttpServletRequest request, HttpServletResponse response) throws Exception {
        //ModelAndView 模型和 视图
        ModelAndView modelAndView = new ModelAndView();
        //封装对象，放到ModelAndView中
        modelAndView.addObject("msg","hello");
        modelAndView.setViewName("success");//WEB-INF/jsp/success.jsp
        return modelAndView;
    }
}

```



9、将自己的类交给SpringIOC容器，注册bean

```jsp
<!--Handler-->
<bean name="/hello" class="cn.bloghut.controller.HelloController"/>
10、写要跳转的jsp页面，显示ModelandView存放的数据，以及我们的正常页面；
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
    <h1>${msg}</h1>
</body>
</html>

```



11、配置Tomcat 启动测试！

![在这里插入图片描述](https://img-blog.csdnimg.cn/98063e27a9d54b5b9260ed6c70c301d5.png#pic_center)

可能遇到的问题：访问出现404，排查步骤：
查看控制台输出，看一下是不是缺少了什么jar包。

![在这里插入图片描述](https://img-blog.csdnimg.cn/a384091424cf4b6caf6c1ad569bbafdc.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)

如果jar包存在，显示无法输出，就在IDEA的项目发布中，添加lib依赖！
重启Tomcat 即可解决！



### 2.4、SpringMVC执行原理

![在这里插入图片描述](https://img-blog.csdnimg.cn/a04a7785787c477fbdfee0c3c85fe9d7.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)

图为SpringMVC的一个较完整的流程图，实线表示SpringMVC框架提供的技术，不需要开发者实现，虚线表示需要开发者实现。



简要分析执行流程
  1.**DispatcherServlet表示前置控制器**，是整个SpringMVC的控制中心。用户发出请求，**DispatcherServlet接收请求并拦截请求**。我们假设请求的url为 : http://localhost:8080/SpringMVC/hello

**如上url拆分成三部分：**

- http://localhost:8080服务器域名
- SpringMVC部署在服务器上的web站点
- hello表示控制器

通过分析，如上url表示为：请求位于服务器**localhost:8080**上的**SpringMVC**站点的**hello**控制器。

2.HandlerMapping为处理器映射。DispatcherServlet调用HandlerMapping,HandlerMapping根据请求url查找Handler。

3.HandlerExecution表示具体的Handler,其主要作用是根据url查找控制器，如上url被查找控制器为：hello。

4.HandlerExecution将解析后的信息传递给DispatcherServlet,如解析控制器映射等。

5.HandlerAdapter表示处理器适配器，其按照特定的规则去执行Handler。

6.Handler让具体的Controller执行。

7.Controller将具体的执行信息返回给HandlerAdapter,如ModelAndView。

8.HandlerAdapter将视图逻辑名或模型传递给DispatcherServlet。

9.DispatcherServlet调用视图解析器(ViewResolver)来解析HandlerAdapter传递的逻辑视图名。

10.视图解析器将解析的逻辑视图名传给DispatcherServlet。

11.DispatcherServlet根据视图解析器解析的视图结果，调用具体的视图。

12.最终视图呈现给用户。



**可以将SpringMVC处理请求的过程分为三部分**

1. **第一步**，用户发起请求的时候它会经过一个前端控制器DispatcherServlet
2. DispatcherServlet 根据这个请求找到他的映射器HandlerMapping
3. 然后把HandlerExecution 映射器返回回来 DispatcherServlet。
4. **第二步**，DispatcherServlet 前端控制器根据这个映射器HandlerExecution 再去适配这个映射器HandlerAdapter ，适配到的这个映射器说白了就是一个Controller。
5. 由具体的Controller去执行，执行完后会返回一个具体的ModelAndView。
6. **第三步**，DispatcherServlet 前端控制器通过 ModelAndView 去配置具体的视图的解析器 ViewResolver，视图解析器返回给前端调用。



### 2.5、注解开发

1、新建一个Moudle添加web支持！
2、由于Maven可能存在资源过滤的问题，我们将配置完善

```xml
<build>
    <resources>
        <resource>
            <directory>src/main/java</directory>
            <includes>
                <include>**/*.properties</include>
                <include>**/*.xml</include>
            </includes>
            <filtering>false</filtering>
        </resource>
        <resource>
            <directory>src/main/resources</directory>
            <includes>
                <include>**/*.properties</include>
                <include>**/*.xml</include>
            </includes>
            <filtering>false</filtering>
        </resource>
    </resources>
</build>

```





3、在pom.xml文件引入相关的依赖：主要有Spring框架核心库、Spring MVC。

```xml
<dependencies>
    <!--单元测试-->
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.12</version>
    </dependency>
    <!--
        包含了：AOP，bean，context，core，web
    -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-webmvc</artifactId>
        <version>5.1.9.RELEASE</version>
    </dependency>
    <!--servlet依赖 -->
    <dependency>
        <groupId>javax.servlet</groupId>
        <artifactId>servlet-api</artifactId>
        <version>2.5</version>
    </dependency>
    <!--jsp 依赖-->
    <dependency>
        <groupId>javax.servlet.jsp</groupId>
        <artifactId>jsp-api</artifactId>
        <version>2.2</version>
    </dependency>
    <!--jstl依赖-->
    <dependency>
        <groupId>javax.servlet</groupId>
        <artifactId>jstl</artifactId>
        <version>1.2</version>
    </dependency>
</dependencies>

```



4、配置web.xml
注意点：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">

    <!--1.注册servlet-->
    <servlet>
        <servlet-name>SpringMVC</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <!--通过初始化参数指定SpringMVC配置文件的位置，进行关联-->
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>classpath:springmvc.xml</param-value>
        </init-param>
        <!-- 启动顺序，数字越小，启动越早 -->
        <load-on-startup>1</load-on-startup>
    </servlet>

    <!--所有请求都会被springmvc拦截 -->
    <servlet-mapping>
        <servlet-name>SpringMVC</servlet-name>
        <url-pattern>/</url-pattern>
    </servlet-mapping>

</web-app>

```



**/ 和 /* 的区别：**

`< url-pattern > / </ url-pattern > `**不会匹配到.jsp， 只针对我们编写的请求**；即：.jsp 不会进入spring的 DispatcherServlet类 。

`< url-pattern > /* </ url-pattern >` **会匹配 *.jsp，会出现返回 jsp视图 时再次进入spring的DispatcherServlet 类**，导致找不到对应的controller所以报404错。

1. 注意web.xml版本问题，要最新版！
2. 注册DispatcherServlet
3. 关联SpringMVC的配置文件
4. 启动级别为1
5. 映射路径为 / 【不要用/*，会404】



5、添加Spring MVC配置文件
  在resource目录下添加springmvc.xml配置文件，配置的形式与Spring容器配置基本类似，**为了支持基于注解的IOC，设置了自动扫描包的功能**，具体配置信息如下：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/mvc
        http://www.springframework.org/schema/mvc/spring-mvc.xsd
        http://www.springframework.org/schema/context
        http://www.springframework.org/schema/context/spring-context.xsd">

    <!-- 自动扫描包，让指定包下的注解生效,由IOC容器统一管理 -->
    <context:component-scan base-package="cn.bloghut.controller"/>
    <!-- 让Spring MVC不处理静态资源 -->
    <mvc:default-servlet-handler />
    <!--
    支持mvc注解驱动
        在spring中一般采用@RequestMapping注解来完成映射关系
        要想使@RequestMapping注解生效
        必须向上下文中注册DefaultAnnotationHandlerMapping
        和一个AnnotationMethodHandlerAdapter实例
        这两个实例分别在类级别和方法级别处理。
        而annotation-driven配置帮助我们自动完成上述两个实例的注入。
     -->
    <mvc:annotation-driven />

    <!-- 视图解析器 -->
    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver"
          id="internalResourceViewResolver">
        <!-- 前缀 -->
        <property name="prefix" value="/WEB-INF/jsp/" />
        <!-- 后缀 -->
        <property name="suffix" value=".jsp" />
    </bean>

</beans>

```

在视图解析器中我们把所有的视图都存放在/WEB-INF/目录下，这样可以保证视图安全，因为这个目录下的文件，客户端不能直接访问。

1. 让IOC的注解生效
2. 静态资源过滤 ：HTML . JS . CSS . 图片 ， 视频 …
3. MVC的注解驱动
4. 配置视图解析器



6、创建Controller

```java
package cn.bloghut.controller;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.servlet.ModelAndView;

@Controller
public class AnnotationController {

    @RequestMapping("hello")
    public ModelAndView hello(){
        ModelAndView model = new ModelAndView();
        //封装数据
        model.setViewName("test");

        model.addObject("msg","Hello Annotation");
        return model;//会被视图解析器处理
    }
}

```



- @Controller是为了让Spring IOC**容器初始化时自动扫描到**；
- @RequestMapping是为了**映射请求路径**，这里因为**类**与**方法**上都有映射所以访问时应该是/hello；
- 方法中声明**Model类型的参数是为了把Action中的数据带到视图中**；
- 方法返回的结果是视图的名称hello，加上配置文件中的**前后缀变成WEB-INF/jsp/test.jsp**。



7、创建视图层
  在WEB-INF/ jsp目录中创建test.jsp ， 视图可以直接取出并展示从Controller带回的信息

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>test</title>
</head>
<body>
    ${msg}
</body>
</html>

```



8、配置Tomcat运行
配置Tomcat ， 开启服务器 ， 访问 对应的请求路径！

![在这里插入图片描述](https://img-blog.csdnimg.cn/fa23ae78b88949e1baacf76fef198138.png#pic_center)



### 2.6小结

实现步骤其实非常的简单：

1. 新建一个web项目
2. 导入相关jar包
3. 编写web.xml , 注册DispatcherServlet
4. 编写springmvc配置文件
5. 接下来就是去创建对应的控制类 , controller
6. 最后完善前端视图和controller之间的对应
7. 测试运行调试.



**使用springMVC必须配置的三大件**：
1.处理器映射器、2.处理器适配器、3.视图解析器

通常，我们只需要手动配置视图解析器，而处理器映射器和处理器适配器只需要开启注解驱动即可，而省去了大段的xml配置



## 3、控制器

### 3.1控制器Controller

1. 控制器复杂提供访问应用程序的行为，通常通过接口定义或注解定义两种方法实现。
2. 控制器**负责解析用户的请求**并将其转换为一个模型。
3. 在Spring MVC中一个控制器类可以包含多个方法
4. 在Spring MVC中，对于Controller的配置方式有很多种



### 3.2实现Controller接口方式

Controller是一个接口，在`org.springframework.web.servlet.mvc`包下，接口中只有一个方法；

```java
@FunctionalInterface
public interface Controller {
   @Nullable
   ModelAndView handleRequest(HttpServletRequest request, HttpServletResponse response) throws Exception;
}

```



新建一个model，设置为web项目
配置web.xml文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">

    <!--1.配置DispatcherServlet-->
    <servlet>
        <servlet-name>dispatcherServlet</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>classpath:spirngmvc.xml</param-value>
        </init-param>

        <load-on-startup>1</load-on-startup>
    </servlet>
    <servlet-mapping>
        <servlet-name>dispatcherServlet</servlet-name>
        <url-pattern>/</url-pattern>
    </servlet-mapping>

</web-app>

```



配置springmvc配置文件，配置文件中注册请求的bean，**name对应请求路径**，class对应处理请求的类

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/mvc
        http://www.springframework.org/schema/mvc/spring-mvc.xsd
        http://www.springframework.org/schema/context
        http://www.springframework.org/schema/context/spring-context.xsd">

    <!-- 视图解析器 -->
    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver"
          id="internalResourceViewResolver">
        <!-- 前缀 -->
        <property name="prefix" value="/WEB-INF/jsp/" />
        <!-- 后缀 -->
        <property name="suffix" value=".jsp" />
    </bean>

    <bean name="/hello" class="cn.bloghut.controller.HelloController"/>

</beans>

```



编写controller类，继承Controller接口

```java
public class HelloController implements Controller {

    @Override
    public ModelAndView handleRequest(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse) throws Exception {
        ModelAndView model = new ModelAndView();
        model.setViewName("test");
        model.addObject("msg","Hello Controller");
        return model;
    }
}

```



编写跳转视图test.jsp

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>test</title>
</head>
<body>
${msg}
</body>
</html>

```



测试

![在这里插入图片描述](https://img-blog.csdnimg.cn/702c9b26bcac401297b1ca89cb9db26a.png#pic_center)



### 3.3使用注解@Controller方式

- @Controller注解类型用于声明Spring类的实例是一个控制器；
- Spring可以使用**扫描机制**来找到应用程序中所有**基于注解的控制器类**，为了保证Spring能找到你的控制器，**需要在配置文件中声明组件扫描**。

```xml
<!--开启包扫描-->
<context:component-scan base-package="cn.bloghut.controller"/>

```



增加一个ControllerTest2类，使用注解实现；

```java
@Controller
public class HelloController2 {

    @RequestMapping("hello2")
    public String hello2(Model model){

        model.addAttribute("msg","HelloController2");

        return "test";
    }
}

```



运行tomcat测试

![在这里插入图片描述](https://img-blog.csdnimg.cn/72473a9ead3c490dbf28ed9e1dd370b6.png#pic_center)

可以发现，我们的两个请求都可以指向一个视图，但是页面结果的结果是不一样的，从这里可以看出视图是被复用的，而**控制器**与**视图**之间是**弱偶合关系**。

注解方式是平时使用的最多的方式！



### 3.4@RequestMapping

- @RequestMapping注解**用于映射url到控制器类或一个特定的处理程序方法**。可用于**类**或**方法上**。用于类上，表示类中的所有响应请求的方法都是**以该地址作为父路径**。

只注解在方法上面

```java
@Controller
public class HelloController2 {

    @RequestMapping("t1")
    public String hello2(Model model){

        model.addAttribute("msg","HelloController2");

        return "test";
    }
}

```



访问路径：`http://localhost:8080 / t1`

同时注解类与方法

```java
@Controller
@RequestMapping("c3")
public class HelloController3 {

    @RequestMapping("t1")
    public String t1(Model model){

        model.addAttribute("msg","HelloController3");

        return "test";
    }
}

```

访问路径：`http://localhost:8080 /admin /t1` , 需要先指定类的路径再指定方法的路径；



## 4、RestFul风格

**概念**
  Restful就是一个资源定位及资源操作的风格。不是标准也不是协议，**只是一种风格**。基于这个风格设计的软件可以**更简洁，更有层次**，更易于实现缓存等机制。



**功能**

- 资源：互联网所有的事物都可以被抽象为资源
- 资源操作：使用**POST**、**DELETE**、**PUT**、**GET**，使用不同方法对资源进行操作。
- 分别对应 **添加**、 **删除**、**修改**、**查询**。



传统方式操作资源 ：通过不同的参数来实现不同的效果！方法单一，**post** 和 **get**

```http
http://127.0.0.1/item/queryItem.action?id=1 查询,GET
http://127.0.0.1/item/saveItem.action 新增,POST
http://127.0.0.1/item/updateItem.action 更新,POST
http://127.0.0.1/item/deleteItem.action?id=1 删除,GET或POST

```



使用RESTful操作资源 ：**可以通过不同的请求方式来实现不同的效果**！如下：**请求地址一样，但是功能可以不同**！

```http
http://127.0.0.1/item/1 查询,GET
http://127.0.0.1/item 新增,POST
http://127.0.0.1/item 更新,PUT
http://127.0.0.1/item/1 删除,DELETE

```



### 4.1测试

1.在新建一个类 RestFulController

```java
@Controller
public class RestFulController {

}

```



2.在Spring MVC中可以使用 @**PathVariable** 注解，**让方法参数的值对应绑定到一个URI模板变量上**。

```java
@Controller
public class RestFulController {

    @RequestMapping("/add/{a}/{b}")
    public String t1(@PathVariable int a,@PathVariable int b, Model model) {
        int res = a + b;
        model.addAttribute("msg", "结果为：" + res);
        return "test";
    }

}

```



3.测试请求查看下

![在这里插入图片描述](https://img-blog.csdnimg.cn/d6e6dc33a86b4cca9ec7529ed4c2be63.png#pic_center)



4.思考：使用路径变量的好处？

1. 使**路径变得更加简洁**；
2. **获得参数更加方便，框架会自动进行类型转换**。
3. 通过路径变量的类型可以约束访问参数，如果类型不一样，则访问不到对应的请求方法，如这里访问是的路径是/add/1/a，则路径与方法不匹配，而不会是参数转换失败。

![在这里插入图片描述](https://img-blog.csdnimg.cn/9e9029dfc32a4cbdae21e08a76285c8d.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_13,color_FFFFFF,t_70,g_se,x_16#pic_center)



5.修改下对应的参数类型，再次测试

```java
@Controller
public class RestFulController {
    @RequestMapping("/add/{a}/{b}")
    public String t1(@PathVariable int a,@PathVariable String b, Model model) {
        String res = a + b;
        model.addAttribute("msg", "结果为：" + res);
        return "test";
    }
}

```

![在这里插入图片描述](https://img-blog.csdnimg.cn/191bf12af1ef4ddc9e19aec017927548.png#pic_center)



### 4.2使用method属性指定请求类型

用于约束请求的类型，可以收窄请求范围。指定请求谓词的类型如GET, POST, HEAD, OPTIONS, PUT, PATCH, DELETE, TRACE等

1.增加一个方法

```java
/**
 * 删除方法
 * @param model
 * @return
 */
@RequestMapping(value = "hello",method = {RequestMethod.POST})
public String delete(Model model){
    model.addAttribute("msg","post");
    return "test";
}

```



2.我们使用浏览器地址栏进行访问默认是Get请求，会报错405：

3.如果将POST修改为GET则正常了；

```java
@RequestMapping(value = "hello",method = {RequestMethod.GET})
public String delete(Model model){
    model.addAttribute("msg","post");
    return "test";
}

```



**小结：**
  Spring MVC 的 **@RequestMapping** 注解能够处理 HTTP 请求的方法, 比如 GET, PUT, POST, DELETE 以及 PATCH。

所有的地址栏请求默认都会是 HTTP GET 类型的。
方法级别的注解变体有如下几个：组合注解

```java
@GetMapping
@PostMapping
@PutMapping
@DeleteMapping
@PatchMapping

```



@GetMapping 是一个**组合注解**，平时使用的会比较多！
它所扮演的是 @RequestMapping(method =RequestMethod.GET) 的一个快捷方式。



## 5、重定向和转发

### 5.1ModelAndView

设置ModelAndView对象 , 根据view的名称 , 和视图解析器跳到指定的页面 .
页面 : {视图解析器前缀} + viewName +{视图解析器后缀}

```xml
<!-- 视图解析器 -->
<bean class="org.springframework.web.servlet.view.InternalResourceViewResolver"
      id="internalResourceViewResolver">
    <!-- 前缀 -->
    <property name="prefix" value="/WEB-INF/jsp/" />
    <!-- 后缀 -->
    <property name="suffix" value=".jsp" />
</bean>

```



对应的controller类

```java
@Override
public ModelAndView handleRequest(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse) throws Exception {
    ModelAndView model = new ModelAndView();
    model.setViewName("test");
    model.addObject("msg","Hello Controller");
    return model;
}

```



### 5.2ServletAPI

通过设置ServletAPI , 不需要视图解析器 .

1. 通过HttpServletResponse进行**输出**
2. 通过HttpServletResponse实现**重定向**
3. 通过HttpServletResponse实现**转发**

```java
/**
 * 往页面输出内容
 * @param req
 * @param rsp
 * @throws IOException
 */
@RequestMapping("/result/t1")
public void test1(HttpServletRequest req, HttpServletResponse rsp) throws IOException {
    rsp.getWriter().println("Hello,Spring BY servlet API");
}

/**
 * 演示重定向
 * @param req
 * @param rsp
 * @throws IOException
 */
@RequestMapping("/result/t2")
public void test2(HttpServletRequest req, HttpServletResponse rsp) throws IOException {
    rsp.sendRedirect("/index.jsp");
}

/**
 * 演示请求转发
 * @param req
 * @param rsp
 * @throws Exception
 */
@RequestMapping("/result/t3")
public void test3(HttpServletRequest req, HttpServletResponse rsp) throws Exception {
    //转发
    req.setAttribute("msg","/result/t3");
    req.getRequestDispatcher("/WEB-INF/jsp/test.jsp").forward(req,rsp);
}

```



### 5.3SpringMVC

通过SpringMVC来实现转发和重定向 - **无需视图解析器**；
测试前，需要将视图解析器注释掉

```java
@RequestMapping("/rsm/t1")
public String test1(){
    //转发
    return "/index.jsp";
}

@RequestMapping("/rsm/t2")
public String test2(){
    //转发二
    return "forward:/index.jsp";
}

@RequestMapping("/rsm/t3")
public String test3(){
    //重定向
    return "redirect:/index.jsp";
}

```



通过SpringMVC来实现转发和重定向 - 有视图解析器；
  **重定向** , 不需要视图解析器 , 本质就是**重新请求一个新地方嘛** , 所以**注意路径问题.**
可以重定向到另外一个请求实现 .



## 6、SpringMVC数据处理

### 6.1处理提交数据

1、提交的域名称和处理方法的参数名一致
提交数据 : `http://localhost:8080/hello?name=xianyan`

```java
@RequestMapping("t1")
public String t1(String name, Model model, HttpSession session){
    //localhost:8080/user/t1?name=xxx
    //1.接收前端参数
    System.out.println("接收到前端的参数为："+name);
    //2.将返回的结果传递给前端
    model.addAttribute("msg",name);
    //3.视图跳转
    return "test";
}

```



2、提交的域名称和处理方法的参数名不一致
提交数据 : `http://localhost:8080/hello?username=kuangshen`
处理方法 :

```java
@RequestMapping("t1")
public String t1(@RequestParam("username") String name, Model model, HttpSession session){
    //localhost:8080/user/t1?name=xxx
    //1.接收前端参数
    System.out.println("接收到前端的参数为："+name);
    //2.将返回的结果传递给前端
    model.addAttribute("msg",name);
    //3.视图跳转
    return "test";
}

```



3、提交的是一个对象
要求提交的**表单域**和**对象的属性名**一致 , 参数使用对象即可
1、实体类

```java
@Data
public class User {
    private int id;
    private String name;
    private int age;
}

```



2、提交数据的表单 :

```jsp
<form action="/user/t2" method="post">
    id：<input name="id" type="text"><br>
    姓名：<input name="name" type="text"><br>
  年龄：<input name="age" type="text"><br>
  <input type="submit">
</form>

```



3、处理方法 :

```java
@PostMapping("t2")
public String t2(User user){
    System.out.println(user);
    return "test";
}

```



后台输出 :

```json
User(id=1, name=闲言, age=18)

```



说明：如果使用对象的话，前端传递的参数名和对象名必须一致，否则就是null。



### 6.2数据显示到前端

第一种 : 通过**ModelAndView**

```java
public ModelAndView handleRequest(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse) throws Exception {
    //返回一个模型视图对象
    ModelAndView mv = new ModelAndView();
    mv.addObject("msg","ControllerTest1");
    mv.setViewName("test");
    return mv;
}

```



第二种 : 通过**ModelMap**

```java
@RequestMapping("/hello")
public String hello(@RequestParam("username") String name, ModelMap model){
    //封装要显示到视图中的数据
    //相当于req.setAttribute("name",name);
    model.addAttribute("name",name);
    System.out.println(name);
    return "hello";
}

```



第三种 : 通过**Model**

```java
@RequestMapping("/ct2/hello")
public String hello(@RequestParam("username") String name, Model model){
    //封装要显示到视图中的数据
    //相当于req.setAttribute("name",name);
    model.addAttribute("msg",name);
    System.out.println(name);
    return "test";
}

```



区别
就对于新手而言简单来说使用区别就是：

1. Model 只有寥寥几个方法只适合用于储存数据，**简化了新手对于Model对象的操作和理解**；

2. **ModelMap 继承了 LinkedMap** ，**除了实现了自身的一些方法，同样的继承 LinkedMap 的方法和特性；**
3. ModelAndView 可以在**储存数据的同时**，可以进行**设置返回的逻辑视图**，进行**控制展示层的跳转**



## 7、乱码问题

1、编写一个提交的表单

```jsp
<form action="/user/t2" method="post">
    id：<input name="id" type="text"><br>
    姓名：<input name="name" type="text"><br>
  年龄：<input name="age" type="text"><br>
  <input type="submit">
</form>	

```



2、后台编写对应的处理类

```java
@Controller
public class Encoding {
    @PostMapping("/e/t1")
    public String test1(User user,Model model){
        model.addAttribute("msg",user);
        return "test";
    }
}

```



3、输入中文测试，发现乱码

以前乱码问题通过过滤器解决 , 而SpringMVC给我们提供了一个过滤器 , 可以在web.xml中配置

修改了xml文件需要重启服务器！

```xml
<filter>
    <filter-name>encoding</filter-name>
    <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
    <init-param>
        <param-name>encoding</param-name>
        <param-value>utf-8</param-value>
    </init-param>
</filter>
<filter-mapping>
    <filter-name>encoding</filter-name>
    <url-pattern>/*</url-pattern>
</filter-mapping>

```





## 8、JSON

**前后端分离时代：**

后端部署后端，提供接口，提供数据。
        json
前端独立部署，负责渲染后端的数据。



**什么是JSON？**

1. JSON(JavaScript Object Notation, JS 对象标记) 是一种轻量级的数据交换格式，目前使用特别广泛。
2. 采用完全独立于编程语言的文本格式来存储和表示数据。
3. 简洁和清晰的层次结构使得 JSON 成为理想的数据交换语言。
4. 易于人阅读和编写，同时也易于机器解析和生成，并有效地提升网络传输效率。



在 JavaScript 语言中，**一切都是对象**。因此，任何JavaScript 支持的类型都可以通过 JSON 来表示，例如字符串、数字、对象、数组等。看看他的要求和语法格式：

- 对象表示为**键值对**，数据由**逗号分隔**
- **花括号**保存**对象**
- **方括号**保存**数组**



JSON 键值对是用来保存 JavaScript 对象的一种方式，和 JavaScript 对象的写法也大同小异，键/值对组合中的键名写在前面并**用双引号 “” 包裹，使用冒号 : 分隔，然后紧接着值：**

```json
{"name": "xy"}
{"age": "18"}
{"sex": "男"}

```



JSON 是 JavaScript 对象的**字符串表示法，它使用文本表示一个 JS 对象的信息，本质是一个字符串**。

```json
var obj = {a: 'Hello', b: 'World'}; //这是一个对象，注意键名也是可以使用引号包裹的
var json = '{"a": "Hello", "b": "World"}'; //这是一个 JSON 字符串，本质是一个字符串

```



**JSON 和 JavaScript 对象互转**
  要实现从JSON字符串转换为JavaScript 对象，使用 **JSON.parse()** 方法：

```js
//将json对象转换为javaScript对象
var obj = JSON.parse(str);
console.log(obj);

```



要实现从JavaScript 对象转换为JSON字符串，使用 **JSON.stringify()** 方法：

```js
//将js对象转换为JSON对象;
var str = JSON.stringify(user);
console.log(str);

```

![在这里插入图片描述](https://img-blog.csdnimg.cn/6802a875b48f4713b4b1e1044913db59.png#pic_center)





### 8.1返回JSON数据 Jackson

1. **Jackson**应该是目前比较好的json解析工具了

2. 当然工具不止这一个，比如还有阿里巴巴的 fastjson 等等。

3. 我们这里使用Jackson，使用它需要导入它的jar包；

```xml
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-databind</artifactId>
    <version>2.9.8</version>
</dependency>

```



配置SpringMVC需要的配置
web.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">
    <!--前端控制器-->
    <servlet>
        <servlet-name>dispatcherServlet</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>classpath:spirngmvc.xml</param-value>
        </init-param>

        <load-on-startup>1</load-on-startup>
    </servlet>
    <servlet-mapping>
        <servlet-name>dispatcherServlet</servlet-name>
        <url-pattern>/</url-pattern>
    </servlet-mapping>
    
    <!--编码过滤器-->
    <filter>
        <filter-name>encoding</filter-name>
        <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
        <init-param>
            <param-name>encoding</param-name>
            <param-value>UTF-8</param-value>
        </init-param>
    </filter>
    <filter-mapping>
        <filter-name>encoding</filter-name>
        <url-pattern>/*</url-pattern>
    </filter-mapping>

</web-app>

```



springmvc-servlet.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/mvc
        http://www.springframework.org/schema/mvc/spring-mvc.xsd
        http://www.springframework.org/schema/context
        http://www.springframework.org/schema/context/spring-context.xsd">
    <!--开启包扫描-->
    <context:component-scan base-package="cn.bloghut.controller"/>
    <!--支持注解-->
    <mvc:annotation-driven/>
    <!--过滤静态资源-->
    <mvc:default-servlet-handler/>
    <!-- 视图解析器 -->
    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver"
          id="internalResourceViewResolver">
        <!-- 前缀 -->
        <property name="prefix" value="/WEB-INF/jsp/" />
        <!-- 后缀 -->
        <property name="suffix" value=".jsp" />
    </bean>
</beans>

```

这里我们需要两个新东西，一个是**@ResponseBody**，一个是**ObjectMapper对象**，我们看下具体的用法
编写一个Controller；

```java
@Controller
public class JSONController {
    /**
     * 加了  @ResponseBody 注解之后，它就不会走视图解析器，会直接返回一个字符串
     * @return
     */
    @ResponseBody
    @RequestMapping(value = "j1",produces = "application/json;charset=utf-8")
    public String json1() throws JsonProcessingException {
        //创建一个对象
        User user = new User(1,"闲言",18);
        //jackson，ObjectMapper
        ObjectMapper objectMapper = new ObjectMapper();
        String json = objectMapper.writeValueAsString(user);
        return json;
    }
}

```



配置Tomcat ， 启动测试一下！

```http
http://localhost:8080/j1

```

![在这里插入图片描述](https://img-blog.csdnimg.cn/78e7370b7ff24099abcbca4ce8527d4d.png#pic_center)

发现出现了乱码问题，我们需要设置一下他的编码格式为**utf-8**，以及它返回的类型；
通过**@RequestMaping**的**produces属性**来实现，修改下代码

```java
@RequestMapping(value = "j1",produces = "application/json;charset=utf-8")

```

![在这里插入图片描述](https://img-blog.csdnimg.cn/fdea44495c764c5eac1b5b578ec84cb5.png#pic_center)



**【注意：使用json记得处理乱码问题】**

代码优化

**乱码统一解决**

1. 上一种方法比较麻烦，如果项目中有许多请求则每一个都要添加，可以通过Spring配置统一指定，这样就不用每次都去处理了！
2. 我们可以在springmvc的配置文件上添加一段消息**StringHttpMessageConverter**转换配置！

```xml
<mvc:annotation-driven>
    <mvc:message-converters register-defaults="true">
        <bean class="org.springframework.http.converter.StringHttpMessageConverter">
            <constructor-arg value="UTF-8"/>
        </bean>
        <bean class="org.springframework.http.converter.json.MappingJackson2HttpMessageConverter">
            <property name="objectMapper">
                <bean class="org.springframework.http.converter.json.Jackson2ObjectMapperFactoryBean">
                    <property name="failOnEmptyBeans" value="false"/>
                </bean>
            </property>
        </bean>
    </mvc:message-converters>
</mvc:annotation-driven>

```



测试集合输出
增加一个新的方法

```java
@RequestMapping(value = "j2")
public String json2() throws JsonProcessingException {
    //创建一个对象
    List<User> list = new ArrayList<>();
    list.add(new User(1,"闲言1",18));
    list.add(new User(2,"闲言2",18));
    list.add(new User(3,"闲言3",18));
    list.add(new User(4,"闲言4",18));
    //jackson，ObjectMapper
    ObjectMapper objectMapper = new ObjectMapper();

    //将我们的对象解析成为json格式
    String json = objectMapper.writeValueAsString(list);
    return json;
}

```



运行结果 :

![在这里插入图片描述](https://img-blog.csdnimg.cn/ecaaeb3d54344749a0aedc280682674d.png#pic_center)



输出时间对象
增加一个新的方法

```java
@RequestMapping(value = "j3")
public String json3() throws JsonProcessingException {
    //jackson，ObjectMapper
    ObjectMapper objectMapper = new ObjectMapper();
    Date date = new Date();

    //ObjectMapper，时间解析后的格式为：Timestamp
    String json = objectMapper.writeValueAsString(date);
    return json;
}

```

运行结果 :

![img](https://img-blog.csdnimg.cn/ab83bb0587774319aaee134a759df8ae.png#pic_center)



默认日期格式会变成一个数字，是1970年1月1日到当前日期的毫秒数！
Jackson 默认是会把时间转成**timestamps**形式

解决方案：取消timestamps形式 ， 自定义时间格式

```java
@RequestMapping(value = "j4")
public String json4() throws JsonProcessingException {
    //jackson，ObjectMapper
    ObjectMapper objectMapper = new ObjectMapper();
    Date date = new Date();
    //自定义日期格式对象
    SimpleDateFormat  sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");

    //ObjectMapper，时间解析后的格式为：Timestamp
    String json = objectMapper.writeValueAsString(sdf.format(date));
    return json;
}

```



运行结果 :

![在这里插入图片描述](https://img-blog.csdnimg.cn/8a0171bed4a043fe93e53db784a9f534.png#pic_center)



### 8.2返回JSON数据FastJson

**fastjson.jar是阿里开发的一款专门用于Java开发的包**，可以**方便的实现json对象与JavaBean对象的转换，实现JavaBean对象与json字符串的转换**，**实现json对象与json字符串的转换**。实现json的转换方法很多，最后的实现结果都是一样的。

fastjson 的 pom依赖！

```xml
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>fastjson</artifactId>
    <version>1.2.67</version>
</dependency>

```



astjson 三个主要的类：

1. **JSONObject 代表 json 对象**
2. JSONObject实现了Map接口, 猜想 JSONObject底层操作是由Map实现的。

3. JSONObject对应json对象，通过各种形式的get()方法可以获取json对象中的数据，也可利用诸如size()，isEmpty()等方法获取"键：值"对的个数和判断是否为空。其本质是通过实现Map接口并调用接口中的方法完成的。

4. JSONArray 代表 **json 对象数组**

5. 内部是有List接口中的方法来完成操作的。

6. **JSON代表 JSONObject和JSONArray的转化**



**JSON类源码分析与使用**
  仔细观察这些方法，主要是实现json对象，json对象数组，javabean对象，json字符串之间的相互转化。

```java
@RequestMapping(value = "j5")
public String json5() throws JsonProcessingException {
    //创建一个对象
    User user1 = new User(1,"闲言1号", 18);
    User user2 = new User(2,"闲言2号", 19);
    User user3 = new User(3,"闲言3号", 20);
    User user4 = new User(4,"闲言4号", 21);
    List<User> list = new ArrayList<User>();
    list.add(user1);
    list.add(user2);
    list.add(user3);
    list.add(user4);
    System.out.println("*******Java对象 转 JSON字符串*******");
    String str1 = JSON.toJSONString(list);
    System.out.println("JSON.toJSONString(list)==>"+str1);
    String str2 = JSON.toJSONString(user1);
    System.out.println("JSON.toJSONString(user1)==>"+str2);

    System.out.println("\n****** JSON字符串 转 Java对象*******");
    User jp_user1=JSON.parseObject(str2,User.class);
    System.out.println("JSON.parseObject(str2,User.class)==>"+jp_user1);

    System.out.println("\n****** Java对象 转 JSON对象 ******");
    JSONObject jsonObject1 = (JSONObject) JSON.toJSON(user2);
    System.out.println("(JSONObject) JSON.toJSON(user2)==>"+jsonObject1.getString("name"));

    System.out.println("\n****** JSON对象 转 Java对象 ******");
    User to_java_user = JSON.toJavaObject(jsonObject1, User.class);
    System.out.println("JSON.toJavaObject(jsonObject1, User.class)==>"+to_java_user);

    return JSON.toJSONString(list);
}

```



运行结果 :

![在这里插入图片描述](https://img-blog.csdnimg.cn/50d67e1cd6a645f5a3bde8f50f1eab6e.png#pic_center)



## 9、Ajax研究

### 9.1简介

1. AJAX = Asynchronous JavaScript and XML（异步的 JavaScript 和 XML）。
2. AJAX 是一种在无需重新加载整个网页的情况下，能够更新部分网页的技术。
3. Ajax 不是一种新的编程语言，而是一种用于创建更好更快以及交互性更强的Web应用程序的技术。
4. 在 2005 年，Google 通过其 Google Suggest 使 AJAX 变得流行起来。Google Suggest能够自动帮你完成搜索单词。
5. Google Suggest 使用 AJAX 创造出动态性极强的 web 界面：当您在谷歌的搜索框输入关键字时，JavaScript 会把这些字符发送到服务器，然后服务器会返回一个搜索建议的列表。
6. 就和国内百度的搜索框一样!
7. 传统的网页(即不用ajax技术的网页)，想要更新内容或者提交一个表单，都需要重新加载整个网页。
8. 使用ajax技术的网页，通过在后台服务器进行少量的数据交换，就可以实现异步局部更新。
9. 使用Ajax，用户可以创建接近本地桌面应用的直接、高可用、更丰富、更动态的Web用户界面。



### 9.2伪造Ajax

我们可以使用前端的一个标签来伪造一个ajax的样子。iframe标签
1、新建一个module， 导入web支持！
2、编写一个 ajax-frame.html 使用 iframe 测试，感受下效果

```jsp
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title>title</title>
</head>
<body>

<script type="text/javascript">
    window.onload = function(){
        var myDate = new Date();
        document.getElementById('currentTime').innerText = myDate.getTime();
    };

    function LoadPage(){
        var targetUrl =  document.getElementById('url').value;
        console.log(targetUrl);
        document.getElementById("iframePosition").src = targetUrl;
    }

</script>

<div>
    <p>请输入要加载的地址：<span id="currentTime"></span></p>
    <p>
        <input id="url" type="text" value="https://blog.csdn.net/qq_42025798?spm=1000.2115.3001.5343"/>
        <input type="button" value="提交" onclick="LoadPage()">
    </p>
</div>

<div>
    <h3>加载页面位置：</h3>
    <iframe id="iframePosition" style="width: 100%;height: 500px;"></iframe>
</div>

</body>
</html>

```



3、使用IDEA开浏览器测试一下！
**利用AJAX可以做：**

- 注册时，输入用户名自动**检测用户是否已经存在**。
- 登陆时，提示用户名密码错误
- 删除数据行时，将行ID发送到后台，后台在数据库中删除，数据库删除成功后，在页面DOM中将数据行也删除。
- …等等

**JQeury 是一个库，js 的大量函数**



### 9.3jQuery.ajax

1. Ajax的核心是XMLHttpRequest对象(XHR)。XHR为向服务器发送请求和解析服务器响应提供了接口。能够以异步方式从服务器获取新数据。
2. jQuery 提供多个与 AJAX 有关的方法。
3. 通过 jQuery AJAX 方法，您能够使用 HTTP Get 和 HTTP Post 从远程服务器上请求文本、HTML、XML 或 JSON – 同时您能够把这些外部数据直接载入网页的被选元素中。
4. jQuery 不是生产者，而是大自然搬运工。
5. jQuery **Ajax本质就是 XMLHttpRequest，对他进行了封装，方便调用！**

```javascript
jQuery.ajax(...)
      部分参数：
            url：请求地址
            type：请求方式，GET、POST（1.9.0之后用method）
        headers：请求头
            data：要发送的数据
    contentType：即将发送信息至服务器的内容编码类型(默认: "application/x-www-form-urlencoded; charset=UTF-8")
          async：是否异步
        timeout：设置请求超时时间（毫秒）
      beforeSend：发送请求前执行的函数(全局)
        complete：完成之后执行的回调函数(全局)
        success：成功之后执行的回调函数(全局)
          error：失败之后执行的回调函数(全局)
        accepts：通过请求头发送给服务器，告诉服务器当前客户端可接受的数据类型
        dataType：将服务器端返回的数据转换成指定类型
          "xml": 将服务器端返回的内容转换成xml格式
          "text": 将服务器端返回的内容转换成普通文本格式
          "html": 将服务器端返回的内容转换成普通文本格式，在插入DOM中时，如果包含JavaScript标签，则会尝试去执行。
        "script": 尝试将返回值当作JavaScript去执行，然后再将服务器端返回的内容转换成普通文本格式
          "json": 将服务器端返回的内容转换成相应的JavaScript对象
        "jsonp": JSONP 格式使用 JSONP 形式调用函数时，如 "myurl?callback=?" jQuery 将自动替换 ? 为正确的函数名，以执行回调函数

```



### 9.4使用最原始的HttpServletResponse处理

1、配置**web.xml** 和 **springmvc**的配置文件【记得静态资源过滤和注解驱动配置上】

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">
    <!--前端控制器-->
    <servlet>
        <servlet-name>dispatcherServlet</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>classpath:applicationContext.xml</param-value>
        </init-param>
        <load-on-startup>1</load-on-startup>
    </servlet>
    <servlet-mapping>
        <servlet-name>dispatcherServlet</servlet-name>
        <url-pattern>/</url-pattern>
    </servlet-mapping>
    <!--编码过滤器-->
    <filter>
        <filter-name>encodingFilter</filter-name>
        <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
        <init-param>
            <param-name>encodingUTF-8</param-name>
            <param-value></param-value>
        </init-param>
    </filter>
    <filter-mapping>
        <filter-name>encodingFilter</filter-name>
        <url-pattern>/*</url-pattern>
    </filter-mapping>
</web-app>

```

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/mvc
        http://www.springframework.org/schema/mvc/spring-mvc.xsd
        http://www.springframework.org/schema/context
        http://www.springframework.org/schema/context/spring-context.xsd">

    <!--开启包扫描-->
    <context:component-scan base-package="cn.bloghut.controller"/>
    <!--支持注解-->
    <mvc:annotation-driven/>
    <!--过滤静态资源-->
    <mvc:default-servlet-handler/>

    <!-- 视图解析器 -->
    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver"
          id="internalResourceViewResolver">
        <!-- 前缀 -->
        <property name="prefix" value="/WEB-INF/jsp/" />
        <!-- 后缀 -->
        <property name="suffix" value=".jsp" />
    </bean>
</beans>

```



2、编写一个Controller

```java
@RequestMapping("a1")
public void a1(String name , HttpServletResponse response) throws Exception{
    if ("admin".equals(name)) {
        response.getWriter().print("true");
    } else {
        response.getWriter().print("false");
    }
}

```



3、导入jquery ， 可以使用在线的CDN ， 也可以下载导入

```javascript
<script src="https://code.jquery.com/jquery-3.1.1.min.js"></script>
<script src="${pageContext.request.contextPath}/statics/js/jquery-3.1.1.min.js"></script>

```



4、编写index.jsp测试

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>$Title$</title>
    <script src="https://code.jquery.com/jquery-3.1.1.min.js"></script>
<%--    <script src="${pageContext.request.contextPath}/statics/js/jquery-3.1.1.min.js"></script>--%>
    <script>
        function a1(){
            $.post({
                url:"${pageContext.request.contextPath}/a1",
                data:{'name':$("#txtName").val()},
                success:function (data,status) {
                    alert(data);
                    alert(status);
                }
            });
        }
    </script>
</head>
<body>

<%--onblur：失去焦点触发事件--%>
用户名:<input type="text" id="txtName" onblur="a1()"/>

```



5、启动tomcat测试！打开浏览器的控制台，当我们鼠标离开输入框的时候，可以看到发出了一个ajax的请求！是后台返回给我们的结果！

![在这里插入图片描述](https://img-blog.csdnimg.cn/0759653bd5334a10bc12117bd5b0ac97.png#pic_center)

![在这里插入图片描述](https://img-blog.csdnimg.cn/d2d5c0cb8bb2455b9ceb6557ff3a14c3.png#pic_center)



### 9.5Ajax异步加载数据

实体类user

```java
@Data
@AllArgsConstructor
@NoArgsConstructor
public class User {
    private int id;
    private String name;
    private int age;
}

```



我们来获取一个集合对象，展示到前端页面

```java
@RequestMapping("a2")
public List<User> a2(){
    List<User> users = new ArrayList<>();
    users.add(new User(1,"闲言1号",18));
    users.add(new User(2,"闲言2号",19));
    users.add(new User(3,"闲言3号",20));
    users.add(new User(4,"闲言4号",21));
    return users; //由于@RestController注解，将list转成json格式返回
}

```



前端页面

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
<input type="button" id="btn" value="获取数据"/>
<table width="80%" align="center">
    <tr>
        <td>id</td>
        <td>姓名</td>
        <td>年龄</td>
    </tr>
    <tbody id="content">
    </tbody>
</table>

<script src="https://code.jquery.com/jquery-3.1.1.min.js"></script>
<script>

    $(function () {
        $("#btn").click(function () {
            $.post("${pageContext.request.contextPath}/a2",function (data) {
                console.log(data)
                var html="";
                for (var i = 0; i <data.length ; i++) {
                    html+= "<tr>" +
                        "<td>" + data[i].id + "</td>" +
                        "<td>" + data[i].name + "</td>" +
                        "<td>" + data[i].age + "</td>" +
                        "</tr>"
                }
                $("#content").html(html);
            });
        })
    })
</script>
</body>
</html>

```



启动tomcat测试！

![在这里插入图片描述](https://img-blog.csdnimg.cn/cf3e0d5d8b104f27a63c6540e7326e4f.png#pic_center)





### 9.6注册提示效果

思考一下我们平时注册时候，输入框后面的实时提示怎么做到的；
写一个Controller

```java
@RequestMapping("/a3")
public String ajax3(String name,String pwd){
    String msg = "";
    //模拟数据库中存在数据
    if (name!=null){
        if ("admin".equals(name)){
            msg = "OK";
        }else {
            msg = "用户名输入错误";
        }
    }
    if (pwd!=null){
        if ("123456".equals(pwd)){
            msg = "OK";
        }else {
            msg = "密码输入有误";
        }
    }
    return msg; //由于@RestController注解，将msg转成json格式返回
}

```



前端页面 login.jsp
测试一下效果

![在这里插入图片描述](https://img-blog.csdnimg.cn/57df75b663894cec8a29ee1e6e129f37.png#pic_center)



## 10、拦截器

### 10.1概述

SpringMVC的处理器拦截器类似于Servlet开发中的**过滤器Filter**,用于**对处理器进行预处理和后处理**。开发者可以自己定义一些拦截器来实现特定的功能。

过滤器与拦截器的区别：**拦截器是AOP思想的具体应用。**



**过滤器**

- servlet规范中的一部分，**任何java web工程都可以使用**
- 在url-pattern中配置了/*之后，可以对**所有要访问的资源进行拦截**



**拦截器**

- 拦截器是SpringMVC框架自己的，只有**使用了SpringMVC框架的工程才能使用**
- 拦截器只会拦截访问的控制器方法（请求）， 如果访问的是**jsp/html/css/image/js**是不会进行拦截的



### 10.2自定义拦截器

那如何实现拦截器呢？
想要自定义拦截器，必须实现 HandlerInterceptor 接口。
1、新建一个Moudule ， springmvc-07-Interceptor ， 添加web支持
2、配置web.xml 和 springmvc-servlet.xml 文件
3、编写一个拦截器

```java
public class MyInterceptor implements HandlerInterceptor {
    /**
     * 预处理回调方法
     * @param request
     * @param response
     * @param handler
     * @return
     * @throws Exception
     */
    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        System.out.println("====================================处理前====================================");

        return true;
    }
    /**
     * 后处理回调方法
     * @param request
     * @param response
     * @param handler
     * @param modelAndView
     * @throws Exception
     */
    @Override
    public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView) throws Exception {
        System.out.println("====================================处理后====================================");
    }
    /**
     * 整个请求处理完毕回调方法
     * @param request
     * @param response
     * @param handler
     * @param ex
     * @throws Exception
     */
    @Override
    public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) throws Exception {
        System.out.println("====================================清理====================================");
    }
}

```



4、在springmvc的配置文件中配置拦截器

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/mvc
        http://www.springframework.org/schema/mvc/spring-mvc.xsd
        http://www.springframework.org/schema/context
        http://www.springframework.org/schema/context/spring-context.xsd">
    <!--开启注解扫描-->
    <context:component-scan base-package="cn.bloghut.controller"/>
    <!--对注解的支持-->
    <mvc:annotation-driven/>
    <!--过滤静态资源-->
    <mvc:default-servlet-handler/>
    <!--配置视图解析器-->
    <bean id="internalResourceViewResolver" class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <!--前缀-->
        <property name="prefix" value="/WEB-INF/jsp/"/>
        <!--后缀-->
        <property name="suffix" value=".jsp"/>
    </bean>
    <!--过滤静态资源-->
    <mvc:annotation-driven>
        <mvc:message-converters register-defaults="true">
            <bean class="org.springframework.http.converter.StringHttpMessageConverter">
                <constructor-arg value="UTF-8"/>
            </bean>
            <bean class="org.springframework.http.converter.json.MappingJackson2HttpMessageConverter">
                <property name="objectMapper">
                    <bean class="org.springframework.http.converter.json.Jackson2ObjectMapperFactoryBean">
                        <property name="failOnEmptyBeans" value="false"/>
                    </bean>
                </property>
            </bean>
        </mvc:message-converters>
    </mvc:annotation-driven>
    <!--配置拦截器-->
    <mvc:interceptors>
        <mvc:interceptor>
            <!--/** 包括路径及其子路径-->
            <!--/admin/* 拦截的是/admin/add等等这种 , /admin/add/user不会被拦截-->
            <!--/admin/** 拦截的是/admin/下的所有-->
            <!--拦截所有路径-->
            <mvc:mapping path="/**"/>
            <!--注入拦截器-->
            <bean class="cn.bloghut.interceptor.MyInterceptor"/>
        </mvc:interceptor>
    </mvc:interceptors>
</beans>

```



5、编写一个Controller，接收请求

```java
@RequestMapping("t1")
public String t1() {
    System.out.println("t1 请求执行了");
    return "t1";
}

```



6、前端 index.jsp

```http
http://localhost:8080/t1

```



7、启动tomcat 测试一下！



### 10.3验证用户是否登录 (认证用户)

1、有一个登陆页面，需要写一个controller访问页面。
2、登陆页面有一提交表单的动作。需要在controller中处理。判断用户名密码是否正确。如果正确，向session中写入用户信息。返回登陆成功。
3、拦截用户请求，判断用户是否登陆。如果用户已经登陆。放行， 如果用户未登陆，跳转到登陆页面

1、编写一个登陆页面 login.jsp

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>用户登录</title>
</head>
<body>
<p>${msg}</p>
    <form action="login" method="post">
        用户名<input type="text" name="username"><br>
        密码<input type="password" name="pwd"><br>
        <input type="submit">
    </form>

</body>
</html>

```



2、编写一个Controller处理请求

```java
@Controller
@RequestMapping("user")
public class LoginController {
    /**
     * 执行登录逻辑
     * @param user
     * @param request
     * @return
     */
    @PostMapping("login")
    public ModelAndView login(User user, HttpServletRequest request){
        ModelAndView model = new ModelAndView();
        /**
         * 如果用户名和密码正确，将当前用户存入到session中
         * 跳转到success页面
         */
        if ("admin".equals(user.getUsername()) && "123".equals(user.getPwd())){
            request.getSession().setAttribute("user",user);
            model.setViewName("main");
        }else {
            model.addObject("msg","用户名或密码错误");
            model.setViewName("login");
        }
        return model;
    }
    /**
     * 返回登录界面
     * @return
     */
    @RequestMapping("jumplogin")
    public String jumplogin(){
        System.out.println("获取登录界面方法执行了jumplogin==");
        return "login";
    }
    /**
     * 注销
     * @param request
     * @return
     */
    @RequestMapping("logout")
    public String logout(HttpServletRequest request){
        request.getSession().removeAttribute("user");
        return "login";
    }
}

```



3、编写一个登陆成功的页面 main.jsp

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>登录成功</title>
</head>
<body>
    <h1>SUCCESS</h1>
<h1>${user}</h1>
<hr>
<a href="${pageContext.servletContext.contextPath}/user/logout">注销</a>
</body>
</html>

```



4、在 index 页面上测试跳转！启动Tomcat 测试，未登录也可以进入主页！

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
  <title>$Title$</title>
</head>
<body>
<h1>首页</h1>
<hr>
<%--登录--%>
<a href="${pageContext.request.contextPath}/user/jumplogin">登录</a>
<a href="${pageContext.request.contextPath}/user/success">成功页面</a>
</body>
</html>

```



5、编写用户登录拦截器

```java
public class LoginInterceptor implements HandlerInterceptor {
    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        String uri = request.getRequestURI();
        System.out.println("========请求的路径为=========》"+uri);
        //如果是登录请求和退出登录请求就放行
        if (uri.contains("login") || uri.contains("logout")){
            return true;
        }
        //判断什么情况下放行
        Object user = request.getSession().getAttribute("user");
        if (user != null) {
            return true;
        }

        //转发到登录页面
        request.getRequestDispatcher("/WEB-INF/jsp/login.jsp").forward(request,response);
        return false;
    }

    @Override
    public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView) throws Exception {
    }

    @Override
    public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) throws Exception {
    }
}

```



6、在Springmvc的配置文件中注册拦截器

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/mvc
        http://www.springframework.org/schema/mvc/spring-mvc.xsd
        http://www.springframework.org/schema/context
        http://www.springframework.org/schema/context/spring-context.xsd">
    <!--开启包扫描-->
    <context:component-scan base-package="cn.bloghut.controller"/>
    <!--开启注解支持-->
    <mvc:annotation-driven />
    <!--过滤静态资源-->
    <mvc:default-servlet-handler />
    <!--配置视图解析器-->
    <bean id="internalResourceViewResolver" class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <!--前缀-->
        <property name="prefix" value="/WEB-INF/jsp/"/>
        <!--后缀-->
        <property name="suffix" value=".jsp"/>
    </bean>
    <!--配置拦截器-->
    <mvc:interceptors>
        <mvc:interceptor>
            <!--配置拦截路径-->
            <mvc:mapping path="/user/**"/>
            <!--注入拦截器-->
            <bean class="cn.bloghut.interceptor.LoginInterceptor"/>
        </mvc:interceptor>
    </mvc:interceptors>
</beans>

```



## 11、文件上传与下载

### 11.1基于Springmvc方式文件上传

1、导入文件上传的jar包，commons-fileupload ， Maven会自动帮我们导入他的依赖包 commons-io包；

```xml
<!--文件上传-->
<dependency>
    <groupId>commons-fileupload</groupId>
    <artifactId>commons-fileupload</artifactId>
    <version>1.3.3</version>
</dependency>
<!--servlet-api导入高版本的-->
<dependency>
    <groupId>javax.servlet</groupId>
    <artifactId>javax.servlet-api</artifactId>
    <version>4.0.1</version>
</dependency>

```



2、配置bean：multipartResolver
【注意！！！这个bena的id必须为：multipartResolver ， 否则上传文件会报400的错误】

```xml
<!--配置文件上传-->
<bean id="multipartResolver" class="org.springframework.web.multipart.commons.CommonsMultipartResolver">
    <!--设置默认编码-->
    <property name="defaultEncoding" value="utf-8"/>
    <!--上传文件大小上限 10485760 = 10M-->
    <property name="maxUploadSize" value="10485760"/>
    <property name="maxInMemorySize" value="40960"/>
</bean>

```



**CommonsMultipartFile 的 常用方法：**

- String **getOriginalFilename()**：获取上传文件的原名
- InputStream **getInputStream()**：获取文件流
- void **transferTo(File dest)**：将上传文件保存到一个目录文件中



3、编写前端页面

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
  <head>
    <title>$Title$</title>
  </head>
  <body>

  <form action="/upload" method="post" enctype="multipart/form-data"
    <input type="file" name="file">
  <input type="submit">
  </body>
</html>

```



4、编写Controller

```java
package cn.bloghut.controller;

import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;
import org.springframework.web.multipart.commons.CommonsMultipartFile;

import javax.servlet.http.HttpServletRequest;
import java.io.*;

/**
 * @Classname UploadControler
 * @Description 文件上传
 * @Date 2021/12/7 15:53
 * @Created by 闲言
 */
@RestController
public class UploadController {
    //@RequestParam("file") 将name=file控件得到的文件封装成CommonsMultipartFile 对象
    //批量上传CommonsMultipartFile则为数组即可
    @RequestMapping("/upload")
    public String fileUpload(@RequestParam("file") CommonsMultipartFile file , HttpServletRequest request) throws IOException {

        //获取文件名 : file.getOriginalFilename();
        String uploadFileName = file.getOriginalFilename();

        //如果文件名为空，直接回到首页！
        if ("".equals(uploadFileName)){
            return "redirect:/index.jsp";
        }
        System.out.println("上传文件名 : "+uploadFileName);

        //上传路径保存设置
        String path = request.getServletContext().getRealPath("/upload");
        //如果路径不存在，创建一个
        File realPath = new File(path);
        if (!realPath.exists()){
            realPath.mkdir();
        }
        System.out.println("上传文件保存地址："+realPath);

        InputStream is = file.getInputStream(); //文件输入流
        OutputStream os = new FileOutputStream(new File(realPath,uploadFileName)); //文件输出流

        //读取写出
        int len=0;
        byte[] buffer = new byte[1024];
        while ((len=is.read(buffer))!=-1){
            os.write(buffer,0,len);
            os.flush();
        }
        os.close();
        is.close();
        return "redirect:/index.jsp";
    }

}

```





### 11.2采用file.Transto 来保存上传的文件

```java
/*
 * 采用file.Transto 来保存上传的文件
 */
@RequestMapping("/upload2")
public String  fileUpload2(@RequestParam("file") CommonsMultipartFile file, HttpServletRequest request) throws IOException {

    //上传路径保存设置
    String path = request.getServletContext().getRealPath("/upload");
    File realPath = new File(path);
    if (!realPath.exists()){
        realPath.mkdir();
    }
    //上传文件地址
    System.out.println("上传文件保存地址："+realPath);

    //通过CommonsMultipartFile的方法直接写文件（注意这个时候）
    file.transferTo(new File(realPath +"/"+ file.getOriginalFilename()));

    return "redirect:/index.jsp";
}

```



### 11.3文件下载

文件下载步骤：
1、设置 response 响应头
2、读取文件 – InputStream
3、写出文件 – OutputStream
4、执行操作
5、关闭流 （先开后关）

```java
/**
 * 文件下载
 * @param response
 * @param request
 * @return
 * @throws Exception
 */
@RequestMapping(value="/download")
public String downloads(HttpServletResponse response , HttpServletRequest request) throws Exception{
    //要下载的图片地址
    String  path = request.getServletContext().getRealPath("/upload");
    String  fileName = "1.jpg";

    //1、设置response 响应头
    response.reset(); //设置页面不缓存,清空buffer
    response.setCharacterEncoding("UTF-8"); //字符编码
    response.setContentType("multipart/form-data"); //二进制传输数据
    //设置响应头
    response.setHeader("Content-Disposition",
            "attachment;fileName="+ URLEncoder.encode(fileName, "UTF-8"));

    File file = new File(path,fileName);
    //2、 读取文件--输入流
    InputStream input=new FileInputStream(file);
    //3、 写出文件--输出流
    OutputStream out = response.getOutputStream();

    byte[] buff =new byte[1024];
    int index=0;
    //4、执行 写出操作
    while((index= input.read(buff))!= -1){
        out.write(buff, 0, index);
        out.flush();
    }
    out.close();
    input.close();
    return "ok";
}

```

