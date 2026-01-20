# SpringCloud

**简述：**

springCloud ： 分布式微服务架构的一站式解决方案，是多种微服务架构落地技术的集合体，俗称微服务全家桶

## 1.微服务架构概述

### 1.1**什么是微服务架构？**

微服务架构是一种架构模式，它提倡将单一应用程序划分成一组雄安的服务，服务之间互相协调、互相配合、为用户提供最终价值。每个服务运行在其独立的进程中，服务与服务间采用轻量级的通信机制互相协作（通常是基于HTTP协议的RESTFul API）。每个服务都围绕着具体业务进行构建，并且能够被独立的部署到生产环境、类生产环境等。另外，应当尽量避免统一的、集中式的服务管理机制，对具体的一个服务而言，应根据业务上下文，选择合适的语言、工具对其进行构建。





## 2.微服务架构搭建

约定>配置>编码



### 2.1 IDEA新建project工作空间

#### 2.1.1 新建一个总父工程

 Maven依赖选择自己本地按照的maven，不要选择idea自带的![image-20220505165601466](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220505165601466.png)

设置字符编码为UTF－８

![image-20220505170245458](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220505170245458.png)

选择JDK版本设置为8

![image-20220505170454495](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220505170454495.png)

勾选上自动注解

![image-20220505170543138](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220505170543138.png)



导入依赖,在这里可能会报找不到依赖的异常,建议直接把<dependencyManagement>标签给它注释掉让它导入依赖再取消注释

```xml
<?xml version="1.0" encoding="UTF-8"?>

<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <groupId>com.xiaoliu</groupId>
  <artifactId>Hx_cloud</artifactId>
  <version>1.0-SNAPSHOT</version>
  <packaging>pom</packaging>

  <!--统一管理jar包和版本-->
  <properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <maven.compiler.source>1.8</maven.compiler.source>
    <maven.compiler.target>1.8</maven.compiler.target>
    <junit.version>4.12</junit.version>
    <log4j.version>1.2.17</log4j.version>
    <lombok.version>1.16.18</lombok.version>
    <mysql.version>5.1.47</mysql.version>
    <druid.verison>1.1.16</druid.verison>
    <mybatis.spring.boot.verison>1.3.0</mybatis.spring.boot.verison>
  </properties>

  <dependencyManagement>
    <dependencies>
      <!--spring boot 2.2.2-->
      <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-dependencies</artifactId>
        <version>2.2.2.RELEASE</version>
        <type>pom</type>
        <scope>import</scope>
      </dependency>
      <!--spring cloud Hoxton.SR1-->
      <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-dependencies</artifactId>
        <version>Hoxton.SR1</version>
        <type>pom</type>
        <scope>import</scope>
      </dependency>
      <!--spring cloud alibaba 2.1.0.RELEASE-->
      <dependency>
        <groupId>com.alibaba.cloud</groupId>
        <artifactId>spring-cloud-alibaba-dependencies</artifactId>
        <version>2.2.0.RELEASE</version>
        <type>pom</type>
        <scope>import</scope>
      </dependency>
      <!-- MySql -->
      <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>${mysql.version}</version>
      </dependency>
      <!-- Druid -->
      <dependency>
        <groupId>com.alibaba</groupId>
        <artifactId>druid-spring-boot-starter</artifactId>
        <version>${druid.verison}</version>
      </dependency>
      <!-- mybatis-springboot整合 -->
      <dependency>
        <groupId>org.mybatis.spring.boot</groupId>
        <artifactId>mybatis-spring-boot-starter</artifactId>
        <version>${mybatis.spring.boot.verison}</version>
      </dependency>
      <!--lombok-->
      <dependency>
        <groupId>org.projectlombok</groupId>
        <artifactId>lombok</artifactId>
        <version>${lombok.version}</version>
      </dependency>
      <!--junit-->
      <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>${junit.version}</version>
      </dependency>
      <!-- log4j -->
      <dependency>
        <groupId>log4j</groupId>
        <artifactId>log4j</artifactId>
        <version>${log4j.version}</version>
      </dependency>
    </dependencies>
  </dependencyManagement>

  <build>
    <plugins>
      <plugin>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-maven-plugin</artifactId>
        <configuration>
          <fork>true</fork>
          <addResources>true</addResources>
        </configuration>
      </plugin>
    </plugins>
  </build>
</project>

```



小tips：
1.Maven中的DependencyManagement和Dependencies
dependencyManagement
Maven 使用dependencyManagement元素来提供了一种管理依赖版本号的方式。**通常会在一个组织或者项目的最顶层的父POM中看到dependencyManagement元素。**

使用pom.xml 中的dependencyManagement元素能让所有在子项目中引用一个依赖而不用显式的列出版本号。Maven 会沿着父子层次向上走，直到找到一个拥有dependencyManagement元素的项目，然后它就会使用这个dependencyManagement元素中指定的版本号。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210601225503618.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)



![在这里插入图片描述](https://img-blog.csdnimg.cn/2021060122552165.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)

这样做的好处就是:如果有多个子项目都引用同一样依赖，则可以避免在每个使用的子项目里都声明一个版本号，这样当想升级或切换到另一个版本时，只需要在顶层父容器里更新，而不需要一个一个子项目的修改﹔另外如果某个子项目需要另外的一个版本，只需要声明version就可。

**dependencyManagement里只是声明依赖，并不实现引入，因此子项目需要显示的声明需要用的依赖.**

**maven中践跳过单元测试**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210601225811968.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)





### 2.2支付模块构建

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200509111935449.png)

**一.创建cloud-provider-payment8001微服务提供者支付Module模块**
**主要流程：**

#### **1.建Module**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200509112352113.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200509112417533.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)



#### **2.改pom**

```xml
 <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
        <dependency>
            <groupId>org.mybatis.spring.boot</groupId>
            <artifactId>mybatis-spring-boot-starter</artifactId>
        </dependency>
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>druid-spring-boot-starter</artifactId>
            <version>1.1.10</version>
        </dependency>
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-jdbc</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>
```



#### **3.yml文件**

创建yml文件

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200509112805455.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)

```yaml
server:
  port: 8001
  
  datasource:
    type: com.alibaba.druid.pool.DruidDataSource
    driver-class-name: org.gjt.mm.mysql.Driver
    url: jdbc:mysql://localhost:3306/db2019?useUnicode=true&characterEncoding=utf-8&useSSL=false
    username: root
    password: root

mybatis:
  type-aliases-package: com.atguigu.springcloud.entities
  mapper-locations: classpath:mapper/*.xml


```



#### **4.主启动**

```java
/**
 * @author xiaoliu
 */
@SpringBootApplication
public class Payment8001 {
    public static void main(String[] args) {
        SpringApplication.run(Payment8001.class,args);
    }
}
```



#### **5.新增数据库Payment**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200509113625772.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)



#### **6.构建业务类**

**entity层：**

```java
/**
 * @author xiaoliu
 */
@Data
@AllArgsConstructor
@NoArgsConstructor
public class Payment implements Serializable {
    private Long id;
    private String serial;

}
```

```java
/**
 * @author xiaoliu
 */
@Data
@AllArgsConstructor
@NoArgsConstructor
public class CommonResult<T> {

    private Integer code;
    private String message;
    private T data;

    public CommonResult(Integer code,String message){
        this(code,message,null);
    }


}
```



**mapper层：**

```java
/**
 * @author xiaoliu
 */
@Mapper
public interface PaymentMapper {

    @Insert("insert into payment(serial) values(#{serial})")
    int save(Payment payment);

    Payment getPaymentById(@Param("id") Long id);
}
```

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" "http://mybatis.org/dtd/mybatis-3-mapper.dtd" >
<mapper namespace="com.xiaoliu.springcloud.mapper.PaymentMapper">
    
    <resultMap id="BaseResultMap" type="payment">
        <id column="id" property="id" jdbcType="BIGINT"/>
        <id column="serial" property="serial" jdbcType="VARCHAR"/>
    </resultMap>
    <select id="getPaymentById" parameterType="Long" resultMap="BaseResultMap">
        select * from payment where id=#{id}
    </select>
</mapper>
```



**service层：**

```java
public interface PaymentService {
    int save(Payment payment);

    Payment getPaymentById(@Param("id") Long id);

}
```

```java
@Service
public class PaymentServiceImpl implements PaymentService {
    @Resource
    private PaymentMapper paymentMapper;

    @Override
    public int save(Payment payment) {
        return paymentMapper.save(payment);
    }

    @Override
    public Payment getPaymentById(Long id) {
        return paymentMapper.getPaymentById(id);
    }
}
```



**controller层：**

```java
@Slf4j
@RestController
@RequestMapping("/payment")
public class PaymentController {
    @Resource
    private PaymentService paymentService;

    @PostMapping("/save")
    public CommonResult save(@RequestBody Payment payment){
        int save = paymentService.save(payment);
        log.info("*************插入结果：" + save);
        if (save>0) {
            return new CommonResult(200,"插入数据库成功",save);
        }else {
            return new CommonResult(400,"插入数据库失败",null);
        }
    }

    @PostMapping("/paymentById/{id}")
    public CommonResult PaymentGetById(@PathVariable("id") Long id){
        Payment payment = paymentService.getPaymentById(id);
        log.info("**********查询结果：" + payment);
        if (payment !=null) {
            return new CommonResult(200,"查询数据库成功",payment);
        } else {
            return new CommonResult(400,"没有对应记录，查询ID：" + id,null);
        }
    }
}
```



### 2.3消费者订单模块搭建

#### 2.3.1**创建cloud-consumer-order80的Module**

#### 2.3.2 改pom

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <parent>
        <artifactId>Hx_cloud</artifactId>
        <groupId>com.xiaoliu</groupId>
        <version>1.0-SNAPSHOT</version>
    </parent>
    <modelVersion>4.0.0</modelVersion>

    <artifactId>cloud-consumer-orderMain80</artifactId>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>

    </dependencies>


</project>
```



#### 2.3.3 写YML

```yaml
server:
  port: 80
```



#### 2.3.4 写启动类

```java
package com.xiaoliu.springcloud;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class OrderMain80 {
    public static void main(String[] args) {
        SpringApplication.run(OrderMain80.class,args);
    }
}

```



#### 2.3.5 业务类

1.entity

```java
/**
 * 实体类
 */
@Data
@AllArgsConstructor
@NoArgsConstructor
public class Payment implements Serializable {

    private Long id;

    private String serial;

}


```

```java
/**
 * 返回数据
 * @param <T>
 */
@Data
@AllArgsConstructor
@NoArgsConstructor
public class CommonResult<T> {

    private Integer code;

    private String message;

    private T data;

    private CommonResult(Integer code,String message){
       this(code,message,null);
    }
}


```



2.config

```java
@Configuration
public class ApplicationContextConfig {

    @Bean
    public RestTemplate getRestTemplate(){
        return new RestTemplate();
    }
}


```

**什么是RestTemplate**
RestTemplate提供了多种便捷访问远程Http服务方法，是一种简单便捷的访问restful服务模板类，是Spring提供的用于访问Rest服务的可无端模板工具集



3.controller

```java
import com.atguigu.springcloud.entities.CommonResult;
import com.atguigu.springcloud.entities.Payment;
import lombok.extern.slf4j.Slf4j;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RestController;
import org.springframework.web.client.RestTemplate;

import javax.annotation.Resource;

@RestController
@Slf4j
public class OrderController {

    public static final String PAYMENT_URL="http://localhost:8001";
    
    @Resource
    private RestTemplate restTemplate;

    @GetMapping("/consumer/payment/create")
    public CommonResult<Payment> create(@RequestBody Payment payment){
        return restTemplate.postForObject(PAYMENT_URL+"/payment/create",payment, CommonResult.class);
    }

    @GetMapping("/consumer/payment/get/{id}")
    public CommonResult<Payment> getPayment(@PathVariable("id") Long id){
        return restTemplate.getForObject(PAYMENT_URL+"/payment/get/"+id,CommonResult.class);
    }

}


```



### 2.4工程重构

实体类在多个微服务中使用，是重复部分，我们将他单独提取出来，打包，在各个微服务中使用

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200509145606457.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)



#### **1.新建Module**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200509145711755.png)



#### **2.pom文件**

```xml
 <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>cn.hutool</groupId>
            <artifactId>hutool-all</artifactId>
            <version>5.1.0</version>
        </dependency>
    </dependencies>



```



#### **3.将原先工程中的实体类删除，在重构工程中添加实体类**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200509150004757.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)



#### **4.maven打包**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200509150320334.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)

或者自己手敲命令执行





#### **5.订单80和支付8001分别改造**

pom文件中加入包

```xml
<dependency>
            <groupId>com.atguigu.springcloud</groupId>
            <artifactId>cloud-api-commons</artifactId>
            <version>${project.version}</version>
        </dependency>

```





## 3.EurekaServer

### 3.1单机版EurekaServer搭建

#### **1.创建Module**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200509155054412.png)



#### **2.改pom文件**

```xml
<dependencies>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
        </dependency>
        <dependency>
            <groupId>com.atguigu.springcloud</groupId>
            <artifactId>cloud-api-commons</artifactId>
            <version>${project.version}</version>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>


```



#### **3.yml文件**

```yaml
server:
  port: 7001

#eureka服务端的实例名称
eureka:
  instance:
    hostname: localhost
  client:
    #false表示不向注册中心注册自己
    register-with-eureka: false
    #false表示自己端就是注册中心，我的职责就是维护服务实例，并不需要去搜索服务
    fetch-registry: false
    service-url:
      #设置与eureka server交互的地址查询服务和注册服务都需要依赖这个地址
   defaultZone: http://${eureka.instance.hostname}:${server.port}/eureka/

```



#### **4.主启动类**

```java
@SpringBootApplication
@EnableEurekaServer
public class EurekaMain7001 {
    public static void main(String[] args) {
        SpringApplication.run(EurekaMain7001.class,args);
    }
}


```



#### **5.测试**

http://locallhost:7001
此时还没有服务入驻，所以是没有发现微服务

![image-20220506134403998](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220506134403998.png)





### 3.2将微服务注册到EurekaServer注册中心

#### **1.修改pom文件**

在pom文件添加

```xml
<dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
        </dependency>

```



#### **2.修改yml文件**

在yml文件中添加

```yaml
spring:
  application:
    #微服务名称
    name: cloud-order-service
eureka:
  client:
    #表示是否将自己注册进eurekaServer 默认为true
    register-with-eureka: true
    fetch-registry: true
    service-url:
     defaultZone: http://localhost:7001/eureka/

```





#### **3.修改主启动类**

在主启动类中添加注解

```java
@SpringBootApplication
@EnableEurekaClient
public class OrderMain80 {
    public static void main(String[] args) {
        SpringApplication.run(OrderMain80.class,args);
    }
}
```



#### 4.测试

4.1先启动eurekaServer，7001服务
4.2再要启动服务提供者provider，8001服务
4.3地址：http://localhost/consumer/payment/get/1

![image-20220506142000288](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220506142000288.png)





### 3.3 EurekaServer集群部署

#### **1.新建cloud-eureka-server7002工程（参考7001）**

#### **2.pom文件**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <parent>
        <artifactId>Hx_cloud</artifactId>
        <groupId>com.xiaoliu</groupId>
        <version>1.0-SNAPSHOT</version>
    </parent>
    <modelVersion>4.0.0</modelVersion>

    <artifactId>cloud-eureka_server7002</artifactId>


    <dependencies>
        <!-- eureka-server -->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
        </dependency>
        <!--自定义api通用包-->
        <dependency>
            <groupId>com.xiaoliu</groupId>
            <artifactId>cloud-api-commons</artifactId>
            <version>${project.version}</version>
        </dependency>
        <!--SpringMvc-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <!--图形监视器-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
        <!--热部署-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <!--lombok-->
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
        <!--junit-->
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>

</project>
```



#### 3.YML

```yaml
server:
  port: 7002

#eureka服务端的实例名称
eureka:
  instance:
    hostname: eureka7002.com
  client:
    #false表示不向注册中心注册自己
    register-with-eureka: false
    #false表示自己端就是注册中心，我的职责就是维护服务实例，并不需要去搜索服务
    fetch-registry: false
    service-url:
      #设置与eureka server交互的地址查询服务和注册服务都需要依赖这个地址
      defaultZone: http://eureka7001.com:7001/eureka/
```



#### **4.修改映射配置**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200511142044309.png)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200511142229278.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200511142132282.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)



#### **5.修改7001yml文件**

```yaml
server:
  port: 7001

eureka:
  instance:
    hostname: eureka7001.com #eureka服务端的实例名称
  client:
    # false表示不向注册中心注册自己
    register-with-eureka: false
    # false表示自己端就是注册中心，我的职责就是维护服务实例，并不需要去检索服务
    fetch-registry: false
    service-url:
      # 设置与Eureka Server交互的地址查询服务和注册服务都需要依赖这个地址。
      defaultZone: http://eureka7002.com:7002/eureka/
```



#### **5.主启动类**

```java
@SpringBootApplication
@EnableEurekaServer
public class EurekaMain7002 {
    public static void main(String[] args) {
        SpringApplication.run(EurekaMain7002.class,args);
    }
}


```



#### **测试**

![image-20220506160218469](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220506160218469.png)

![image-20220506160234196](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220506160234196.png)



### 3.4 支付微服务集群配置

#### **1.参考cloud-provider-payment8001构建cloud-provider-payment8002**

#### **2.pom文件**

```xml
 <dependencies>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
        <dependency>
            <groupId>org.mybatis.spring.boot</groupId>
            <artifactId>mybatis-spring-boot-starter</artifactId>
        </dependency>
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>druid-spring-boot-starter</artifactId>
            <version>1.1.10</version>
        </dependency>
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-jdbc</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>com.atguigu.springcloud</groupId>
            <artifactId>cloud-api-commons</artifactId>
            <version>${project.version}</version>
        </dependency>
    </dependencies>


```



#### **3.yml文件**

```yaml
server:
  port: 8002

spring:
  application:
    name: cloud-payment-service

  datasource:
    type: com.alibaba.druid.pool.DruidDataSource
    driver-class-name: org.gjt.mm.mysql.Driver
    url: jdbc:mysql://localhost:3306/db2019?useUnicode=true&characterEncoding=utf-8&useSSL=false
    username: root
    password: root

mybatis:
  type-aliases-package: com.atguigu.springcloud.entities
  mapper-locations: classpath:mapper/*.xml

eureka:
  client:
    #表示是否将自己注册进eurekaServer 默认为true
    register-with-eureka: true
    fetch-registry: true
    service-url:
      defaultZone: http://eureka7001.com:7001/eureka/,http://eureka7002.com:7002/eureka/

  instance:
    instance-id: payment8002
    prefer-ip-address: true



```



#### **4.主启动类**

```java
@SpringBootApplication
@EnableEurekaClient
public class PaymentMain8002 {
    public static void main(String[] args) {
        SpringApplication.run(PaymentMain8002.class,args);
    }
}


```



#### **5.业务类（参考8001）**

#### **6.修改8001,8002controller**

8001:

```java
@RestController
@Slf4j
public class PaymentController {

    @Resource
    private PaymentService paymentService;

    @Resource
    private DiscoveryClient discoveryClient;

    @Value("${server.port}")
    private String serverPort;

    @PostMapping("/payment/creat")
    public CommonResult<Payment> create(@RequestBody Payment payment){

        int result=paymentService.create(payment);
        log.info("******插入结果"+result);
        if (result>0){
            return new CommonResult(200,"success",result);
        }else {
            return new CommonResult(400,"fail",null);
        }
    }

    @GetMapping("/payment/get/{id}")
    public CommonResult<Payment> getPaymentById(@PathVariable("id") Long id){
        Payment payment=paymentService.getPaymentById(id);
        log.info("******查询结果"+payment);
        if(payment!=null) {
            return new CommonResult(200, "success,serverPort:"+serverPort, payment);
        }else {
            return new CommonResult(400,"fail",null);
        }

    }

    @GetMapping("/payment/discovery")
    public Object discovery(){
       List<String> services=discoveryClient.getServices();
       for (String service:services){
           log.info("***********service:"+service);
       }
       List<ServiceInstance> serviceInstances=discoveryClient.getInstances("CLOUD-PAYMENT-SERVICE");
       for (ServiceInstance serviceInstance:serviceInstances){
           log.info(serviceInstance.getHost()+"\t"+serviceInstance.getInstanceId()+"\t"+serviceInstance.getPort()+"\t"+serviceInstance.getUri());
       }
       return this.discoveryClient;
    }
}


```



8002:

```java
@RestController
@Slf4j
public class PaymentController {

    @Resource
    private PaymentService paymentService;

    @Value("${server.port}")
    private String serverPort;

    @PostMapping("/payment/creat")
    public CommonResult<Payment> create(@RequestBody Payment payment){

        int result=paymentService.create(payment);
        log.info("******插入结果"+result);
        if (result>0){
            return new CommonResult(200,"success",result);
        }else {
            return new CommonResult(400,"fail",null);
        }
    }

    @GetMapping("/payment/get/{id}")
    public CommonResult<Payment> getPaymentById(@PathVariable("id") Long id){
        Payment payment=paymentService.getPaymentById(id);
        log.info("******查询结果"+payment);
        if(payment!=null) {
            return new CommonResult(200, "success,serverPort:"+serverPort, payment);
        }else {
            return new CommonResult(400,"fail",null);
        }

    }
}


```





**两台机器做负载均衡**
orderController修改

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210606123108682.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)



ApplicationContextConfig修改,使用了这个注解赋予了RestTemplate负载均衡的能力,是轮询得方式

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210606123426599.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)



#### **7.测试**

http://localhost/consumer/payment/get/1
负载轮询，8001和8002端口轮询出现





### 3.5 actuator微服务信息完善

**主机名称:服务名称修改**
当前问题：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210606124406892.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)



含有主机名称
修改8001，8002

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210606125713455.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210606125737917.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)



重启7001,7002，8001,8002
效果

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210606125811224.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210606125828920.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)



**访问信息有IP信息提示**
无ip信息提示



修改8001,8002

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210606130141858.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210606130157153.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)



效果：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210606130233592.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)







### 3.6 服务发现Discovery

**Discovery功能：**
对于注册进[eureka](https://so.csdn.net/so/search?q=eureka&spm=1001.2101.3001.7020)里面的微服务，可以通过服务发现来获得服务的信息

#### **1.修改cloud-provider-payment8001的controller**

```java
@RestController
@Slf4j
public class PaymentController {

    @Resource
    private PaymentService paymentService;

    @Resource
    private DiscoveryClient discoveryClient;

    @Value("${server.port}")
    private String serverPort;

    @PostMapping("/payment/creat")
    public CommonResult<Payment> create(@RequestBody Payment payment){

        int result=paymentService.create(payment);
        log.info("******插入结果"+result);
        if (result>0){
            return new CommonResult(200,"success",result);
        }else {
            return new CommonResult(400,"fail",null);
        }
    }

    @GetMapping("/payment/get/{id}")
    public CommonResult<Payment> getPaymentById(@PathVariable("id") Long id){
        Payment payment=paymentService.getPaymentById(id);
        log.info("******查询结果"+payment);
        if(payment!=null) {
            return new CommonResult(200, "success,serverPort:"+serverPort, payment);
        }else {
            return new CommonResult(400,"fail",null);
        }

    }

    @GetMapping("/payment/discovery")
    public Object discovery(){
       List<String> services=discoveryClient.getServices();
       for (String service:services){
           log.info("***********service:"+service);
       }
       List<ServiceInstance> serviceInstances=discoveryClient.getInstances("CLOUD-PAYMENT-SERVICE");
       for (ServiceInstance serviceInstance:serviceInstances){
           log.info(serviceInstance.getHost()+"\t"+serviceInstance.getInstanceId()+"\t"+serviceInstance.getPort()+"\t"+serviceInstance.getUri());
       }
       return this.discoveryClient;
    }
}


```



#### **2.8001的主启动类**

```java
@SpringBootApplication
@EnableEurekaClient
@EnableDiscoveryClient
public class PaymentMain8001 {
    public static void main(String[] args) {
        SpringApplication.run(PaymentMain8001.class,args);
    }
}

```



#### **3.测试**

3.1启动eurekaServer
3.2启动8001
地址：http://localhost:8001/payment/discovery
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200512100615993.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)





### 3.7 eureka自我保护机制

#### **1.为什么会产生Eureka自我保护机制？**

为了防止eurekaclient可以正常运行，但是与EurekaServer网络不通的情况下，EurekaServer不会立刻将EurekaClient服务剔除



#### 2.什么是自我保护模式？

默认情况下，如果eurekaServer在一定时间内没有接收到某个服务实例的心跳，EurekaServer将会注销实例（默认90秒）。但是当网络分区故障发生（延时，卡顿，拥挤时）为，微服务与EurekaServer之间无法正常通信，以上行为可能变得非常危险——因为微服务本身其实是健康的，此时不应该注销这个服务。Eureka通过“自我保护模式”来解决这个问题——当EurekaServer节点在短时间内丢失过多客户端时（可能发生了网络分区故障），那么这个节点就会进入自我保护模式。

![在这里插入图片描述](https://img-blog.csdnimg.cn/2020051210305535.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)



## 4.zookeeper

zookeeper代替eureka



#### **1.要求：在centos上已安装zookeeper**

安装教程地址：https://www.cnblogs.com/huangjianping/p/8012580.html



#### **2.环境准备**

1.关闭防火墙
systemctl stop firewalld
2.查看linux的ip地址
ifconfig
3.linux端和windows端互相ping通



#### **3.编码实现**

**3.1 新建cloud-provider-payment8004**
**3.2 pom文件**

```xml
<dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
        <dependency>
            <groupId>org.mybatis.spring.boot</groupId>
            <artifactId>mybatis-spring-boot-starter</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-zookeeper-discovery</artifactId>
<!--            排除自带的的zookeeper-->
            <exclusions>
                <exclusion>
                    <groupId>org.apache.zookeeper</groupId>
                    <artifactId>zookeeper</artifactId>
                </exclusion>
            </exclusions>
        </dependency>
        <!--            添加zookeeper3.4.9版本-->
        <dependency>
            <groupId>org.apache.zookeeper</groupId>
            <artifactId>zookeeper</artifactId>
            <version>3.4.9</version>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>com.atguigu.springcloud</groupId>
            <artifactId>cloud-api-commons</artifactId>
            <version>${project.version}</version>
        </dependency>
    </dependencies>

```



**3.3 yml文件**

```yaml
server:
  port: 8004

spring:
  application:
    name: cloud-provider-payment
  cloud:
    zookeeper:
      connect-string: 192.168.153.129:2181

```



**3.4 主启动类**

```java
@SpringBootApplication(exclude = {DataSourceAutoConfiguration.class})
//该注解用于向使用consul或者zookeeper作为注册中心时注册服务
@EnableDiscoveryClient
public class PaymentMain8004 {
    public static void main(String[] args) {
        SpringApplication.run(PaymentMain8004.class,args);
    }
}


```



**3.5 controller**

```java
@RestController
@Slf4j
public class PaymentController {

    @Value("${server.port}")
    private String serverPort;

    @RequestMapping("/payment/zk")
    public String paymentZk(){
        return serverPort+"\t"+ UUID.randomUUID().toString();
    }
}


```



**3.6 启动zookeeper**
zkServer.sh start

**3.7连接服务端**
./zkCli.sh
如果出现-bash: ./zkCli.sh: 没有那个文件或目录错误
运行zkCli.sh -server localhost:2181则可成功连接

**3.6 启动8004注册进zookeeper**
如果没有做jar包排除，会出现jar冲突问题，在pom文件中排除自带的jar包，引入3.4.9的zookeeper版本即可解决问题



**3.7查看服务**
![img](https://img-blog.csdnimg.cn/20200512113111194.png)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200512113326409.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)



地址：http://localhost:8004/payment/zk

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200512113416547.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)



**测试成功**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200512113450532.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)



## 5.Consul

### 5.1Consul简介

#### 1.什么是consul？

consul是一套开元的分布式服务发现和配置管理系统，由HashCorp公司用Go语言开发

提供了微服务系统中的服务治理，配置中心，控制总线等功能。这些功能中的每一个都可以根据需要单独使用，也可以一起以构建全方位的服务网络，总之consul提供了一种完整的服务网络解决方案

它具有很多优点，包括：基于raft协议，比较简洁；支持健康检查，同时支持HTTP和DNS协议支持跨数据中心的WAN集群 提供图形界面，跨平台，支持linux，mac，windows

#### 2.consul能做什么？

1. 服务发现：提供HTTP和DNS两种发现方式
2. 健康监测：支持多种方式，HTTP,TCP,Docker,Shell脚本定制化
3. KV存储：Key，Value的存储方式
4. 多数据中心：Consul支持多数据中心
5. 可视化Web界面



#### **3.下载地址**

http://www.consul.io/downloads.html



#### **4.consul中文教程**

http://www.springcloud.cc/spring-cloud-consul.html





### 5.2 将服务注册进Consul

#### **1.新建Module支付服务**

cloud-providerconsul-payment8006



#### **2.pom文件**

```xml
<dependencies>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-consul-discovery</artifactId>
        </dependency>
        <!--web包-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
        <!--通用包-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>com.atguigu.springcloud</groupId>
            <artifactId>cloud-api-commons</artifactId>
            <version>${project.version}</version>
        </dependency>
    </dependencies>

```



#### **3.yml文件**

```yaml
server:
  port: 8006


spring:
  application:
    name: consul-provider-payment
    #consul注册中心地址
  cloud:
    consul:
      host: localhost
      port: 8500
      discovery:
        service-name: ${spring.application.name}

```



#### **4.主启动类**

```java
@SpringBootApplication
@EnableDiscoveryClient
public class PaymentMain8006 {
    public static void main(String[] args) {
        SpringApplication.run(PaymentMain8006.class,args);
    }
}


```



#### **5.业务类controller**

```java
@RestController
@Slf4j
public class PaymentController {

    @Value("${server.port}")
    private String serverPort;

    @RequestMapping("/payment/consul")
    public String paymentConsul(){
        return serverPort+"\t"+ UUID.randomUUID().toString();
    }
}


```



#### **6.测试**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200513155828414.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200513155912869.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)





## 6.三个注册中心异同点

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210608220127146.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210608220245584.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)

C:Consistency（强一致性)
A:Availability (可用性)
P: Partition tolerance（分区容错性
CAP理论关注粒度是数据，而不是整体系统设计的策略



最多只能同时较好的满足两个。
CAP理论的核心是:一个分布式系统不可能同时很好的满足一致性，可用性和分区容错性这三个需求，因此，根据CAP原理将NoSQL数据库分成了满足CA原则、满足CP原则和满足AP原则三大类:CA-单点集群，满足一致性，可用性的系统，通常在可扩展性上不太强大。
CP–满足一致性，分区容忍必的系统，通常性能不是特别高。
AP- 满足可用性，分区容忍性的系统，通常可能对—致性要求低一些。

AP(Eureka)
CP(Zookeeper/Consul)





## 7.Ribbon

### 7.1 ribbon是什么？

Spring Cloud Ribbqn是基于Netflix Ribbon实现的一套**客户端负载均衡**的工具。

简单的说，Ribbon是Netflix发 布的开源项目，主要功能是提供客户端的软件负载均衡算法和服务调用。Ribbon客户端组件提供-系列
完善的配置项如连接超时，重试等。简单的说，就是在配置文件中列出Load Balancer (简称LB)后面所有的机器，Ribbon会自动的帮
助你基于某种规则(如简单轮询，随机连接等)去连接这些机器。我们很容易使用Ribbon实现自定义的负载均衡算法。

#### **2.官网**

https://github.com/Netflix/ribbon/wiki/Getting-Started



#### 3.作用

##### 3.1 负载均衡

LB负载均衡(Load Balance)是什么
简单的说就是将用户的请求平摊的分配到多个服务上，从而达到系统的HA (高何用)。
常见的负载均衡有软件Nginx, LVS, 硬件F5等。

Ribbon本地负载均衡客户端VS Nginx服务端负载均衡区别
Nginx是服务器负载均衡，客户端所有请求都会交给nginx,然后由nginx实现转发请求。唤载均衡是由服务端实现的。

Ribbon本地负载均衡，在调用微服务接口时候，会在注册中心上获取注册信息服务列表之后缓存到JVM本地，从而在本地实现RPC远
程服务调用技术。

##### 3.1.1集中式

即在服务的消费方和提供方之间使用独立的LB设施可以是硬件,如F5, 可以是软件,如nginx), 由该设施负责把访问请求通过某种策略转发至服务的提供方;

##### 3.1.2进程式

将L B逻辑集成到消费方，消费方从服务注册中心获知有哪些地址可用,然后自己再从这些地址中选择出一个合适的服务器。

Ribbon就属于进程内LB,它只是一个类库, 集成于消费方进程，消费方通过它来获取到服务提供方的地址。



### 7.2 Ribbon的负载均衡和Rest调用

Ribbon其实就是一 一个软负载均衡的客户端组件,他可以和其他所需请求的客户端结合使用，和eureka结合只是其中的- -个实例

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200514091653478.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)



Ribbon在工作时分成两步
第一步先选择EurekaServer ,它优先选择在同一个区域内负载较少的server.
第二步再根据用户指定的策略，在从server取到的服务注册列表中选择一 个地址。
其中Ribbon提供了多种策略:比如轮询、随机和根据响应时间加权。

spring-cloud-starter-netflix- eureka- client自带了spring-cloud-starter-ibbon引用

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200514092725153.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)



**RestTemplate**

#### 1.官网

https://docs.spring.io/spring-framework/docs/5.2.2.RELEASE/javadoc-api/org/springframework/web/client/RestTemplate.html



#### 2.getForObject方法/getForEntity方法

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200514093845493.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)

```java
 @GetMapping("/consumer/payment/getForEntity/{id}")
    public CommonResult<Payment> getPayment2(@PathVariable("id") Long id){

        ResponseEntity<CommonResult> entity=restTemplate.getForEntity(PAYMENT_URL+"/payment/get/"+id,CommonResult.class);
        if(entity.getStatusCode().is2xxSuccessful()){
            return entity.getBody();
        }else {
            return new CommonResult<>(444,"操作失败");
        }

    }

```

测试

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200514100741278.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)

#### 3.postFqrObject/postForEntity

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200514093951224.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)

4.GET请求方法
5.POST请求方法



### 7.3 Ribbon默认自带的负载均衡策略

#### Ribbon的核心组件IRule

Ribbon默认的负载均衡算法是轮询，而IRule是根据特定的算法中从服务列表中选取其中一个要访问的服务。

一共有7个方法。

![image-20200905163732232](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9naXRlZS5jb20vYmFpbGVmb2xlbi90eXBvcmEtcGljdHVyZXMvcmF3L21hc3Rlci90eXBvcmEtcGljdHVyZXMvaW1nL2ltYWdlLTIwMjAwOTA1MTYzNzMyMjMyLnBuZw?x-oss-process=image/format,png)







### 7.4 Ribbon负载规则替换

**如何替换**

#### 1.修改cloud-consumer-order80

#### 2.注意配置细节



![在这里插入图片描述](https://img-blog.csdnimg.cn/20200514112320739.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)



![在这里插入图片描述](https://img-blog.csdnimg.cn/20200514112401186.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)



#### 3.新建package（com.atguigu.myrule）

#### 4.新建的包中新建MySelfRule规则类

```java
@Configuration
public class MySelfRule {

    @Bean
    public IRule myRule(){
        //定义为随机
        return new RandomRule();
    }
}


```

#### 5.主启动类添加@RibbonClient

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200514112956978.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)



#### 6.测试

端口随机
地址：http://localhost/consumer/payment/get/{id}





### 7.5 Ribbon默认负载轮询算法原理

#### **1.原理**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200514114248428.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)





#### **2.源码**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200514115316924.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/2020051411535388.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)



![在这里插入图片描述](https://img-blog.csdnimg.cn/2020051411555998.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)



#### **3.实现**

自己实现一个本地[负载均衡](https://so.csdn.net/so/search?q=负载均衡&spm=1001.2101.3001.7020)器

##### 3.1 7001/7002集群启动

##### 3.2 8001/8002[微服务](https://so.csdn.net/so/search?q=微服务&spm=1001.2101.3001.7020)改造

修改8001和8002的controller

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200514141459839.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)

```java
 @GetMapping("/payment/lb")
    public String getPaymentLB(){
        return serverPort;
    }

```

##### 3.3 80订单微服务改造



##### 3.3.1 ApplicationContextBean去掉注解@LoadBalanced

##### 3.3.2 LoadBalancer接口

```java
public interface LoadBalancer {
    ServiceInstance instances(List<ServiceInstance> serviceInstances);
}
```

##### 3.3.3 MyLB

```java
@Component
public class MyLB implements LoadBalancer {

    private AtomicInteger atomicInteger=new AtomicInteger(0);

    public final  int getAndIncrement(){
        int current;
        int next;
        do{
            current=this.atomicInteger.get();
            next=current >= 2147483647 ? 0 : current+1;
        }while (!this.atomicInteger.compareAndSet(current,next));
        System.out.println("******next:"+next);
        return next;

    }

    //负载均衡算法: rest接口第几次请求数%服务器集群总数量=实际调用服务器位置下标， 每次服务重启动后rest接口计数从1开始。|

    @Override
    public ServiceInstance instances(List<ServiceInstance> serviceInstances) {

        int index=getAndIncrement() % serviceInstances.size();

        return serviceInstances.get(index);
    }
}


```



##### 3.3.4 OrderController

```java
    @Resource
    private LoadBalancer loadBalancer;
    
    @Resource
    private DiscoveryClient discoveryClient;
    
 @GetMapping("/consumer/payment/lb")
    public String getPaymentLB(){
        List<ServiceInstance> instances=discoveryClient.getInstances("CLOUD-PAYMENT-SERVICE");

        if(instances==null || instances.size() <= 0){
            return null;
        }
        ServiceInstance serviceInstance=loadBalancer.instances(instances);
        URI uri=serviceInstance.getUri();
        return restTemplate.getForObject(uri+"/payment/lb",String.class);
    }

```



##### 3.3.5 测试

地址：http://localhost/consumer/payment/lb





## 8.OpenFeign

### 8.1 OpenFeign是什么

官网：https://cloud.spring.io/spring-cloud-static/Hoxton.SR1/reference/htmlsingle/#spring- cldud-openfeign

Feign是一个声明式WebService喀户端。 使用Feign能让编写Web Service客户端更加简单。

它的使用方法是定义一个服务接口然后在 上面添加注解。Feign支持可拔插式的编码器和解码器。Spring Cloud对Feign进行了封装，使其支持了Spring MVC标准注解和HttpMessageConverters. Feign可以与Eureka和Ribbon组合使用以支持负载均衡



### 8.2 作用

Feign旨在使编写Java Http客户端变得更容易。
前面在使用Ribbon+ RestTemplate时，利用RestTemplate对http请求的封装处理，形成了一套模版化的调用方法。但是在实际开发中，由于对服务依赖的调用可能不止一处， 往往一个接口会被多处调用， 所以通常都会针对每个微服务自行封装一 些客户端类来包装这些依赖服务的调用。所以，Feign在此基础上做了进一封装,由他来帮助我们定义和实现依赖服务接口的定义。在Feign的实现下，我们只需创建一个接口并使用注解的方式来配置它(以前是Dao接口 上面标注Mapper注解,现在是一个微服务接口 上面标注一个Feign注解即可)，即可完成对服务提供方的接口绑定,简化了使用Spring cloud Ribbon时，自动封装服务调用客户端的开发量。


**Feign集成了Ribbon**
利用Ribbon维护了Payment的服务列表信息，并且通过轮询实现了客户端的负载均衡。与Ribbon不同的是,通过feign只需要定义服务绑定接口且以声明式的方法,优雅而简单的实现了服务调用





### **8.3 Feign和OpenFeign的区别**

|                          **Feign**                           |                        **OpenFeign**                         |
| :----------------------------------------------------------: | :----------------------------------------------------------: |
| Feign是Spring Cloud组件中的一个轻量级RESTful的HTTP服务客户端，Feign内置了Ribbon,用来做客户端负载均衡，去调用服务注册中心的服务。Feign的使用方式是:使用Feign的注解定义接口,调用这个接口，就可以调用服务注册中心的服务 | OpenFeign是Spring Cloud在Feign的基础上支持了SpringMVC的注解，如@RequesMapping等等。OpenFeign的**@FeignClient**可以解析SpringMVC的@RequestMapping注解下的接口，并通过动态代理的方式产生实现类，实现类中做负载均衡并调用其他服务。<br/> |
| ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200514155256727.png) |  ![img](https://img-blog.csdnimg.cn/20200514155311406.png)   |





### **8.4.OpenFeign使用步骤**

#### **1 接口+注解**

微服务调用接口+@FeignClient

#### **2 新建cloud-consumer-feign-order80**

#### **3 pom文件**

```xml
 <dependencies>
        <!--openfeign-->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-openfeign</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>com.atguigu.springcloud</groupId>
            <artifactId>cloud-api-commons</artifactId>
            <version>${project.version}</version>
        </dependency>
    </dependencies>

```



#### **4.yml文件**

```yaml
server:
  port: 80



eureka:
  client:
    #表示是否将自己注册进eurekaServer 默认为true
    register-with-eureka: false
    service-url:
      #defaultZone: http://localhost:7001/eureka/
      defaultZone: http://eureka7001.com:7001/eureka/,http://eureka7002.com:7002/eureka/

```



#### **5.主启动类**

```java
@SpringBootApplication
@EnableFeignClients
public class OrderFeignMain80 {

    public static void main(String[] args) {
        SpringApplication.run(OrderFeignMain80.class,args);
    }
}
```



#### **6.业务类**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200514160938268.png)

**接口**

```java
@Component
@FeignClient(value = "CLOUD-PAYMENT-SERVICE")
public interface PaymentFeignService {

    @GetMapping("/payment/get/{id}")
    CommonResult<Payment> getPaymentById(@PathVariable("id") Long id);

}
```



**controller**

```java
@RestController
@Slf4j
public class OrderFeignController {

    @Resource
    private PaymentFeignService paymentFeignService;

    @GetMapping("/consumer/payment/get/{id}")
    public CommonResult<Payment> getPaymentById(@PathVariable("id") Long id){

        return paymentFeignService.getPaymentById(id);
    }

}
```



#### **7.测试**

先启动2个eureka集群7001/7002
再启动2个微服务8001/8002
启动OpenFeign启动
地址：http://localhost/consumer/payment/get/{id}

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210615211614978.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)







### 8.5 OpenFeign超时控制

#### **1.设置超时出错情况**

1.1服务提供方8001故意写暂停程序

```java

    @GetMapping("/payment/feign/timeout")
    public String paymentFeignTimeout(){
        //暂停几秒钟线程
        try{
            TimeUnit.SECONDS.sleep(3);
        }catch (InterruptedException e){
            e.printStackTrace();
        }
        return serverPort;
    }

```



1.2服务消费方80添加超时方法PaymentFeignService

```java
    @GetMapping("/payment/feign/timeout")
    public String paymentFeignTimeout();

```



1.3服务消费方80添加超时方法OrderFeignController

```java
  @GetMapping("/consumer/payment/feign/timeout")
    public String paymentFeignTimeout(){

        //OpenFeign-ribbon 客户端一般默认等待1秒钟
        return paymentFeignService.paymentFeignTimeout();

    }
```



1.4测试
地址：http://localhost/consumer/payment/[feign](https://so.csdn.net/so/search?q=feign&spm=1001.2101.3001.7020)/timeout
错误页面：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200514165357569.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)



#### 2.OpenFeign默认等待1秒钟，超过后报错

#### 3.是什么

默认Feign客户端只等待秒钟, 但是服务端处理需要超过1秒钟,导致Feign客户端不想等待了，直接返回报错。为了避免这样的情况，有时候我们需要设置Feign客户端的超时控制。

#### 4.YML文件里需要开启OpenFeign客户端超时控制

```java
#没置feign客户端超时时间(openFeign默认支持ribbon)
ribbon:
  #指的是建立连接所用的时间，适用于网络状况iE常的情况下两端连接所用的时间
  Readtimeout: 5000
  #指的是建立连接后从服务器读取到可用资源所用的时间
  ConnectTimeout: 5000
```



### 8.4 OpenFeign日志增强

#### **1.日志打印功能**

#### **2.是什么**

[Feign](https://so.csdn.net/so/search?q=Feign&spm=1001.2101.3001.7020)提供了日志打印功能,我们可以通过配置来调整日志级别，从而了解Feign中Http请求的细节。
说白了就是对Feign接口的调用情况进行监控和输出



#### **3.日志级别**

NONE:默认的,不显示任何日志;

BASIC:仅记录请求方法、URL、响应[状态码](https://so.csdn.net/so/search?q=状态码&spm=1001.2101.3001.7020)及执行时间;

HEACIERS:除了BASIC中定义的信息之外,还有请求和响应的头信息;

FULL:除了HEADERS中定义的信息之外，还有请求和响应的正文及元数据。



#### **4.配置日志bean**

```java


@Configuration
public class FeignConfig {

    @Bean
    Logger.Level feignLoggerLevel(){
        return Logger.Level.FULL;
    }
}
```



#### **5.YML文件里需要开启日志的Feign客户端**

```yaml
logging:
  level:
    com.atguigu.springcloud.service.PaymentFeignService: debug
```



#### **6.后台日志查看**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200514171326152.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)







## 9.Hystrix

### 1.分布式系统面临的问题

服务雪崩
多个微服务之间调用的时候,假设微服务A调用微服务B和微服务C,微服务B和微服务C又调用其它的微服务,这就是所谓的“扇出”。
如果扇出的链路上某个微服务的调用响应时间过长或者不可用,对微服务A的调用就会占用越来越多的系统资源，进而引起系统崩溃，所谓的“雪崩效应”.
对于高流量的应用来说，单一的后端依赖可能会导致所有服务 器上的所有资源都在几秒钟内饱和。比失败更糟糕的是,这些应用程序还可能导致服务之间的延迟增加，备份队列，线程和其他系统资源紧张，导致整个系统发生更多的级联故障。这些都表示需要对故障和延迟进行隔离和管理，以便单个依赖关系的失败，不能取消整个应用程序或系统。
所以,通常当你发现一个模块下的某个实例失败后，这时候这个模块依然还会接收流量，然后这个有问题的模块还调用了其他的模块,这样就
会发生级联故障，或者叫雪崩。


### 2.是什么

Hystrix是一个用于处理分布式系统的延迟和容错的开源库, 在分布式系统里,许多依赖不可避免的会调用失败,比如超时、异常等,Hystrix能够保证在一个依赖出问题的情况下， 不会导致整体服务失败,避免级联故障，以提高分布式系统的弹性。
“断路器”本身是-种开关装置，当某个服务单元发生故障之后,通过断路器的故障监控(类似熔断保险丝) .向调用方返回一个符合预期的、可处理的备选响应(FallBack) ，而不是长时间的等待或者抛出调用方无法处理的异常,这样就保证了服务调用方的线程不会被长时间、不必要地占用，从而避免了故障在分布式系统中的蔓延,乃至雪崩。



#### **2.1.作用**

服务降级
服务熔断
接近实时的监控



#### **2.2.官网资料**

https://github.com/Netflix/Hystrix/wiki/How-To-Use



#### **2.3.停更进维**

https://github.com/Netflix/Hystrix

被动修复bugs
不再接受合并请求
不再发布新版本



### 3.Hystrix服务降级熔断限流概念

#### **1.服务降级**

1.1 服务器忙，请稍后再试，不让客户端等待并立刻返回-个友好提示，fallback
1.2 哪些情况会出发降级
程序运行异常
超时
服务熔断触发服务降级
线程池/信号量打满也会导致服务降级



#### **2.服务熔断**

2.1 类比保险丝达到最大服务访问后，直接拒绝访问，拉闸限电，然后调用服务降级的方法并返回友好提示
2.2 就是保险丝
服务的降级->进而熔断->恢复调用链路

#### **3.服务限流**

秒杀高并发等操作，严禁-窝蜂的过来拥挤，大家排队，一秒钟N个,有序进行





### 4.Hystrix支付微服务构建

#### **1.新建cloud-provider-hystrix-payment8001**

#### **2.pom文件**

```xml
 <dependencies>

        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-netflix-hystrix</artifactId>
        </dependency>

        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
        </dependency>

        <!--web包-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
        <!--通用包-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>com.atguigu.springcloud</groupId>
            <artifactId>cloud-api-commons</artifactId>
            <version>${project.version}</version>
        </dependency>

</dependencies>


```



#### **3.yml文件**

```yaml
server:
  port: 8001


spring:
  application:
    name: cloud-provider-hystrix-payment


eureka:
  client:
    register-with-eureka: true
    fetch-registry: true
    service-url:
      defaultZone: http://eureka7001.com:7001/eureka

```



#### **4.主启动类**

```java

@SpringBootApplication
@EnableEurekaClient
public class PaymentHystrixMain8001 {

    public static void main(String[] args) {
        SpringApplication.run(PaymentHystrixMain8001.class,args);
    }

}


```



#### **5.业务类**

service

```java
@Service
public class PaymentService {

    /**
     * 正常访问
     * @param id
     * @return
     */
    public String paymentInfo_ok(Integer id){
        return "线程池:"+Thread.currentThread().getName()+" paymentInfo_ok, id :"+id+"\t"+"成功";
    }


    public String paymentInfo_timeout(Integer id){
        int time=3;
        try {
            TimeUnit.SECONDS.sleep(time);
        }catch (InterruptedException e){
            e.printStackTrace();
        }
        return "线程池:"+Thread.currentThread().getName()+" paymentInfo_timeout, id :"+id+"\t"+"耗时（秒): "+time;
    }


}

```



controller

```java
@RestController
@Slf4j
public class PaymentController {

    @Resource
    private PaymentService paymentService;

    @Value("${server.port}")
    private String serverPort;

    /**
     * 正常访问
     * @param id
     * @return
     */
    @GetMapping("/payment/hystrix/ok/{id}")
    public String paymentInfo_ok(@PathVariable("id") Integer id){
        String result=paymentService.paymentInfo_ok(id);
        log.info("*******result:" +result);
        return  result;
    }

    /**
     * 超时
     * @param id
     * @return
     */
    @GetMapping("/payment/hystrix/timeout/{id}")
    public String paymentInfo_time(@PathVariable("id") Integer id){
        String result=paymentService.paymentInfo_timeout(id);
        log.info("*******result:" +result);
        return  result;
    }
}

```



#### **6.测试**

6.1启动eureka7001
6.2启动cloud-provider-[hystrix](https://so.csdn.net/so/search?q=hystrix&spm=1001.2101.3001.7020)-payment8001
6.3访问
success的方法：http://localhost:8001/payment/hystrix/ok/{id}







### 5.订单微服务调用支付服务

#### **1.新建cloud-consumer-feign-hystrix-order80**

#### **2.pom文件**

```xml
 <dependencies>

        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-openfeign</artifactId>
        </dependency>

        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-netflix-hystrix</artifactId>
        </dependency>

        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
        </dependency>

        <!--web包-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
        <!--通用包-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>com.atguigu.springcloud</groupId>
            <artifactId>cloud-api-commons</artifactId>
            <version>${project.version}</version>
        </dependency>


```



#### **3.yml文件**

```yaml
server:
  port: 80

eureka:
  client:
    #表示是否将自己注册进eurekaServer 默认为true
    register-with-eureka: false
    service-url:
      defaultZone: http://eureka7001.com:7001/eureka/

```



#### **4.主启动**

```java
@SpringBootApplication
@EnableFeignClients
public class OrderHystrixMain80 {

    public static void main(String[] args) {
        SpringApplication.run(OrderHystrixMain80.class,args);
    }
}


```



#### **5.业务类**

service

```java
@Component
@FeignClient(value = "CLOUD-PROVIDER-HYSTRIX-PAYMENT")
public interface PaymentHystrixService {

    @GetMapping("/payment/hystrix/ok/{id}")
    public String paymentInfo_ok(@PathVariable("id") Integer id);

    @GetMapping("/payment/hystrix/timeout/{id}")
    public String paymentInfo_timeout(@PathVariable("id") Integer id);

}

```



controller

```java
@RestController
@Slf4j
public class OrderHystrixController {

    @Resource
    private PaymentHystrixService paymentHystrixService;


    /**
     * 正常访问
     * @param id
     * @return
     */
    @GetMapping("/consumer/payment/hystrix/ok/{id}")
    public String paymentInfo_ok(@PathVariable("id") Integer id){
        String result=paymentHystrixService.paymentInfo_ok(id);
        return result;
    }

    /**
     * 超时
     * @param id
     * @return
     */
    @GetMapping("/consumer/payment/hystrix/timeout/{id}")
    public String paymentInfo_timeout(@PathVariable("id") Integer id){

        String result=paymentHystrixService.paymentInfo_timeout(id);
        return result;

    }

}


```



#### 6.正常测试

地址：http://localhost/consumer/payment/hystrix/ok/{id}

#### 7.高并发测试

7.1 20000个线程压8001
7.2 消费端80微服务再去访问正常的微服务8001地址
7.3 http://localhost/consumer/payment/hystrix/ok/{id}

故障现象和导致原因
8001同一层次的其它接口服务被困死，因为tomcat线程池里面的工作线程已经被挤占完毕
80此时调用8001,客户端访问响应缓慢，转圈圈



### 6.降级容错解决的维度要求

解决的要求：
1.超时导致服务器变慢
2.出错（宕机或程序运行出错）

解决
1.对方服务(8001)超时了，调用者(80)不能一-直卡死等待,必须有服务降级
2.对方服务(8001 )down机了，调用者(80)不能一-直卡死等待，必须有服务降级
3.对方服务(8001)OK,调用者(80)自己出故障或有自我要求(自己的等待时间小于服务提供者），自己降级处理



### 7.Hystrix之服务降级支付侧fallback

#### **1.服务降级**

降级配置：@ HystrixCommand

#### **2.找出8001存在的问题：**

设置自身调用超时时间的峰值，峰值内可以正常运行,超过了需要有兜底的方法处理，作服务降级fallback

#### **3.8001fallback**

##### 3.1业务类启用

##### 3.1.1超时异常

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200515162433705.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)

@HystrixCommand报异常后如何处理
一旦调用服务方法失败并抛出了错误信息后,会自动调用@HystrixCommand标注好的fallbackMethod调用类中的指定方法@HystrixCommand报异常后如何处理

##### 3.2主启动类激活

添加新注解@ EnableCircuitBreaker

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200515165826956.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)



##### 3.3测试

地址：http://localhost:8001/payment/[hystrix](https://so.csdn.net/so/search?q=hystrix&spm=1001.2101.3001.7020)/timeout/{id}

![在这里插入图片描述](https://img-blog.csdnimg.cn/2020051517005571.png)



##### 3.1.2服务异常

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200515170458371.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)

测试：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200515170606657.png)

**总结**
两个异常：
1.超时异常
2.计算异常
**当前服务不可用了，做服务降级，兜底的方案都是paymentInfo TimeOutHandler**





### 8.Hystrix之服务降级订单侧fallback

80订单微服务，为了更好的保护自己，也可以进行客户端降级保护

#### **1.yml文件**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200518104941614.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)



#### **2.主启动类**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200518105008865.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)



#### **3.业务类**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200518105559313.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)





#### **4.测试**

地址:http://localhost/consumer/payment/hystrix/timeout/{id}

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200518110151351.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)



#### **5.异常**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200518110412285.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)

测试

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200518110437428.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)





### 9.Hystrix之全局服务降级DefaultProperties

**存在的问题：**
1.每个业务方法对应一个兜底的方法，代码膨胀
2.统一和自定义分开



**问题解决**
1.@DefaultProperties(defaultFallback = “)
1: 1每个方法配置一个服务降级方法
1: N除了个别重要核心业务有专属,庀普通的可以通过@DefaultProperties(defaultFallback=“”) 统- -跳转到统- 处理结果页面
通用的和独享的各自分开,避免了代码膨胀，合理减少了代码量

controller配置
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200518141605141.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200518141636442.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)

测试
地址：http://localhost/consumer/payment/[hystrix](https://so.csdn.net/so/search?q=hystrix&spm=1001.2101.3001.7020)/timeout/{id}

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200518141820535.png)





### 10.Hystrix之通配服务降级FeignFallback

#### 要解决的问题：

和业务逻辑混合一块，代码混乱

#### 解决问题

服务降级，客户端去调用服务端，碰.上服务端宕机或关闭

本次案例服务降级处理是在客户端80实现完成的，与服务端8001没有关系
只需要为Feign客户端定义的接口添加一个服务降级处理的实现类即可实现解耦

#### 常见异常

运行时异常
超时异常
宕机


修改cloud-consumer-feign-hystrix- order80

#### 1.重新新建一个类(PaymentFallbackService)实现该接口， 统一为接口里面的方法进行异常处理

#### 2.PaymentFallbackService类实现PaymentFeignClientService接口

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200518143451729.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)



#### **3.yml文件**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200518143506877.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)



#### **4.PaymentFeignClientService接口**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200518143520583.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)



#### **5.测试**

5.1 单个eureka先启动7001
5.2 PaymentHystrixMain8001启动
5.3 正常访问测试
http://localhost/consumer/payment/[hystrix](https://so.csdn.net/so/search?q=hystrix&spm=1001.2101.3001.7020)/ok/{id}

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200518143819884.png)

5.4 故意关闭[微服务](https://so.csdn.net/so/search?q=微服务&spm=1001.2101.3001.7020)8001

此时服务端proyider已经down了，但是我们做了服务降级处理，让客户端在服务端不可用时也会获得提示信息而不会挂起耗死服务器







### 11.Hystrix之服务熔断



#### 11.1 服务熔断理论

**服务熔断**
1.类比保险丝达到最大服务访问后，直接拒绝访问，拉闸限电，然后调用服务降级的方法并返回友好提示
2.就是保险丝 服务的降级->进而熔断->恢复调用链路



**熔断机制概述**
熔断机制是应对雪崩效应的一种微服务链路保护机制。当扇出链路的某个微服务出错不可用或者响应时间太长时,会进行服务的降级，进而熔断该节点微服务的调用，快速返回错误的响应信息。
当检测到该节点微服务调用响应正常后，恢复调用链路。

在Spring Cloud框架里，熔断机制通过Hystrix实现。Hystrix会监控微服务间调用的状况，当失败的调用到一定阈值,缺省是5秒内20次调用失败,就会启动熔断机制。熔断机制的注解是@HystrixCommand.





#### 11.2Hystrix之服务熔断案例

**修改cloud-provider-hystrix-payment8001**
PaymentService

```java
//======================服务熔断===============
    @HystrixCommand(fallbackMethod = "paymentCircuitBreaker_fallback",commandProperties = {
            @HystrixProperty(name="circuitBreaker.enabled",value = "true"),//是否开启断路器
            @HystrixProperty(name="circuitBreaker.requestVolumeThreshold",value = "10"),//请求次数
            @HystrixProperty(name="circuitBreaker.sleepWindowInMilliseconds",value = "10000"),//时间窗口期
            @HystrixProperty(name="circuitBreaker.errorThresholdPercentage",value = "60"),//失败率达到多少后跳闸
    })
    public String paymentCircuitBreaker(@PathVariable("id") Integer id){
        if(id<0){
            throw new RuntimeException("========id不能为负数");
        }
        String serialNumber = IdUtil.simpleUUID();
        return Thread.currentThread().getName()+"调用成功，流水号："+serialNumber;
    }

    public String paymentCircuitBreaker_fallback(@PathVariable("id") Integer id){
        return "id不能为负数，请稍后再试";
    }

```



![在这里插入图片描述](https://img-blog.csdnimg.cn/20200518153639393.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)



PaymentController

```java
  //======================服务熔断===============
    @GetMapping("/payment/circuit/{id}")
    public String paymentCircuitBreaker(@PathVariable("id") Integer id){
        String result = paymentService.paymentCircuitBreaker(id);
        log.info("******result:"+result);
        return result;
    }

```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200518153133861.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)

测试
自测cloud- provider-[hystrix](https://so.csdn.net/so/search?q=hystrix&spm=1001.2101.3001.7020)-payment8001
地址：http://localhost:8001/payment/circuit/{id}
**正确**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200518153706300.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)

**错误**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200518153746637.png)

一次正确一次错误
重点测试
多次错误，然后慢慢正确，发现刚开始不满足条件，就算是正确的访问地址也不能进行

**服务熔断总结**
熔断类型
**1.熔断打开**
请求不再进行调用当前服务，内部设置时钟一般为MTTR (平均故障处理时间)，当打开时长达到所设时钟则进入半熔断状态

**2.熔断关闭**
熔断关闭不会对服务进行熔断

**3.熔断半开**
部分请求根据规则调用当前服务，如果请求成功且符合规则则认为当前服务恢复正常，关闭熔断



**官网断路器流程图**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200518155207141.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)





**官网步骤**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200518154940853.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)





**断路器在什么情况下开始起作用**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200518155003528.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)



**断路器开启或者关闭的条件**
1.当满足一定的阀值的时候(默认10秒内超过20个请求次数)
2.当失败率达到一定的时候(默认10秒内超过50%的请求失败)
3.到达以上阀值，断路器将会开启
4.当开启的时候，所有请求都不会进行转发
5.一段时间之后(默认是5秒) ,这个时候断路器是半开状态，会让其中一个请求进行转发。
6.如果成功，断路器会关闭，若失败，继续开启。重复4和5



**断路器开启后**
1:再有请求调用的时候，将不会调用主逻辑，而是直接调用降级fallback.通过断路器,实现了自动地发现错误并将降级逻辑切换为主逻辑，减少响应延迟的效果。
2:原来的主逻辑要如何恢复呢?
对于这一问题，hytrix也为我们实现了自动恢复功能。
当断路器打开,对主逻辑进行熔断之后，hystrix会启动一 个休眠时间窗，在这个时间窗内,降级逻辑是临时的成为主逻辑，当休眠时间窗到期，断路器将进入半开状态,释放- -次请求到原来的主逻辑上,如果此次请求正常返回,那么断路器将继续闭合,主逻辑恢复，如果这次请求依然有问题，断路器继续进入打开状态，休眠时间窗重新计时。



**All配置**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200518163307424.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)







### 12.Hystrix图形化Dashboard搭建

**服务监控hystrixDashboar**
概述：
除了隔离依赖服务的调用以外，Hystrix还提供 了准实时的调用监控(Hystrix Dashboard) . Hystrix会持续地记录所有通过Hystrix发起的请求的执行信息，并以统计报表和图形的形式展示给用户,包括每秒执行多少请求多少成功,多少失败等。Netflix通过hystrix-metrics-event-stream项目实现了对以上指标的监控。Spring Cloud也提供了Hystrix Dashboard的整合,对监控内容转化成可视化界面。



**仪表盘9001**

#### 1.新建cloud-consumer-hystrix-dashboard9001

#### 2.POM

```xml
  <dependencies>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-netflix-hystrix-dashboard</artifactId>
        </dependency>
        <!--web包-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
        <!--通用包-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>com.atguigu.springcloud</groupId>
            <artifactId>cloud-api-commons</artifactId>
            <version>${project.version}</version>
        </dependency>
    </dependencies>

```



#### 3.YML

```yaml
server:
  port: 9001
```



#### 4.HystrixDashboardMain9001 +新注解@ EnableHystrixDashboard

```java
@SpringBootApplication
@EnableHystrixDashboard
public class HystrixDashboardMain9001 {
    public static void main(String[] args) {
        SpringApplication.run(HystrixDashboardMain9001.class,args);
    }
}
```





#### 5.所有Provider[微服务](https://so.csdn.net/so/search?q=微服务&spm=1001.2101.3001.7020)提供类(8001/8002/8003)都需要监控依赖配置

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210620145507579.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)





#### 6.启动cloud-consumer-hystrix-dashboard9001该微服务后续将监控微服务8001

#### 7.测试

地址：http://localhost:9001/hystrix

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200518165857407.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)







### 13.Hystrix图形化Dashboard监控实战

**断路器演示(服务监控hystrixDashboard)**

#### 1.修改cloud-provider-hystrix-payment8001

注意:新版本Hystrix需要在主启动类MainAppHystrix8001中指定监控路径

```java
 /**
     * 此配置是为了服务监控而配置，与服务容错本身无观，springCloud 升级之后的坑
     * ServletRegistrationBean因为springboot的默认路径不是/hystrix.stream
     * 只要在自己的项目中配置上下面的servlet即可
     *
     * @return
     */
    @Bean
    public ServletRegistrationBean getServlet() {
        HystrixMetricsStreamServlet streamServlet = new HystrixMetricsStreamServlet();
        ServletRegistrationBean<HystrixMetricsStreamServlet> registrationBean = new ServletRegistrationBean<>(streamServlet);
        registrationBean.setLoadOnStartup(1);
        registrationBean.addUrlMappings("/hystrix.stream");
        registrationBean.setName("HystrixMetricsStreamServlet");
        return registrationBean;
    }

```

![在这里插入图片描述](https://img-blog.csdnimg.cn/2021062015000634.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)



报错：404Unable to connect to Command Metric Stream.

#### 2.监控测试

2.1启动1个eureka或者3个eureka集群均可
2.2观察监控窗口
9001监控8001
地址：http://localhost:8001/hystrix.stream

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200518171846510.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)



测试地址：http://localhost:8001/payment/circuit/1
http://localhost:8001/payment/circuit/-1
上述测试通过
先访问正确地址，再访问错误地址，再正确地址，会发现图示断路器都是慢慢放开的

**正确的**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200518172358772.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)



**错误的**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200518172434766.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)



**实心圆:**共有两种含义。它通过颜色的变化代表了实例的健康程度，它的健康度从绿色<黄色<橙色<红色递减。该实心圆除了颜色的变化之外，它的大小也会根据实例的请求流量发生变化,流量越大该实心圆就越大。所以通过该实心圆的展示，就
可以在大量的实例中快速的发现故障实例和高压力实例。
**曲线:**用来记录2分钟内流量的相对变化，可以通过它来观察到流量的上升和下降趋势。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200518172746579.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200518172815328.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)





## 10.GateWay

### 1.简介



**官网：**

上一代zuul X1:https://github.com/Netflix/zuul/wiki

当前gateway：https://cloud.spring.io/spring-cloud-static/spring-cloud-gateway/2.2.1.RELEASE/reference/html



**是什么**
Cloud全家桶中有个很重要的组件就是**网关**，在1.x版本中都是 采用的Zuul网关;
但在2.x版本中，zuul的升级一直跳票, SpringCloud最后自己研发了一个网关替代Zuul,那就是SpringCloud Gateway一句话: gateway是原zuul1.x版的替代

Gateway是在Spring生态系统之上构建的API网关服务,基于Spring 5, Spring Boot 2和Project Reactor等技术。
Gateway旨在提供一 种简单辆有效的方式来对API进行路由，以吸提供一 些强大的过滤器功能，例如:熔断、限流、重试等

SpringCloud Gateway是Spring Cloud的一个全新项目，基纡Spring 5.0+Spring Boot 2.0和Project Reactor等技术开发的网关，它旨在为**微服务**架构提供-种简单有效的统一的API路由管理方式。

SpringCloud Gateway作为Spring Cloud生态系统中的网关,目标是替代Zuul,在Spring Cloud 2.0以上版本中，没有对新版本的Zuul 2.0以上最新高性能版本进行集成，仍然还是使用的Zuul 1.x非Reactor模式的老版本。而为了提升网关的性能，SpringCloud Gateway是基于WebFlux框架实现的，而WebFlux框架底层则使用了高性能的Reactor模式通信框架Netty.

Spring Cloud Gateway的目标提供统一的路由方式且基于Filter 链的方式提供了网关基本的功能，例如:安全,监控/指标,和限流。




**作用**
反向代理
鉴权
流量控制
熔断
日志监控
。。。。。。



**微服务架构中网关在哪里**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200519100308560.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)







### 2.Gateway9527搭建

#### **1.新建Module：cloud-gateway-gateway9527**

#### **2.pom文件**

```xml
<dependencies>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-gateway</artifactId>
        </dependency>
        <!--eureka client-->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
        </dependency>
        <!--通用包-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>com.atguigu.springcloud</groupId>
            <artifactId>cloud-api-commons</artifactId>
            <version>${project.version}</version>
        </dependency>
    </dependencies>
```



#### **3.yml文件**

```yaml
server:
  port: 9527

spring:
  application:
    name: cloud-gateway
  cloud:
    gateway:
      discovery:
        locator:
          enabled: true # 开启从注册中心动态创建路由的功能，利用微服务名称j进行路由
      routes:
        - id: payment_route # 路由的id,没有规定规则但要求唯一,建议配合服务名
          #匹配后提供服务的路由地址
          uri: http://localhost:8001
          predicates:
            - Path=/payment/get/** # 断言，路径相匹配的进行路由
              #- After=2017-01-20T17:42:47.789-07:00[America/Denver]
              #- Before=2017-01-20T17:42:47.789-07:00[America/Denver]
              #- Cookie=username,zzyy
              #- Header=X-Request-Id, \d+ #请求头要有X-Request-Id属性，并且值为正数
              #- Host=**.atguigu.com
              #- Method=GET
              #- Query=username, \d+ # 要有参数名username并且值还要是正整数才能路由
              # 过滤
              #filters:
            #  - AddRequestHeader=X-Request-red, blue
        - id: payment_route2
          uri: http://localhost:8001
          predicates:
            Path=/payment/lb/** #断言,路径相匹配的进行路由

eureka:
  instance:
    hostname: cloud-gateway-service
  client:
    fetch-registry: true
    register-with-eureka: true
    service-url:
      defaultZone: http://eureka7001.com:7001/eureka/
```

#### **4.业务类**

无

#### **5.主启动类**

```java
@SpringBootApplication
@EnableEurekaClient
public class GateWayMain9527 {
    public static void main(String[] args) {
        SpringApplication.run(GateWayMain9527.class,args);
    }
}
```

#### **6.9527网关如何做路由映射**

#### **7.yml新增网关配置**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200520102941645.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)



#### 8.测试

8.1 启动7001
8.2 启动8001
8.3 启动9527网关

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200520103812903.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)



8.4 访问说明
添加网关前：http://localhost:8001/payment/get/1

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200520104016332.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)

添加网关后：http://localhost:9527/payment/get/1

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200520104100166.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)







### 3.Gateway配置路由的两种方式

#### Gateway[网关](https://so.csdn.net/so/search?q=网关&spm=1001.2101.3001.7020)路由有两种配置方式:

**1.在配置文件yml中配置（上一篇博客）**
**2.代码中注入RouteLocator的Bean**
2.1官网案例

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200520104944984.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)

2.2百度国内新闻地址，需要外网
http://new.baidu.com/guonei
2.3自己写一个
百度新闻
业务要求：通过9527网关访问到外网的百度新闻网址
编码：
config

```java
@Configuration
public class GatewayConfig {

    @Bean
    public RouteLocator customRouteLocator(RouteLocatorBuilder routeLocatorBuilder){

        RouteLocatorBuilder.Builder routes=routeLocatorBuilder.routes();

        routes.route("path_route_atguigu",
                r ->r.path("/guonei")
        .uri("http://news.baidu.com/guonei")).build();

        return routes.build();
    }
}
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200520110312420.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)

访问地址：http://localhost:9527/guonei

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200520110422391.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)







### 4.GateWay配置动态路由

**默认情况下Gateway会根据注册中心注册的服务列表,以注册中心上微服务名为路径创建动态路由进行转发,从而实现动态路由的功能**

#### 1.启动：一个eureka7001 +两个服务提供者8001/8002

#### 2.pom文件

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200520111712510.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)

#### 3.yml文件

需要注意的是uri的协议为b，表示启用Gateway的负 载均衡功能。
lb://serviceName是spring cloud
gateway在[微服务](https://so.csdn.net/so/search?q=微服务&spm=1001.2101.3001.7020)中自动为我们创建的负载均衡uri

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200520112203627.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)

#### 4.测试

地址：http://localhost:9527/payment/lb
效果：8001/8002两个端口切换





### 5.GateWay常用的Predicate

**Route Predicate Factories是什么**
Spring Cloud Gateway将路由匹配作为Spring WebFlux HandlerMapping基础[架构](https://so.csdn.net/so/search?q=架构&spm=1001.2101.3001.7020)的一部分。

Spring Cloud Gateway包括许多内置的Route Predicate工厂。所有这些Predicate都与HTTP请求的不同属性匹配。 多个Route Predicate工厂可以进行组合Spring Cloud Gateway创建Route对象时，使用RoutePredicateFactory创建Predicate对象, Predicate对象可以赋值给Route。Spring Cloud Gateway包含许多内置的Route Predicate Factories.

所有这些谓词都匹配HTTP请求的不同属性。多种谓词工厂可以组合,并通过逻辑and.



常用的Route Predicate

1. After Route Predicate
2. Before Route Predicate
3. Between Route Predicate
4. Cookie Route Predicate
5. Header Route Predicate
6. Host Route Predicate
7. Method Route Predicate
8. Path Route Predicate
9. Query Route Predicate





### 6.GateWay的Filter

**是什么：**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200520135355366.png)

路由过滤器可用于修改进入的HTTP请求和返回的HTTP响应，路由过滤器只能指定路由进行使用。
Spring Cloud Gateway内置了多种路由过滤器，他们都由GatewayFilter的工厂 类来产生



生命周期：
1.pre
2.post

种类：

#### 1.GatewayFilter

官网：

```http
https://cloud.spring.io/spring-cloud-static/spring-cloud-gateway/2.2.1.RELEASE/reference/html/#the addrequestparameter-gatewayfilter-factory
```



#### 2.GlobalFilter

**自定义过滤器**
自定义全局GlobalFilter

##### 1.实现两个接口

```java
@Component
@Slf4j
public class MyLogGatewayFilter implements GlobalFilter, Ordered {

    @Override
    public Mono<Void> filter(ServerWebExchange exchange, GatewayFilterChain chain) {
        log.info("come in global filter: {}", new Date());

        ServerHttpRequest request = exchange.getRequest();
        String uname = request.getQueryParams().getFirst("uname");
        if (uname == null) {
            log.info("用户名为null，非法用户");
            exchange.getResponse().setStatusCode(HttpStatus.NOT_ACCEPTABLE);
            return exchange.getResponse().setComplete();
        }
        // 放行
        return chain.filter(exchange);
    }

    /**
     * 过滤器加载的顺序 越小,优先级别越高
     *
     * @return
     */
    @Override
    public int getOrder() {
        return 0;
    }
}
```



![在这里插入图片描述](https://img-blog.csdnimg.cn/20200520141801922.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)

2.测试
启动
正确
http://localhost:9527/payment/lb?uname=111

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200520142141538.png)

错误
http://localhost:9527/payment/lb

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200520142212233.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)





![在这里插入图片描述](https://img-blog.csdnimg.cn/20200520142225495.png)





## 11.Config分布式配置中心

### 1.介绍

**分布式系统面临的问题——配置问题**
微服务章味着要将单体应用中的业务拆分成一个个子服务, 每个服务的粒度相对较小，因此系统中会出现大量的服务。由于每个服务都需要必要的配置信息才能运行，所以一套集中式的、动态的配置管理设施是必不可少的。

SpringCloud提供了ConfigServer来解决这个问题,我们每一个微服务自己带着- 个application.yml, 上百个配置文件的管理… .



**是什么**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200607120532136.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)



SpringCloud Config为微服务架构中的微服务提供集中化的外部配置支持,配置服务器为各个不同微服务应用的所有环境提供了一个中
心化的外部配置。

SpringCloud Config分为服务端和客户端两部分。
服务端也称为分布式配置中心，它是一个独立的微服务应用， 用来连接配置服务器并为客户端提供获取配置信息,加密/解密信息等访问
接口

客户端则是通过指定的配置中心来管理应用资源,以及与业务相关的配置内容,并在启动的时候从配置中心获取和加载配置信息配置服务器默认采用git来存储配置信息,这样就有助于对环境配置进行版本管理，并且可以通过git客户端工具来方便的管理和访问配置内容



作用
1.集中管理配置文件
2.不同环境不同配置，动态化的配置更新，分环境部署比如dev/test/prod/beta/release
3.运行期间动态调整配置，不再需要在每个服务部署的机器上编写配置文件，服务会向配置中心统一拉取配置自己的信息
4.当配置发生变动时，服务不需要重启即可感知到配置的变化并应用新的配置
5.将配置信息以REST接口的形式暴露



**与GitHub整合配置**
由于SpringCloud Config默认使用Git来存储配置文件(也有其它方式，比如支持SVN和本地文件)，但最推荐的还是Git,而且使用的是http/https访问的形式



**官网**
https://cloud.spring.io/spring-cloud-static/spring-cloud-config/2.2.1.RELEASE/reference/html/





### 2.Config配置总控中心搭建

#### **一、Config服务端配置与测试**

1.用你自己的账号在[GitHub](https://so.csdn.net/so/search?q=GitHub&spm=1001.2101.3001.7020)上新建一-个名为springcloud-config的新Repository

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200823211429959.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70#pic_center)



#### 2.由上一步获得刚新建的git地址

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200823211935169.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70#pic_center)









#### 3.本地硬盘目录上新建git仓库并clone

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200823212031519.png#pic_center)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200823212148737.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70#pic_center)

#### 4.新建Module模块cloud-config-center-3344，它即为Cloud的配置中心模块cloudConfig Center

#### 5.pom文件

```xml
<dependencies>
    <!--config server-->
    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-config-server</artifactId>
    </dependency>
    <dependency><!-- 引用自己定义的api通用包，可以使用Payment支付Entity -->
        <groupId>com.eiletxie.springcloud</groupId>
        <artifactId>cloud-api-commons</artifactId>
        <version>${project.version}</version>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
    <!--监控-->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-actuator</artifactId>
    </dependency>
    <!--eureka client-->
    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
    </dependency>
    <!--热部署-->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-devtools</artifactId>
        <scope>runtime</scope>
        <optional>true</optional>
    </dependency>
    <dependency>
        <groupId>org.projectlombok</groupId>
        <artifactId>lombok</artifactId>
        <optional>true</optional>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-test</artifactId>
        <scope>test</scope>
    </dependency>
</dependencies>

```

#### 6.yml文件

```yaml
server:
  port: 3344

spring:
  application:
    name: cloud-config-center
  cloud:
    config:
      server:
        git:
          uri: https://github.com/lin-lx/springcloud-config.git #Github上的git仓库名字
          ##搜索目录.这个目录指的是github上的目录
          search-paths:
            - springcloud-config
      ##读取分支
      label: master

eureka:
  client:
    service-url:
      defaultZone: http://eureka7001.com:7001/eureka/

```

#### 7.主启动类

```java
@SpringBootApplication
@EnableConfigServer
public class ConfigCenterMain3344 {

    public static void main(String[] args) {
        SpringApplication.run(ConfigCenterMain3344.class,args);
    }
}
```

#### 8.windows下修改hosts文件，增加映射（127.0.0.1 config-3344.com

）
C:\Windows\System32\drivers\etc

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200823215734224.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70#pic_center)

#### 9.测试通过Config[微服务](https://so.csdn.net/so/search?q=微服务&spm=1001.2101.3001.7020)是否可以从GitHub,上获取配置内容

启动微服务3344
http://config-3344.com:3344/master/config-dev.yml

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200824205253330.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70#pic_center)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200824205322181.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70#pic_center)







### 3.Config客户端配置与测试

#### 1.新建cloud-config-client-3355

#### 2.pom文件

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-starter-config</artifactId>
    </dependency>
    <dependency><!-- 引用自己定义的api通用包，可以使用Payment支付Entity -->
        <groupId>com.eiletxie.springcloud</groupId>
        <artifactId>cloud-api-commons</artifactId>
        <version>${project.version}</version>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
    <!--监控-->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-actuator</artifactId>
    </dependency>
    <!--eureka client-->
    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
    </dependency>
    <!--热部署-->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-devtools</artifactId>
        <scope>runtime</scope>
        <optional>true</optional>
    </dependency>
    <dependency>
        <groupId>org.projectlombok</groupId>
        <artifactId>lombok</artifactId>
        <optional>true</optional>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-test</artifactId>
        <scope>test</scope>
    </dependency>
</dependencies>
```



#### 3.bootstrap.yml

**是什么**
applicaiton.yml是用户级的资源配置项
bootstrap.ym是系统级的，优先级更加高



Spring Cloud会创建一个“Bootstrap Context”，作为Spring应用的’Application Context的父上下文。初始化的时候，Bootstrap Context负责从外部源加载配置属性并解析配置。这两个上下文共享一个从外部获取的`Environment’。



'Bootstrap属性有高优先级，默认情况下，它们不会被本地配置覆盖。Bootstrap context和Application Context有着不同的约定，所以新增了一个'bootstrap.yml'文件，保证Bootstrap Context’和Application Context’配置的分离。



要将Client模块下的application.yml文件改为bootstrap.yml,这是很关键的，
因为bootstrap.yml是比application.yml先加载的。bootstrap.yml优先级高于application.yml

```yaml
server:
  port: 3355

spring:
  application:
    name: config-client
  cloud:
    #Config客户端配置
    config:
      label: master #分支名称
      name: config #配置文件名称
      profile: dev #读取后缀名称 上诉3个综合就是 master分支上 config-dev.yml
      uri: http://localhost:3344
eureka:
  client:
    service-url:
      defaultZone: http://eureka7001.com:7001/eureka/
```



#### 4.主启动类

```java
@SpringBootApplication
@EnableEurekaClient
public class ConfigClientMain3355 {

    public static void main(String[] args) {
        SpringApplication.run(ConfigClientMain3355.class,args);
    }
}
```



#### 5.业务类

```java
@RestController
public class ConfigClientController {

    // 因为config仓库以rest形式暴露，所以所有客户端都可以通过config服务端访问到github上对应的文件信息
    @Value("${config.info}")
    private String configInfo;

    @GetMapping("/configInfo")
    public String getConfigInfo() {
        return  configInfo;
    }
}
```



#### 6.测试

http://localhost:3355/configInfo

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200824214227206.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70#pic_center)



### 4.Config动态刷新

修改3355模块

#### 1.pom引入actuator监控

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```



#### 2.修改yml，暴露监控端口

```yaml
#暴露监控端点
management:
  endpoints:
    web:
      exposure:
        include: "*"
```



#### 3.业务类controller修改

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200824220145934.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70#pic_center)





#### 4.发送post请求刷新3355

curl -X POST “http://localhost:3355/actuator/refresh”

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200824221003941.png#pic_center)





修改GitHub上的文件，无需重启3355服务，即可刷新

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200824221054713.png#pic_center)

http://localhost:3355/configInfo

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200824221107720.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70#pic_center)



### 5.Bus消息总线

##### **1.什么是bus消息总线**

Spring Cloud Bus配合Spring Cloud Config 使用可以实现配置的动态刷新。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200830195503222.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70#pic_center)



Spring Cloud Bus是用来将[分布式](https://so.csdn.net/so/search?q=分布式&spm=1001.2101.3001.7020)系统的节点与轻量级消息系统链接起来的框架，它整合了Java的事件处理机制和消息中间件的功能。Spring Clud Bus目前支持RabbitMQ和Kafka。



##### **2.作用**

Spring Cloud Bus能管理和传播分布式系统间的消息，就像一个分布式执行器，可用于广播状态更改、事件推送等，也可以当作[微服务](https://so.csdn.net/so/search?q=微服务&spm=1001.2101.3001.7020)间的通信通道。

![在这里插入图片描述](https://img-blog.csdnimg.cn/2020083019583554.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70#pic_center)

##### **3.为什么被称为总线**

什么是总线
在微服务架构的系统中，通常会使用轻量级的消息代理来构建一个共用的消息主题，并让系统中所有微服务实俐都连接上来。由于该主题中产生的消
息会被所有实例监听和消费，所以称它为消息总线。在总线上的各个实例，都可以方便地广播一些需要让其他连接在该主题上的实例都知道的消息。

基本原理
ConfigClient实例都监听MQ中同一个topic(默认是springCloudBus)当一个服务刷新数据的时候，它会把这个信息放入到Topic中，这样其它监听同一Topic的服务就能得到通知，然后去更新自身的配置。



### 6.RabbitMQ安装（win版）

安装Erlang，下载地址:(10.3版本)
http://erlang.org/download/otp_win64_21.3.exe

安装RabbitMQ，下载地址:（3.7.14版本）
https://github.com/rabbitmq/rabbitmq-server/releases/tag/v3.7.14

相关安装方法可参考：
Windows下Erlang和RabbitMQ下载安装教程
https://blog.csdn.net/zmj1049933053/article/details/107321866/





### 7.Bus动态刷新全局应播的设计思想和选型

新建cloud-config-client-3366
pom

```xml
<dependencies>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-bus-amqp</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-config</artifactId>
        </dependency>
        <dependency>
            <groupId>com.atguigu.springcloud</groupId>
            <artifactId>cloud-api-commons</artifactId>
            <version>${project.version}</version>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <!--监控-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
        <!--eureka client-->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
        </dependency>
        <!--热部署-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>
```

bootstrap.yml

```yaml
server:
  port: 3366

spring:
  application:
    name: config-client
  cloud:
    #Config客户端配置
    config:
      label: master #分支名称
      name: config #配置文件名称
      profile: dev #读取后缀名称 上诉3个综合就是 master分支上 config-dev.yml
      uri: http://localhost:3344

  rabbitmq: #rabbitmq相关配置，15672是web管理端口，5672是mq访问端口
    port: 5672
    host: localhost
    username: guest
    password: guest

eureka:
  client:
    service-url:
      defaultZone: http://eureka7001.com:7001/eureka/

#暴露监控端点
management:
  endpoints:
    web:
      exposure:
        include: "*"
```

主启动

```java

@SpringBootApplication
@EnableEurekaClient
public class ConfigClientMain3366 {
    public static void main(String[] args) {
        SpringApplication.run(ConfigClientMain3366.class, args);
    }
}
```

controller

```java
@RestController
@RefreshScope
public class ConfigClientController {

    @Value("${config.info}")
    private String configInfo;

    @GetMapping("/configInfo")
    public String getConfigInfo() {
        return configInfo;
    }
}
```

设计思想：
（1）利用消息总线触发一公客户端/bus/refresh,而刷新所有客户端的配置

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210626103849543.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)

（2）利用消息总线触发一个服务端ConfigServer的/bus/refresh端点，而刷新所有客户端的配置

![在这里插入图片描述](https://img-blog.csdnimg.cn/2021062610403587.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)

图二更合适，图一不合适的原因：
打破了微服务的职责单一性，因为微服务本身是业务模块，它本不应该承担配置刷新的职责。
破坏了微服务各节点的对等性。
有一定的局限性。例如，微服务在迁移时，.它的网络地址常常会发生变化，此时如果想要做到自动刷新，那就会增加更多的修改





### 8.Bus动态刷新全局广播配置实现

#### 一：给cloud-config-center-3344、3355配置中心服务端添加消息总线支持

##### 1.pom

```xml
<dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-bus-amqp</artifactId>
        </dependency>
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201114214054417.png#pic_center)



##### 2.yml

```yaml
server:
  port: 3344

spring:
  application:
    name: cloud-config-center
  cloud:
    config:
      server:
        git:
          #uri: git@github.com:EiletXie/config-repo.git #Github上的git仓库名字
          uri: https://github.com/EiletXie/config-repo.git
          ##搜索目录.这个目录指的是github上的目录
          search-paths:
            - config-repo
      ##读取分支
      label: master
  rabbitmq:
    host: localhost
    port: 5672
    username: guest
    password: guest
eureka:
  client:
    service-url:
      defaultZone: http://eureka7001.com:7001/eureka/

#rabbitmq相关设置 ，暴露 bus刷新配置的端点
management:
  endpoints:
    web:
      exposure:
        include: 'bus-refresh'
```



#### **二：测试**

##### 1.运维工程师

修改[Github](https://so.csdn.net/so/search?q=Github&spm=1001.2101.3001.7020)上配置文件增加版本号
发送POST请求
curl -X POST “http://localhost:3344/actuator/bus-refresh”

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210626105827436.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)

##### 2.配置中心

http://config-3344.com:3344/config-dev.yml

##### 3.客户端

http://localhost:3355/configInfo
http://localhost:3366/configInfo





### 9.Bus动态刷新定点通知

不想全部通知，只想定点通知
指定具体某一个实例生效而不是全部
公式: http://localhost:3344/actuator/bus-refresh/{destination}
/bus/refresh请求不再发送到具体的服务实例上,而是发给config server并通过destination参数类指定需要更新配置的服务或实例

案例：
只通知3355，不通知3366
curl -X POST "http://localhost:3344/actuator/bus-refresh/config-client:3355 "
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210626113232197.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)



修改GitHub上配置文件

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210626113637567.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)

通知3355

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210626113734139.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)

不通知3366

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210626113754286.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70)

## 12.Spring Cloud Stream

**什么是Spring Cloud Stream**
官方定义Spring Cloud Stream是一个构建消息驱动微服务的框架。

应用程序通过inputs或者outputs来与Spring Cloud Stream中binder对象交互.
通过我们配置来binding(绑定)，而Spring Cloud Stream的 binder对象负责与消息中间件交互。所以，我们只需要搞清楚如何与Spring Cloud Stream交互就可以方便使用消息驱动的方式。

通过使用Spring Integration来连接消息代理中间件以实现消息事件驱动。
Spring Cloud Stream为一些供应商的消息中间件产品提供了个性化的自动化配置实现，引用了发布-订阅、消费组、分区的三个核心概念。

目前仅支持**RabbitMQ Kafka**。



官网
大纲级别
https://spring.io/projects/spring-cloud-stream#overview

Spring Cloud Stream是用于构建与共享消息传递系统连接的高度可伸缩的事件驱动微服务框架，该框架提供了一个灵活的编程模型，它建立在已经建立和熟悉的Spring熟语和最佳实践上，包括支持持久化的发布/订阅、消费组以及消息分区这三个核心概念

api级别
https://cloud.spring.io/spring-cloud-static/spring-cloud-stream/3.0.1.RELEASE/reference/html/

Spring Cloud Stream中文指导手册
https://m.wang1314.com/doc/webapp/topic/20971999.html



### 1.Stream的设计思想

#### **设计思想**

标准MQ

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201108225034300.png#pic_center)

1.生产者/消费者之间靠消息媒介传递信息内容（message）
2.消息必须走特定的通道（消息通道MessageChannel
）
3.消息通道里的消息如何被消费呢，谁负责收发处理（消息通道MessageChannel的子接口SubscribableChannel，由MessageHandler消息处理器所订阅）

#### **为什么用Cloud Stream**

比方说我们用到了[RabbitMQ](https://so.csdn.net/so/search?q=RabbitMQ&spm=1001.2101.3001.7020)和Kafka，由于这两个消息中间件的架构上的不同，像RabbitMQ有exchange，kafka有Topic和Partitions分区，

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201108225533955.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70#pic_center)

这些中间件的差异性导致我们实际项目开发给我们造成了一定的困扰，我们如果用了两个消息队列的其中一种，后面的业务需求，我想往另外一种消息队列进行迁移，这时候无疑就是一个灾难性的，一大堆东西都要重新推倒重新做，因为它跟我们的系统耦合了，这时候springcloud Stream给我们提供了一种解耦合的方式。


#### stream为什么可以统一底层差异?

在没有绑定器这个概念的情况下，我们的SpringBoot应用要直接与消息中间件进行信息交互的时候,由于各消息中间件构建的初衷不同，它们的实现细节上会有较大的差异性
通过定义绑定器作为中间层，完美地实现了应用程序与消廪中间件细节之间的隔离。
通过向应用程序暴露统一的Channel通道，使得应用程序不需要再考虑各种不同的消息中间件实现。

通过定义绑定器Binder作为中间层，实现了应用程序与消息中间件细节之间的隔离。


![在这里插入图片描述](https://img-blog.csdnimg.cn/20201108225818926.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70#pic_center)



#### Binder

在没有绑定器这个概念的情况下，我们的SpringBoot应用要直接与消息中间件进行信息交互的时候，由于各消息中间件构建的初衷不同，它们的实现细节上会有较大的差异性.通过定义绑定器作为中间层，完美地实现了应用程序与消息中间件细节之间的隔离。Stream对消息中间件的进一步封装，可以做到代码层面对中间件的无感知，甚至于动态的切换中间件(rabbitmq切换为kafka)，使得微服务开发的高度解耦，服务可以关注更多自己的业务流程


![在这里插入图片描述](https://img-blog.csdnimg.cn/20201108230028205.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70#pic_center)

通过定义绑定器Binder作为中间层，实现了应用程序与消息中间件细节之间的隔离。

INPUT对应于消费者
OUTPUT对应于生产者

#### Stream中的消息通信方式遵循了发布-订阅模式

Topic主题进行广播（在RabbitMQ就是Exchange
，在Kakfa中就是Topic）





### 2.Stream编码常用注解简介

**Spring Cloud Stream标准流程**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201108230554336.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70#pic_center)



1.Binder
很方便的连接中间件，屏蔽差异
2.Channel
通道，是队列Queue的一种抽象，在消息通讯系统中就是实现存储和转发的媒介，通过Channel对队列进行配置
3.Source和Sink
简单的可理解为参照对象是Spring Cloud Stream自身从Stream发布消息就是输出，接受消息就是输入。

**编码API和常用注解**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201108231005625.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDg3MTkzNA==,size_16,color_FFFFFF,t_70#pic_center)



### 3.Binder Implementations 绑定器

通过绑定器Binder作为中间件，实现了应用程序与消息中间件细节的解耦。

Input对应消息生产者

Output对应消息消费者



#### 生产者案例

1. 新建子模块

   cloud-stream-rabbitmq-provider8801 消息生产模块

2. pom

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-actuator</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-starter-stream-rabbit</artifactId>
    </dependency>
    <dependency>
        <groupId>org.projectlombok</groupId>
        <artifactId>lombok</artifactId>
        <optional>true</optional>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-test</artifactId>
        <scope>test</scope>
    </dependency>
</dependencies>
```



3.yml

```yaml
server:
  port: 8801
 
spring:
  application:
    name: cloud-stream-provider
  cloud:
    stream:
      binders: # 在此处配置要绑定的rabbitMQ的服务信息
        defaultRabbit: # 表示定义的名称，用于binding的整合
          type: rabbit # 消息中间件类型
          environment: # 设置rabbitMQ的相关环境配置
            spring:
              rabbitmq:
                host: localhost
                port: 5672
                username: guest
                password: guest
      bindings: # 服务的整合处理
        output: # 这个名字是一个通道的名称
          destination: studyExchange # 表示要使用的exchange名称定义
          content-type: application/json # 设置消息类型，本次为json，文本则设为text/plain
          binder: defaultRabbit # 设置要绑定的消息服务的具体设置
 
eureka:
  client:
    service-url:
      defaultZone: http://eureka7001.com:7001/eureka
  instance:
    lease-renewal-interval-in-seconds: 2 # 设置心跳的间隔时间，默认30
    lease-expiration-duration-in-seconds: 5 # 超过5秒间隔，默认90
    instance-id: send-8801.com # 主机名
    prefer-ip-address: true # 显示ip
```



业务类

1.主启动类

2.MessageProvider接口

```java
public interface IMessageProvider {
    String send();
}
```

3.MessageProviderImpl实现类

```java
public class MessageProviderImpl implements IMessageProvider {
@Override
public String send() {
    return null;
    }
}
```

4.控制层

```java
@RestController
public class SendMessageController {

    @Autowired
    private IMessageProvider messageProvider;

    @GetMapping("/sendMessage")
    public String send() {
        return messageProvider.send();
    }
}
```



5.启动rabbitMQ,7001,8801 访问localhost:8801/sendMessage

返回结果：62b3cb3e-ca40-410e-a601-dc72dfd004b5

![img](https://img-blog.csdnimg.cn/20200311082102106.PNG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyMTA3NDMw,size_16,color_FFFFFF,t_70)







#### 消费者案例

1.新建子模块

cloud-stream-rabbitmq-consumer8802 消息消费模块

2.pom文件同8801

3.yml文件

```yaml
server:
  port: 8802
​
spring:
  application:
    name: cloud-stream-consumer
  cloud:
    stream:
      binders: # 在此处配置要绑定的rabbitMQ的服务信息
        defaultRabbit: # 表示定义的名称，用于binding的整合
          type: rabbit # 消息中间件类型
          environment: # 设置rabbitMQ的相关环境配置
            spring:
              rabbitmq:
                host: localhost
                port: 5672
                username: guest
                password: guest
      bindings: # 服务的整合处理
        input: # 这个名字是一个通道的名称
          destination: studyExchange # 表示要使用的exchange名称定义
          content-type: application/json # 设置消息类型，本次为json，文本则设为text/plain
          binder: defaultRabbit # 设置要绑定的消息服务的具体设置
          # group: spectrumrpcA
​
eureka:
  client:
    service-url:
      defaultZone: http://eureka7001.com:7001/eureka
  instance:
    lease-renewal-interval-in-seconds: 2 # 设置心跳的间隔时间，默认30
    lease-expiration-duration-in-seconds: 5 # 超过5秒间隔，默认90
    instance-id: receive-8802.com #主机名
    prefer-ip-address: true # 显示ip
```



业务类

1.主启动类

2.服务类

```java
/**
 * @ClassName: ReceiveMessageListenerController
 * @description:
 * @author: XZQ
 * @create: 2020/3/10 15:34
 **/
@Component
@EnableBinding(Sink.class)
public class ReceiveMessageListenerController {

    @Value("${server.port}")
    private String serverPort;

    @StreamListener(Sink.INPUT)
    public void input(Message<String> message) {
        System.out.println("消费者1，-------" + message.getPayload() + "\t port:" + serverPort);
    }
 
}
```

启动8802，8801发送消息，可以看到8802可以接受到消息，案例完成。



#### 消息重复消费

原理：微服务应用放置于同一个group中，就能够保证消息只会被其中一个应用消费一次。**不同的组是可以消费的，同一个组内会发生竞争关系，只有其中一个可以消费。**

复制一份跟8802同样的8803

##### 不同组

8802/8803都变成不同组，group两个不同

8802修改YML：

![image-20220322175518532](https://img-blog.csdnimg.cn/img_convert/2f5816b736d6c50a6e54a6fe0572a6b0.png)



8803修改YML：

![image-20220322175605202](https://img-blog.csdnimg.cn/img_convert/ee5028bfb294d0dbb9c5ada55a267dee.png)

​     

我们自己配置：

![image-20220322175755621](https://img-blog.csdnimg.cn/img_convert/5df076017b66325bc52b72873680126f.png)

分布式微服务应用为了实现高可用和负载均衡，实际上都会部署多个实例，本例阳哥启动了两个消费微服务(8802/8803)，多数情况，生产者发送消息给某个具体微服务时只希望被消费一次，按照上面我们启动两个应用的例子，虽然它们同属一个应用，但是这个消息出现了被重复消费两次的情况。为了解决这个问题，在Spring Cloud Stream中提供了消费组的概念

结论：还是重复消费

8802/8803实现了轮询分组，每次只有一个消费者，8801模块的发的消息只能被8802或8803其中一个接收到，这样避免了重复消费

##### ② 同组

8802/8803都变成相同组，group两个相同，都变成 atguiguA

```json
group: atguiguA
```

结论：同一个组的多个微服务实例，每次只会有一个拿到





#### 持久化

通过上述，解决了重复消费问题，再看看持久化

- 停止8802/8803并去除掉8802的分组group: atguiguA，8803的分组group: atguiguA没有去掉
- 8801先发送4条消息到rabbitmq
- 先启动8802，无分组属性配置，后台没有打出来消息
- 再启动8803，有分组属性配置，后台打出来了MQ上的消息

8802控制台：
![image-20220322180553889](https://img-blog.csdnimg.cn/img_convert/8c9b40240041594bde42a8030a83619a.png)



8803控制台：

![image-20220322180645114](https://img-blog.csdnimg.cn/img_convert/04b8658d7ad048672037e38528cb90c3.png)







## 13.SpringCloud Sleuth 分布式请求链路跟踪



#### 一）概述

为什么会出现这个技术？需要解决哪些问题？

在微服务框架中，一个由客户端发起的请求在后端系统中会经过多个不同的的服务节点调用来协同产生最后的请求结果，每一个前段请求都会形成一条复杂的分布式服务调用链路，链路中的任何一环出现高延时或错误都会引起整个请求最后的失败

是什么

官网：https://github.com/spring-cloud/spring-cloud-sleuth

Spring Cloud Sleuth提供了一套完整的服务跟踪的解决方案，在分布式系统中提供追踪解决方案并且兼容支持了zipkin
![image-20220322180945364](https://img-blog.csdnimg.cn/img_convert/925dad05a7880c46e0d8183853054c16.png)







二）搭建链路监控步骤
1、zipkin
SpringCloud从F版起已不需要自己构建Zipkin Server了，只需调用jar包即可

https://repo1.maven.org/maven2/io/zipkin/zipkin-server/

zipkin-server-2.12.9-exec.jar
打开cmd切换到jar包存在路径

```bash
java -jar zipkin-server-2.12.9-exec.jar
```

![image-20220322181520318](https://img-blog.csdnimg.cn/img_convert/91267074c910501cf8517ae398930fd2.png)

运行控制台：http://localhost:9411/zipkin/

术语—完整的调用链路： 表示一请求链路，一条链路通过Trace Id唯一标识，Span标识发起的请求信息，各span通过parent id 关联起来

![image-20220322181811124](https://img-blog.csdnimg.cn/img_convert/b66c066a2ebf28afafae930dc8fe6642.png)





一条链路通过Trace Id唯一标识，Span标识发起的请求信息，各span通过parent id 关联起来

![image-20220322181859871](https://img-blog.csdnimg.cn/img_convert/1566924ba94b4123f54ce2ef10010879.png)





![image-20220322181913301](https://img-blog.csdnimg.cn/img_convert/9e1477ded07e5ca6654259c34c4c91eb.png)



名词解释：

- Trace：类似于树结构的Span集合，表示一条调用链路，存在唯一标识
- span：表示调用链路来源，通俗的理解span就是一次请求信息



### 2、使用

cloud-provider-payment8001

#### 1）改 pom.xml

增加：

```xml
<!--包含了sleuth+zipkin-->
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-zipkin</artifactId>
</dependency>

```

#### 2）改 application.yml

增加：

```yaml
zipkin:
  base-url: http://localhost:9411
sleuth:
  sampler:
    #采样率值介于 0 到 1 之间，1 则表示全部采集
    probability: 1
```

![image-20220322182412645](https://img-blog.csdnimg.cn/img_convert/cce7dae88613fcd6d6c1fdfb6e396de4.png)



#### 3）改业务类 PaymentController

增加：

```java
@GetMapping("/payment/zipkin")
public String paymentZipkin() {
    return "hi ,i'am paymentzipkin server fall back，welcome to atguigu，O(∩_∩)O哈哈~";
}
```



**80端口**pom、yml、maven重复跟8001一样操作，只修改controller文件

```java
/**
 * zipkin+sleuth
 *
 * @return
 */
@GetMapping("/consumer/payment/zipkin")
public String paymentZipkin() {
    String result = restTemplate.getForObject("http://localhost:8001" + "/payment/zipkin/", String.class);
    return result;
}
```



### 3、测试

- 依次启动eureka7001/8001/80
- 80调用8001几次测试下：http://localhost/consumer/payment/get/2
- 打开浏览器访问：http://localhost:9411

![image-20220322190255772](https://img-blog.csdnimg.cn/img_convert/6835767a88b6521b720b234cbe55f276.png)

查看依赖关系

![image-20220322190519137](https://img-blog.csdnimg.cn/img_convert/d0f5d125e7b3faa16e589d1752942f6a.png)



### 4、原理

![image-20220322181811124](https://img-blog.csdnimg.cn/img_convert/90547884c67d41224d7efb08ff68feff.png)









# SpringCloud Alibaba

## 入门简介

### 一）why会出现SpringCloud alibaba

Spring Cloud Netflix项目进入维护模式：https://spring.io/blog/2018/12/12/spring-cloud-greenwich-rc1-available-now

![image-20220322190917289](https://img-blog.csdnimg.cn/img_convert/fd8df798f169fbda4424c8368a8c42ed.png)



Spring Cloud Netflix Projects Entering Maintenance Mode

什么是维护模式？

![image-20220322190943840](https://img-blog.csdnimg.cn/img_convert/a37cd7744d5477cc532251dc69bf8ab8.png)



将模块置于维护模式，意味着 Spring Cloud 团队将不会再向模块添加新功能。我们将修复 block 级别的 bug 以及安全问题，我们也会考虑并审查社区的小型 pull request

进入维护模式意味着什么呢？

进入维护模式意味着 Spring Cloud Netflix 将不再开发新的组件，我们都知道Spring Cloud 版本迭代算是比较快的，因而出现了很多重大ISSUE都还来不及Fix就又推另一个Release了。进入维护模式意思就是目前一直以后一段时间Spring Cloud Netflix提供的服务和功能就这么多了，不在开发新的组件和功能了。以后将以维护和Merge分支Full Request为主

新组件功能将以其他替代平代替的方式实现

![image-20220322191038903](https://img-blog.csdnimg.cn/img_convert/a4d095b0d5d20b724feb4085d72ca3e6.png)





### 二）SpringCloud alibaba带来了什么

#### 1、是什么

官网：https://github.com/alibaba/spring-cloud-alibaba/blob/master/README-zh.md

诞生：2018.10.31，Spring Cloud Alibaba 正式入驻了 Spring Cloud 官方孵化器，并在 Maven 中央库发布了第一个版本


![image-20220322191128049](https://img-blog.csdnimg.cn/img_convert/df03fe252f5d2eac18f6b134a4e8423e.png)



#### 2、能干嘛

服务限流降级：默认支持 Servlet、Feign、RestTemplate、Dubbo 和 RocketMQ 限流降级功能的接入，可以在运行时通过控制台实时修改限流降级规则，还支持查看限流降级 Metrics 监控

服务注册与发现：适配 Spring Cloud 服务注册与发现标准，默认集成了 Ribbon 的支持

分布式配置管理：支持分布式系统中的外部化配置，配置更改时自动刷新

消息驱动能力：基于 Spring Cloud Stream 为微服务应用构建消息驱动能力

阿里云对象存储：阿里云提供的海量、安全、低成本、高可靠的云存储服务。支持在任何应用、任何时间、任何地点存储和访问任意类型的数据

分布式任务调度：提供秒级、精准、高可靠、高可用的定时（基于 Cron 表达式）任务调度服务。同时提供分布式的任务执行模型，如网格任务。网格任务支持海量子任务均匀分配到所有 Worker（schedulerx-client）上执行


### 3、去哪下

https://github.com/alibaba/spring-cloud-alibaba/blob/master/README-zh.md

### 4、怎么玩

![image-20220322191240304](https://img-blog.csdnimg.cn/img_convert/50d84baa501b551b5182a887635aa342.png)



### 三）SpringCloud alibaba学习资料获取

官网：https://spring.io/projects/spring-cloud-alibaba#overview

![image-20220322191431284](https://img-blog.csdnimg.cn/img_convert/1b8075ec67939be310071144cc704597.png)

Spring Cloud Alibaba 致力于提供微服务开发的一站式解决方案。此项目包含开发分布式应用微服务的必需组件，方便开发者通过 Spring Cloud 编程模型轻松使用这些组件来开发分布式应用服务。依托 Spring Cloud Alibaba，您只需要添加一些注解和少量配置，就可以将 Spring Cloud 应用接入阿里微服务解决方案，通过阿里中间件来迅速搭建分布式应用系统。

SpringCloud Alibaba进入了SpringCloud官方孵化器，而且毕业了

英文：

https://github.com/alibaba/spring-cloud-alibaba
https://spring-cloud-alibaba-group.github.io/github-pages/greenwich/spring-cloud-alibaba.html

中文：https://github.com/alibaba/spring-cloud-alibaba/blob/master/README-zh.md



## Nacos服务注册和配置中心

### （一）Nacos简介

#### 1、为什么叫Nacos

前四个字母分别为Naming和Configuration的前两个字母，最后的s为Service



#### 2、是什么

Nacos: Dynamic Naming and Configuration Service 一个更易于构建云原生应用的动态服务发现、配置管理和服务管理平台

Nacos 就是注册中心 + 配置中心的组合 Nacos = Eureka+Config +Bus



#### 3、能干嘛

1. 替代Eureka做服务注册中心
2. 替代Config做服务配置中心





#### 4、去哪下

https://github.com/alibaba/Nacos

官网文档：

https://nacos.io/zh-cn/index.html
https://spring-cloud-alibaba-group.github.io/github-pages/greenwich/spring-cloud-alibaba.html#_spring_cloud_alibaba_nacos_discovery



#### 5、各种注册中心比较

![image-20220322192116429](https://img-blog.csdnimg.cn/img_convert/f38c22041e321d483a4318534addd7a0.png)

据说 Nacos 在阿里巴巴内部有超过 10 万的实例运行，已经过了类似双十一等各种大型流量的考验





### （二）安装并运行Nacos

本地Java8+Maven环境已经OK

先从官网下载Nacos：https://github.com/alibaba/nacos/releases

解压安装包，直接运行bin目录下的startup.cmd

![image-20220322193218894](https://img-blog.csdnimg.cn/img_convert/1af878082b5a86cbe25d183e2b178079.png)

命令运行成功后直接访问：http://localhost:8848/nacos 默认账号密码都是nacos

![image-20220513182002039](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220513182002039.png)





### （三）Nacos作为服务注册中心演示

官网文档：https://spring-cloud-alibaba-group.github.io/github-pages/greenwich/spring-cloud-alibaba.html#_spring_cloud_alibaba_nacos_config



#### 1、基于Nacos的服务提供者9001

新建Module：cloudalibaba-provider-payment9001

##### （1）父 pom.xml

增加：

```xml
<dependency>
    <groupId>com.alibaba.cloud</groupId>
    <artifactId>spring-cloud-alibaba-dependencies</artifactId>
    <version>2.1.0.RELEASE</version>
    <type>pom</type>
    <scope>import</scope>
</dependency>
```



##### （2）本模块 pom.xml

```xml
 <dependencies>
        <!--SpringCloud ailibaba nacos -->
        <dependency>
            <groupId>com.alibaba.cloud</groupId>
            <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
        </dependency>
        <!-- SpringBoot整合Web组件 -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
        <!--日常通用jar包配置-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>
```



##### （3）application.yml

```yaml
server:
  port: 9001

spring:
  application:
    name: nacos-payment-provider
  cloud:
    nacos:
      discovery:
        server-addr: localhost:8848 #配置Nacos地址

management:
  endpoints:
    web:
      exposure:
        include: '*'
```



##### （4）主启动

com.xiaoliu.cloudalibaba.PaymentMain9001

```java
@EnableDiscoveryClient
@SpringBootApplication
public class PaymentMain9001 {
    public static void main(String[] args) {
        SpringApplication.run(PaymentMain9001.class, args);
    }
}
```



##### （5）业务类

com.xiaoliu.cloudalibaba.controller.PaymentController

```java
@RestController
public class PaymentController {
    @Value("${server.port}")
    private String serverPort;

    @GetMapping(value = "/payment/nacos/{id}")
    public String getPayment(@PathVariable("id") Integer id) {
        return "nacos registry, serverPort: " + serverPort + "\t id" + id;
    }
}
```



##### （6）测试

http://localhost:9001/payment/nacos/1

nacos控制台：

![image-20220514133119799](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220514133119799.png)



nacos服务注册中心+服务提供者9001都OK了

为了下一章节演示nacos的负载均衡，参照9001新建9002

新建cloudalibaba-provider-payment9002

或者取巧不想新建重复体力劳动，直接拷贝虚拟端口映射

![image-20220322194841578](https://img-blog.csdnimg.cn/img_convert/9903f4789f41253c1dad45a031d1a083.png)

```java
-DServer.port=9002
```

![image-20220322201838021](https://img-blog.csdnimg.cn/img_convert/8826bc4bf884bd2d18c96d2e919ca91c.png)

![image-20220322201858346](https://img-blog.csdnimg.cn/img_convert/9b8e8d4c73cad399245c0938fddc9fc5.png)



#### 2、基于Nacos的服务消费者83

新建Module：cloudalibaba-consumer-nacos-order83

##### （1）pom.xml

```xml
<dependencies>
        <!--SpringCloud ailibaba nacos -->
        <dependency>
            <groupId>com.alibaba.cloud</groupId>
            <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
        </dependency>
        <!-- 引入自己定义的api通用包，可以使用Payment支付Entity -->
        <dependency>
            <groupId>com.atguigu.springcloud</groupId>
            <artifactId>cloud-api-commons</artifactId>
            <version>${project.version}</version>
        </dependency>
        <!-- SpringBoot整合Web组件 -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
        <!--日常通用jar包配置-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>
```

为什么nacos支持负载均衡？

![image-20220322195454778](https://img-blog.csdnimg.cn/img_convert/1858e28a04e4c42f11ef9def88926361.png)



##### （2）application.yml

```yaml
server:
  port: 83

spring:
  application:
    name: nacos-order-consumer
  cloud:
    nacos:
      discovery:
        server-addr: localhost:8848

#消费者将要去访问的微服务名称(注册成功进nacos的微服务提供者)
service-url:
  nacos-user-service: http://nacos-payment-provider
```





##### （3）主启动

```java
@EnableDiscoveryClient
@SpringBootApplication
public class OrderNacosMain83 {
    public static void main(String[] args) {
        SpringApplication.run(OrderNacosMain83.class, args);
    }
} 
```



##### （4）业务类

###### ① ApplicationContextBean

```java
@Configuration
public class ApplicationContextBean {
    @Bean
    @LoadBalanced
    public RestTemplate getRestTemplate() {
        return new RestTemplate();
    }
}
```





###### ② OrderNacosController

```java
@RestController
public class OrderNacosController {
    @Resource
    private RestTemplate restTemplate;

    @Value("${service-url.nacos-user-service}")
    private String serverURL;

    @GetMapping("/consumer/payment/nacos/{id}")
    public String paymentInfo(@PathVariable("id") Long id) {
        return restTemplate.getForObject(serverURL + "/payment/nacos/" + id, String.class);
    }

}
```



##### （5）测试

nacos控制台：

![image-20220322201922973](https://img-blog.csdnimg.cn/img_convert/88a49a0674eaa3836e3a52e9da7b587d.png)





http://localhost:83/consumer/payment/nacos/1

![image-20220322201957740](https://img-blog.csdnimg.cn/img_convert/a8b76586238e1166b29dabd40674b336.png)

![image-20220322202015749](https://img-blog.csdnimg.cn/img_convert/d62d2878f41ea00da499044116da215a.png)

83访问9001/9002，轮询负载OK







#### 3、服务注册中心对比

Nacos全景图所示：

![image-20220323100012376](https://img-blog.csdnimg.cn/img_convert/ad25aea9e06df0816df5db556e48e51e.png)



Nacos和CAP：

![image-20220323100126191](https://img-blog.csdnimg.cn/img_convert/cb68e9851b8dbe99d3aae41075a35daf.png)

![image-20220323100140809](https://img-blog.csdnimg.cn/img_convert/7d06c215c63f3556293b446d8dce687a.png)

Nacos 支持AP和CP模式的切换：

C是所有节点在同一时间看到的数据是一致的；而A的定义是所有的请求都会收到响应

何时选择使用何种模式？

一般来说，如果不需要存储服务级别的信息且服务实例是通过nacos-client注册，并能够保持心跳上报，那么就可以选择AP模式。当前主流的服务如 Spring cloud 和 Dubbo 服务，都适用于AP模式，AP模式为了服务的可能性而减弱了一致性，因此AP模式下只支持注册临时实例。

如果需要在服务级别编辑或者存储配置信息，那么 CP 是必须，K8S服务和DNS服务则适用于CP模式。CP模式下则支持注册持久化实例，此时则是以 Raft 协议为集群运行模式，该模式下注册实例之前必须先注册服务，如果服务不存在，则会返回错误。

```http
curl -X PUT '$NACOS_SERVER:8848/nacos/v1/ns/operator/switches?entry=serverMode&value=CP'
```







### （四）Nacos作为服务配置中心演示

#### 1、Nacos作为配置中心3377-基础配置

新建 cloudalibaba-config-nacos-client3377

##### （1）pom.xml

```xml
<dependencies>
        <!--nacos-config-->
        <dependency>
            <groupId>com.alibaba.cloud</groupId>
            <artifactId>spring-cloud-starter-alibaba-nacos-config</artifactId>
        </dependency>
        <!--nacos-discovery-->
        <dependency>
            <groupId>com.alibaba.cloud</groupId>
            <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
        </dependency>
        <!--web + actuator-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
        <!--一般基础配置-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>
```



##### （2）两个 yml

why配置两个？

Nacos 同 springcloud-config 一样，在项目初始化时，要保证先从配置中心进行配置拉取，拉取配置之后，才能保证项目的正常启动。

springboot 中配置文件的加载是存在优先级顺序的，bootstrap 优先级高于application

bootstrap.yml

```yaml
# nacos配置
server:
  port: 3377

spring:
  application:
    name: nacos-config-client
  cloud:
    nacos:
      discovery:
        server-addr: localhost:8848 #Nacos服务注册中心地址
      config:
        server-addr: localhost:8848 #Nacos作为配置中心地址
        file-extension: yaml #指定yaml格式的配置


# ${spring.application.name}-${spring.profile.active}.${spring.cloud.nacos.config.file-extension}
```



application.yml

```yaml
spring:
  profiles:
    active: dev # 表示开发环境
```





##### （3）主启动

```java
@EnableDiscoveryClient
@SpringBootApplication
public class NacosConfigClientMain3377 {
    public static void main(String[] args) {
        SpringApplication.run(NacosConfigClientMain3377.class, args);
    }
}
```



##### （4）业务类

```java
@RestController
@RefreshScope //在控制器类加入@RefreshScope注解使当前类下的配置支持Nacos的动态刷新功能。
public class ConfigClientController {
    @Value("${config.info}")
    private String configInfo;

    @GetMapping("/config/info")
    public String getConfigInfo() {
        return configInfo;
    }
}
```



##### （5）在Nacos中添加配置信息

① 理论
Nacos中的dataid的组成格式及与SpringBoot配置文件中的匹配规则

官网：https://nacos.io/zh-cn/docs/quick-start-spring-cloud.html

说明：之所以要配置 spring.application.name，是因为它是构成 Nacos 配置管理 dataId字段的一部分

在 Nacos Spring Cloud 中，dataId 的完整格式如下：（就是说在nacos端我们怎么命名文件的）

```java
${prefix}-${spring.profiles.active}.${file-extension}
```



- prefix 默认为 spring.application.name 的值，也可以通过配置项 spring.cloud.nacos.config.prefix 来配置
- spring.profiles.active 即为当前环境对应的 profile，详情可以参考 Spring Boot文档。 注意：当 spring.profiles.active 为空时，对应的连接符 - 也将不存在，dataId的拼接格式变成 ${prefix}.${file-extension}
- file-exetension 为配置内容的数据格式，可以通过配置项 spring.cloud.nacos.config.file-extension 来配置。目前只支持 properties 和 yaml类型（注意nacos里必须使用yaml）
- 通过 Spring Cloud 原生注解 @RefreshScope 实现配置自动刷新



最后公式：

```java
${spring.application.name}-${spring.profiles.active}.${spring.cloud.nacos.config.file-extension}
```

综合以上说明，和下面的截图，Nacos 的 dataid（类似文件名）应为： nacos-config-client-dev.yaml (必须是yaml)

![image-20220323103313360](https://img-blog.csdnimg.cn/img_convert/8c96c0da96d1e4fca7b4fe6e3030d92c.png)

**② 实操**

配置新增：nacos-config-client-dev.yaml

tips：不要掉了 `.yaml`

```yaml
config:
  info: "config info for dev,from nacos config center."
```

![image-20220323110431533](https://img-blog.csdnimg.cn/img_convert/8a4102f5065445e5ce8990b2e035ed87.png)

![image-20220323110448780](https://img-blog.csdnimg.cn/img_convert/f200691b9827a6b8d9285eb4426fadc9.png)

小总结：

![img](https://img-blog.csdnimg.cn/img_convert/d0029d542053c07cf98b4b05586dc06e.png)

历史配置：Nacos会记录配置文件的历史版本默认保留30天，此外还有一键回滚功能，回滚操作将会触发配置更新

回滚：

![image-20220323110528581](https://img-blog.csdnimg.cn/img_convert/14bd9c2365b38edaee47eb815f2833a4.png)



##### （6）测试

- 启动前需要在 nacos 客户端-配置管理-配置管理栏目下有对应的 yaml 配置文件
- 运行cloud-config-nacos-client3377的主启动类
- 调用接口查看配置信息：http://localhost:3377/config/info

![image-20220323110744293](https://img-blog.csdnimg.cn/img_convert/a4f36132b47f6b6d44b31c1379fe4def.png)

自带动态刷新：修改下Nacos中的yaml配置文件，再次调用查看配置的接口，就会发现配置已经刷新

![image-20220323110853107](https://img-blog.csdnimg.cn/img_convert/7fcae10b79d7015e43dcd9373b5e1975.png)

刷新：

![image-20220323110916166](https://img-blog.csdnimg.cn/img_convert/27a4af3060fd0bd5c006afd8a60d4236.png)





#### 2、Nacos作为配置中心-分类配置

##### （1）问题——多环境多项目管理

问题1：

实际开发中，通常一个系统会准备：dev开发环境、test测试环境、prod生产环境，如何保证指定环境启动时服务能正确读取到Nacos上相应环境的配置文件呢？

问题2：

一个大型分布式微服务系统会有很多微服务子项目，每个微服务项目又都会有相应的开发环境、测试环境、预发环境、正式环境…那怎么对这些微服务配置进行管理呢？


##### （2）Nacos的图形化管理界面

配置管理：

![image-20220323111251204](https://img-blog.csdnimg.cn/img_convert/8a7ba12e003927957b89741f8669469d.png)



命名空间：

![image-20220323111325623](https://img-blog.csdnimg.cn/img_convert/33415edf268d833568953d9348d33bcb.png)



##### （3）Namespace+Group+Data ID三者关系？

思考：为什么这么设计？

① 是什么？

类似Java里面的package名和类名，最外层的namespace是可以用于区分部署环境的，Group和DataID逻辑上区分两个目标对象

② 三者情况

![image-20220323111515475](https://img-blog.csdnimg.cn/img_convert/18dec81d8d12b4033cff3af6ff690b2e.png)



③ 默认情况

Namespace=public，Group=DEFAULT_GROUP，默认Cluster是DEFAULT

Nacos默认的命名空间是public；Namespace主要用来实现隔离，比方说我们现在有三个环境：开发、测试、生产环境，我们就可以创建三个Namespace，不同的Namespace之间是隔离的

Group默认是DEFAULT_GROUP，Group可以把不同的微服务划分到同一个分组里面去

Service就是微服务；一个Service可以包含多个Cluster（集群），Nacos默认Cluster是DEFAULT，Cluster是对指定微服务的一个虚拟划分。比方说为了容灾，将Service微服务分别部署在了杭州机房和广州机房，这时就可以给杭州机房的Service微服务起一个集群名称（HZ），给广州机房的Service微服务起一个集群名称（GZ），还可以尽量让同一个机房的微服务互相调用，以提升性能

最后是Instance，就是微服务的实例





##### （4）三种方案加载配置 Case

###### ① DataID方案

指定spring.profile.active和配置文件的DataID来使不同环境下读取不同的配置

默认空间+默认分组+新建dev和test两个DataID

新建test配置DataID：nacos-config-client-test.yaml

```yaml
config:
  info: "config info for test,from nacos config center."
```

![image-20220323112114934](https://img-blog.csdnimg.cn/img_convert/a7079889df0a47252a5c296badbbee76.png)



通过spring.profile.active属性就能进行多环境下配置文件的读取：

![image-20220323112358412](https://img-blog.csdnimg.cn/img_convert/884457ba58b314ad557da8dd23428f97.png)

测试：http://localhost:3377/config/info

配置是什么就加载什么——test

![image-20220323112518141](https://img-blog.csdnimg.cn/img_convert/28e24a6b6663803c0c6de920e5ac8c21.png)



###### ② Group方案

通过Group实现环境区分，新建Group

**Data ID：**nacos-config-client-info.yaml

**Group：**TEST_GROUP

```yaml
config:
  info: "nacos-config-client-info.yaml,TEST_GROUP,version = v1.0."
```

![image-20220323112959609](https://img-blog.csdnimg.cn/img_convert/30d367d73e00339ecdb51c9d2fd54af4.png)

**Data ID：**nacos-config-client-info.yaml

**Group：**DEV_GROUP

```yaml
config:
  info: "nacos-config-client-info.yaml,DEV_GROUP,version = v1.0."
```

![image-20220323113236868](https://img-blog.csdnimg.cn/img_convert/04c8362afa65a84b1536d1c8228617d9.png)



![image-20220323113342091](https://img-blog.csdnimg.cn/img_convert/5c6b96bd62b9070b6321e71ceec27568.png)

bootstrap+application

![image-20220323113616914](https://img-blog.csdnimg.cn/img_convert/741266fc9eff1855f46f575d1b7f575e.png)

刷新：http://localhost:3377/config/info

![image-20220323113658336](https://img-blog.csdnimg.cn/img_convert/6fa50fc299030ac1da6bed3d62746d69.png)

###### ③ Namespace方案

新建dev/test的Namespace

注意下面的命名空间ID：

![image-20220323113855550](https://img-blog.csdnimg.cn/img_convert/be4946eccdb8357ac8b323317ebd4db1.png)

回到服务管理-服务列表查看

![image-20220323113939684](https://img-blog.csdnimg.cn/img_convert/0d4835160ff1d9e5a7fe77c24374a6e8.png)



按照域名配置填写：

**Data ID：**nacos-config-client-dev.yaml

**Group：**DEFAULT_GROUP

```yaml
config:
  info: "nacos-config-client-dev.yaml,DEFAULT_GROUP,version = v1.0."
```



**Data ID：**nacos-config-client-dev.yaml

**Group：**DEV_GROUP

```yaml
config:
  info: "nacos-config-client-dev.yaml,DEV_GROUP,version = v1.0."
```



**Data ID：**nacos-config-client-dev.yaml

**Group：**TEST_GROUP

```yaml
config:
  info: "nacos-config-client-dev.yaml,TEST_GROUP,version = v1.0."
```



![image-20220323115847249](https://img-blog.csdnimg.cn/img_convert/179e1cb74c2f8c71db145b59c09ad4d9.png)

bootstrap+application：

![image-20220323115258486](https://img-blog.csdnimg.cn/img_convert/5aeebf5104a126785f5341e7bcece788.png)

刷新：http://localhost:3377/config/info

![image-20220323133320733](https://img-blog.csdnimg.cn/img_convert/80631c8961d9f77844a9189b52622242.png)







## Nacos集群和持久化配置

### 1、官网说明

https://nacos.io/zh-cn/docs/cluster-mode-quick-start.html

![image-20220323133720484](https://img-blog.csdnimg.cn/img_convert/a2933c409f2c9e3a43c51fc8c602c7e1.png)



上图官网翻译，真实情况

![image-20220323133755904](https://img-blog.csdnimg.cn/img_convert/8dd07e9c3872c5bd57e916e0e3d29095.png)



说明：

默认Nacos使用嵌入式数据库实现数据的存储。所以，如果启动多个默认配置下的Nacos节点，数据存储是存在一致性问题的。为了解决这个问题，Nacos采用了集中式存储的方式来支持集群化部署，目前只支持MySQL的存储

按照上述，我们需要mysql数据库

官网说明：https://nacos.io/zh-cn/docs/deployment.html

重点说明：

![image-20220323134716536](https://img-blog.csdnimg.cn/img_convert/57d77dcfa695be9efee18cb2ae743758.png)

![image-20220323134436168](https://img-blog.csdnimg.cn/img_convert/b50bbac704f04fc6a79fa280413908ea.png)



### 2、Nacos持久化配置解释

Nacos默认自带的是嵌入式数据库derby：https://github.com/alibaba/nacos/blob/develop/config/pom.xml

derby到mysql切换配置步骤：

nacos-server-1.1.4\nacos\conf目录下找到sql脚本，执行 nacos-mysql.sql


![image-20220323140136905](https://img-blog.csdnimg.cn/img_convert/a749bfb2f4c927408835ec11a4a38a31.png)

- 修改nacos/conf/application.properties文件(切换数据库)，增加支持mysql数据源配置（目前只支持mysql），添加mysql数据源的url、用户名和密码

![image-20220323135619249](https://img-blog.csdnimg.cn/img_convert/fa91ecba1fb747c50c602b3349932161.png)

```cobol
# 切换数据库
spring.datasource.platform=mysql

db.num=1
db.url.0=jdbc:mysql://localhost:3306/nacos_config?characterEncoding=utf8&connectTimeout=1000&socketTimeout=3000&autoReconnect=true
db.user=root
db.password=123456
```

- 访问：http://localhost:8848/nacos，可以看到是个全新的空记录界面，以前是记录进derby

![image-20220323141300144](https://img-blog.csdnimg.cn/img_convert/6ad4c8dc0b51ee4d5a945f0c91dbba54.png)





### 3、Linux版Nacos+MySQL生产环境配置

预计需要，1个Nginx+3个nacos注册中心+1个mysql

##### （1）Nacos下载Linux版

![image-20220323141343546](https://img-blog.csdnimg.cn/img_convert/e1a7e1053b8726a47f05dcba3266cd35.png)



https://github.com/alibaba/nacos/releases/tag/1.1.4

nacos-server-1.1.4.tar.gz

解压后安装：

![image-20220323141408633](https://img-blog.csdnimg.cn/img_convert/9fa9dba681df8ac6c6c016b3e13f44a8.png)







##### （2）集群配置步骤（重点）

###### ① Linux服务器上mysql数据库配置

SQL脚本在哪里



![image-20220323141549792](https://img-blog.csdnimg.cn/img_convert/45b6da782ba5d8f73d0551bca0940bdd.png)



sql语句源文件：nacos-mysql.sql

自己Linux机器上的Mysql数据库粘贴

![image-20220323141618679](https://img-blog.csdnimg.cn/img_convert/9e92519cdcfe415aa4403db1e91c8d58.png)

###### ② application.properties 配置

位置：

![image-20220323141653784](https://img-blog.csdnimg.cn/img_convert/e2c495c6995c40d9b518c2a158c4e916.png)

![image-20220323141704028](https://img-blog.csdnimg.cn/img_convert/9932e17e8a45177ed58c371ef3ffe6d7.png)

内容：

application.properties 文件打开后的最后面，配置如下内容：

```properties
spring.datasource.platform=mysql
 
db.num=1
db.url.0=jdbc:mysql://127.0.0.1:3306/nacos_config?characterEncoding=utf8&connectTimeout=1000&socketTimeout=3000&autoReconnect=true
db.user=root
db.password=root
```

![image-20220323141753696](https://img-blog.csdnimg.cn/img_convert/572ddbf0efb96ae0697de66585adf35b.png)

###### ③ Linux服务器上nacos的集群配置cluster.conf

梳理出3台nacos集器的不同服务端口号

复制出cluster.conf

![image-20220323141837927](https://img-blog.csdnimg.cn/img_convert/bc0f5198ae4363e55aff8a4ab9e7d848.png)

![image-20220323141906906](https://img-blog.csdnimg.cn/img_convert/451af013b10b0c9b6f89f97d2ec3d53f.png)

![image-20220323141932345](https://img-blog.csdnimg.cn/img_convert/7e9ecfac6a4a158cecc3a10ed2bf1850.png)

内容：

![image-20220323141947891](https://img-blog.csdnimg.cn/img_convert/cf1a82f8eb77eb1c9ed00d04c780886b.png)

这个IP不能写127.0.0.1，必须是Linux命令hostname -i能够识别的IP

![image-20220323142008034](https://img-blog.csdnimg.cn/img_convert/7b0c262e58d43076df4e14cb53f8794e.png)



###### ④ 编辑Nacos的启动脚本startup.sh，使它能够接受不同的启动端口

/mynacos/nacos/bin 目录下有startup.sh

在什么地方，修改什么，怎么修改？

/mynacos/nacos/bin 目录下有startup.sh，平时单机版的启动，都是./startup.sh即可。但是集群启动，我们希望可以类似其它软件的shell命令，传递不同的端口号启动不同的nacos实例

命令：./startup.sh -p 3333 表示启动端口号为3333的nacos服务器实例，和上一步的cluster.conf配置的一致

修改内容：


![image-20220323142133647](https://img-blog.csdnimg.cn/img_convert/e9c0a786e3ba2b1f41119e5c4c8be095.png)

修改前：

![image-20220323142155402](https://img-blog.csdnimg.cn/img_convert/5078c3f9ef03921ba27d305b3bb36873.png)

![image-20220323142227641](https://img-blog.csdnimg.cn/img_convert/c6de20b6e46d5d850d3d4a6debf121fc.png)

修改后：

![image-20220323142206985](https://img-blog.csdnimg.cn/img_convert/25dea42d2be66944c23bdee1cc0cd299.png)

![image-20220323142232345](https://img-blog.csdnimg.cn/img_convert/e3b7afd6b21f19f75a816f1ea6ab7f9b.png)



执行方式：

![image-20220323142248748](https://img-blog.csdnimg.cn/img_convert/7ca2a3419b0c4a97baf2a7c807b5af39.png)



###### ⑤ Nginx的配置，由它作为负载均衡器

修改nginx的配置文件：

![image-20220323142336450](https://img-blog.csdnimg.cn/img_convert/477d1d70ec5360e9f3cf6bf7517d1784.png)

nginx.conf：

```bash
upstream cluster{
        server 127.0.0.1:3333;
        server 127.0.0.1:4444;
        server 127.0.0.1:5555;
    }
```

```bash
server {
        listen       1111;
        server_name  localhost;
        #charset koi8-r;
        #access_log  logs/host.access.log  main;
        location / {
            #root   html;
            #index  index.html index.htm;
            proxy_pass http://cluster;
        }
.......省略
```

![image-20220323142437877](https://img-blog.csdnimg.cn/img_convert/92aa1105531f01119ea6c1783ca5094c.png)

按照指定启动：

![image-20220323142517545](https://img-blog.csdnimg.cn/img_convert/d684c395535ff1c9abdea69f4f3e5933.png)



###### ⑥ 截止到此处，1个Nginx+3个nacos注册中心+1个mysql

测试通过nginx访问nacos：http://192.168.111.144:1111/nacos/#/login

新建一个配置测试：

![image-20220323142601613](https://img-blog.csdnimg.cn/img_convert/9f5dbcec70f568fddc4a72381c0ad3e3.png)

linux服务器的mysql插入一条记录：

![image-20220323142620678](https://img-blog.csdnimg.cn/img_convert/68807b32e2a86c6e389a058e36fa3297.png)



##### （3）测试

微服务cloudalibaba-provider-payment9002启动注册进nacos集群

```yaml
server:
  port: 9002

spring:
  application:
    name: nacos-payment-provider
  cloud:
    nacos:
      discovery:
        #配置Nacos地址
        #server-addr: localhost:8848
        # 换成nginx的1111端口，做集群
        server-addr: 192.168.111.144:1111


management:
  endpoints:
    web:
      exposure:
        include: '*'
```



结果：

![image-20220323142809485](https://img-blog.csdnimg.cn/img_convert/65ee3cd8f3af3a6efe4d4c43bb1b92a3.png)



### 4、高可用小总结

![image-20220323142830346](https://img-blog.csdnimg.cn/img_convert/67c2c5a55a69da4d9eaac6a49ba61699.png)









## SpringCloud Alibaba Sentinel 实现熔断与限流

### （一）概述

官网：https://github.com/alibaba/Sentinel

中文：https://github.com/alibaba/Sentinel/wiki/%E4%BB%8B%E7%BB%8D

#### 1、是什么

一句话解释，之前我们讲解过的Hystrix

![image-20220323143025709](https://img-blog.csdnimg.cn/img_convert/4aed028fad9cfeb0705e3f3e2f3e3366.png)



#### 2、去哪下

https://github.com/alibaba/Sentinel/releases

![image-20220323143055298](https://img-blog.csdnimg.cn/img_convert/c104113bc0c3683669183eab2a3e85f0.png)



#### 3、能干嘛

![image-20220323143105095](https://img-blog.csdnimg.cn/img_convert/89905b5312f1cfd4915430537b9b9bd5.png)



#### 4、怎么玩

https://spring-cloud-alibaba-group.github.io/github-pages/greenwich/spring-cloud-alibaba.html#_spring_cloud_alibaba_sentinel

服务使用中的各种问题：

- 服务雪崩
- 服务降级
- 服务熔断
- 服务限流



### （二）安装Sentinel控制台

sentinel组件由两部分构成：

核心库（Java 客户端）不依赖任何框架/库，能够运行于所有 Java 运行时环境，同时对 Dubbo / Spring Cloud 等框架也有较好的支持
控制台（Dashboard）基于 Spring Boot 开发，打包后可以直接运行，不需要额外的 Tomcat 等应用容器
后台 + 前台8080

安装步骤：
下载：https://github.com/alibaba/Sentinel/releases，下载到本地 sentinel-dashboard-1.7.1.jar

前提：java8环境OK + 8080端口不能被占用

运行命令：java -jar sentinel-dashboard-1.7.1.jar

![image-20220323143710437](https://img-blog.csdnimg.cn/img_convert/47bb4981c85e1bc00d07f8d88e750648.png)

访问sentinel管理界面：http://localhost:8080，登录账号密码均为sentinel

![image-20220323143825731](https://img-blog.csdnimg.cn/img_convert/fef86e0e2f1c0b8620d4e35c15b4ea01.png)



### （三）初始化演示工程

启动Nacos8848成功：http://localhost:8848/nacos/#/login

新建 cloudalibaba-sentinel-service8401

#### 1、pom.xml

```xml
<dependencies>
        <!--SpringCloud ailibaba nacos -->
        <dependency>
            <groupId>com.alibaba.cloud</groupId>
            <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
        </dependency>
        <!--SpringCloud ailibaba sentinel-datasource-nacos 后续做持久化用到-->
        <dependency>
            <groupId>com.alibaba.csp</groupId>
            <artifactId>sentinel-datasource-nacos</artifactId>
        </dependency>
        <!--SpringCloud ailibaba sentinel -->
        <dependency>
            <groupId>com.alibaba.cloud</groupId>
            <artifactId>spring-cloud-starter-alibaba-sentinel</artifactId>
        </dependency>
        <!--openfeign-->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-openfeign</artifactId>
        </dependency>
        <!-- SpringBoot整合Web组件+actuator -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
        <!--日常通用jar包配置-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>cn.hutool</groupId>
            <artifactId>hutool-all</artifactId>
            <version>4.6.3</version>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>

    </dependencies>
```



#### 2、application.yml

```yaml
server:
  port: 8401

spring:
  application:
    name: cloudalibaba-sentinel-service
  cloud:
    nacos:
      discovery:
        #Nacos服务注册中心地址
        server-addr: localhost:8848
    sentinel:
      transport:
        #配置Sentinel dashboard地址
        dashboard: localhost:8080
        #默认8719端口，假如被占用会自动从8719开始依次+1扫描,直至找到未被占用的端口
        port: 8719

management:
  endpoints:
    web:
      exposure:
        include: '*'
```



#### 3、主启动

```java
@EnableDiscoveryClient
@SpringBootApplication
public class SentinelMainApp8401 {
    public static void main(String[] args) {
        SpringApplication.run(SentinelMainApp8401.class, args);
    }
}
```



#### 4、业务类FlowLimitController

```java
@RestController
public class FlowLimitController {

    @GetMapping("/testA")
    public String testA() {
        return "------testA";
    }

    @GetMapping("/testB")
    public String testB() {
        return "------testB";
    }
}
```



#### 5、测试

- 启动Sentinel8080：java -jar sentinel-dashboard-1.7.0.jar
- 启动微服务8401
- 启动8401微服务后查看sentienl控制台

空空如也，啥都没有

Sentinel采用的懒加载说明：

执行一次访问即可：http://localhost:8401/testA、http://localhost:8401/testB

![image-20220323145628467](https://img-blog.csdnimg.cn/img_convert/3bb718ae521317e53e733026ad782551.png)



结论：sentinel8080正在监控微服务8401



### （四）流控规则

#### 1、基本介绍

![image-20220323145829338](https://img-blog.csdnimg.cn/img_convert/2e4c175346a2defa51e3ab09aaaeff42.png)



解释说明：

- 资源名：唯一名称，默认请求路径

- 针对来源：sentinel可以针对调用者进行限流，填写微服务名，默认default（不区分来源）

- 阈值类型/单机值：

  - QPS（每秒钟的请求数量）：当调用该api就QPS达到阈值的时候，进行限流

  - 线程数．当调用该api的线程数达到阈值的时候，进行限流

- 是否集群：不需要集群

- 流控模式：

  - 直接：api达到限流条件时，直接限流。分为QPS和线程数

  - 关联：当关联的资到阈值时，就限流自己。别人惹事，自己买单

  - 链路：只记录指定链路上的流量（指定资源从入口资源进来的流量，如果达到阈值，就进行限流）【api级别的针对来源】

- 流控效果：

  - 快速失败：直接抛异常
  - warm up：根据codeFactor（冷加载因子，默认3）的值，从阈值codeFactor，经过预热时长，才达到设置的QPS阈值
  - 排队等待：匀速排毒，让请求以匀速通过，阈值类型必须设置为QPS，否则无效

- QPS和线程数的区别：

  - QPS 类似于银行的保安：所有的请求到Sentinel 后，他会根据阈值放行，超过报错

  - 线程数类似于银行的窗口：所有的请求会被放进来，但如果阈值设置为1，那么其他的请求就会报错也就是，银行里只有一个窗口，一个人在办理业务中，其他人跑过来则会告诉你“现在不行，没到你”

![在这里插入图片描述](https://img-blog.csdnimg.cn/2cb7532ab5b34073bdddaab382414a8e.png)

**重要属性：**

|      Field      |                             说明                             |           默认值            |
| :-------------: | :----------------------------------------------------------: | :-------------------------: |
|    resource     |              资源名，资源名是限流规则的作用对象              |                             |
|      count      |                           限流阈值                           |                             |
|      grade      |       限流阈值类型，QPS 模式（1）或并发线程数模式（0）       |          QPS 模式           |
|    limitApp     |                      流控针对的调用来源                      | default，代表不区分调用来源 |
|    strategy     |              调用关系限流策略：直接、链路、关联              |    根据资源本身（直接）     |
| controlBehavior | 流控效果（直接拒绝/WarmUp/匀速+排队等待），不支持按调用关系限流 |          直接拒绝           |
|   clusterMode   |                         是否集群限流                         |             否              |



#### 2、流控模式

##### （1）直接（默认）

- 直接->快速失败：系统默认
- 配置及说明：表示1秒钟内查询1次就是OK，若超过次数1，就直接-快速失败，报默认错误

![image-20220323150201131](https://img-blog.csdnimg.cn/img_convert/e5b33a4fd890b19541be3cd94f3da7b6.png)

![image-20220323150409267](https://img-blog.csdnimg.cn/img_convert/371e4ba57176e0dfbcf16cd140f3ec88.png)

测试：快速点击访问：http://localhost:8401/testA

结果：Blocked by Sentinel (flow limiting)

![image-20220323150346997](https://img-blog.csdnimg.cn/img_convert/a9d88b4d1c543de90ecec3d48be17be9.png)

思考？？？

直接调用默认报错信息，技术方面OK，但是否应该有我们自己的后续处理？类似有个fallback的兜底方法？

##### （2）关联

- 当关联的资源达到阈值时，就限流自己
- 当与A关联的资源B达到阀值后，就限流A自己
- B惹事，A挂了

配置A：设置效果，当关联资源/testB的qps阀值超过1时，就限流/testA的Rest访问地址，当关联资源到阈值后限制配置好的资源名


![image-20220323150636586](https://img-blog.csdnimg.cn/img_convert/56abdc1970d3435f846e6b149c09263a.png)

测试：

访问testB成功：

![image-20220323152120040](https://img-blog.csdnimg.cn/img_convert/3089727542cfcde3d26ffb4c6fc70d65.png)

postman里新建多线程集合组：

![image-20220323152235062](https://img-blog.csdnimg.cn/img_convert/4642ec03ccb55c1ce183432903ca028c.png)

将访问地址添加进新新线程组：

![image-20220323152333645](https://img-blog.csdnimg.cn/img_convert/3ff7c2fc5b3d533d45ae0641e11e78b2.png)

Run：

![image-20220323152427426](https://img-blog.csdnimg.cn/img_convert/fec836ed795837d9b34189471c8f738d.png)

![image-20220323152530854](https://img-blog.csdnimg.cn/img_convert/aac9f5785cadc181670930331a4f4506.png)

运行后发现testA挂了，点击访问：http://localhost:8401/testA，结果：Blocked by Sentinel (flow limiting)

##### （3）链路【尝试失败】

链路模式：只针对从指定链路访问到本资源的请求做统计，判断是否超过阈值

例如有两条请求链路：

- /test1 /common

- /test2 /common

如果只希望统计从/test2进入到/common的请求，对/test2 进行限流，则可以这样配置：


![image-20220323171559605](https://img-blog.csdnimg.cn/img_convert/0ae2d3d5ad009fe1bedbdf0457899c27.png)

注意有个大坑：https://blog.csdn.net/qq_31155349/article/details/108478190

```tex
从1.6.3 版本开始，Sentinel Web filter默认收敛所有URL的入口context，因此链路限流不生效。1.7.0 版本开始（对应SCA的2.1.1.RELEASE)，官方在CommonFilter 引入了WEB_CONTEXT_UNIFY 参数，用于控制是否收敛context。将其配置为 false 即可根据不同的URL 进行链路限流。SCA 2.1.1.RELEASE之后的版本，可以通过配置spring.cloud.sentinel.web-context-unify=false即可关闭收敛，我们当前使用的版本是SpringCloud Alibaba 2.1.0.RELEASE，无法实现链路限流。目前官方还未发布SCA 2.1.2.RELEASE，所以我们只能使用2.1.1.RELEASE，需要写代码的形式实现
```

我们使用的版本：

![image-20220323175347809](https://img-blog.csdnimg.cn/img_convert/3b71554671b5c76310f4a6e4b2998924.png)

上面这段是从百度down下来的，经过测试，SCA换成最新版本2.2.1.RELEASE仍然无效：配置spring.cloud.sentinel.web-context-unify=false无效！！！

推荐做法仍然是关闭官方的CommonFilter实例化，自己手动实例化CommonFilter，设置WEB_CONTEXT_UNIFY=false

```yaml
spring:
    cloud:
        sentinel:
            filter:
                enabled: false
```

【未解决】

**案例：流控模式-链路**

需求：有查询订单和创建订单业务，两者都需要查询商品。针对从查询订单进入到查询商品的请求统计，并设置限流

步骤：

1. 在OrderService中添加一个queryGoods方法，不用实现业务
2. 在OrderController中，创建/order/query端点，调用OrderService中的queryGoods方法(/order/query -> queryGoods)
3. 在OrderController中，创建/order/save端点，调用OrderService的queryGoods方法(/order/save -> queryGoods)
4. 给queryGoods设置限流规则，从/order/query进入queryGoods的方法限制QPS必须小于2**（设置/order/query qqs<2）**

Sentinel默认只标记Controller中的方法为资源，如果要标记其它方法，需要利用@SentinelResource注解，示例：

```java
@SentinelResource("goods")
public void queryGoods(){
    System.err.println("查询商品");
}
```

Sentinel默认会将Controller方法做context整合，导致链路模式的流控失效，需要修改application.yml，添加配置：

```yaml
spring:
  cloud:
    sentinel:
      transport:
        dashboard: localhost:8080 # sentinel控制台地址
      web-context-unify: false # 关闭context整合
```

![image-20220323174132581](https://img-blog.csdnimg.cn/img_convert/06064d27aa9449bc02b81e710e37eeec.png)

访问/order/query、/order/save资源

- http://localhost:8088/order/query：##触发链路限流
- http://localhost:8088/order/save：不会触发链路限流



#### 3、流控效果

##### （1）快速失败（默认的流控处理）

直接失败，抛出异常：Blocked by Sentinel (flow limiting)

源码：com.alibaba.csp.sentinel.slots.block.flow.controller.DefaultController

##### （2）预热

官网：https://github.com/alibaba/Sentinel/wiki/%E6%B5%81%E9%87%8F%E6%8E%A7%E5%88%B6


![image-20220323153241843](https://img-blog.csdnimg.cn/img_convert/3f23c5db83c21058357fd42e4d4751c8.png)

默认coldFactor为3，即请求 QPS 从 threshold / 3 开始，经预热时长逐渐升至设定的 QPS 阈值

限流冷启动：https://github.com/alibaba/Sentinel/wiki/%E9%99%90%E6%B5%81—%E5%86%B7%E5%90%AF%E5%8A%A8

源码：com.alibaba.csp.sentinel.slots.block.flow.controller.WarmUpController

![image-20220323153556079](https://img-blog.csdnimg.cn/img_convert/4600f72d4bc235fa1915214b5a3e66cf.png)



WarmUp配置：

默认 coldFactor 为 3，即请求QPS从(threshold / 3) 开始，经多少预热时长才逐渐升至设定的 QPS 阈值

案例，阀值为10+预热时长设置5秒

系统初始化的阀值为10 / 3 约等于3，即阀值刚开始为3；然后过了5秒后阀值才慢慢升高恢复到10，效果为：开始访问 http://localhost:8401/testB 时每秒请求别超过10/3个才能正常访问，5秒后可以接受的请求可以达到每秒10次

![image-20220323153932479](https://img-blog.csdnimg.cn/img_convert/97e8ad9fdb841b973f643dca58237c31.png)

多次点击：http://localhost:8401/testB

刚开始不行，后续慢慢OK

应用场景：

秒杀系统在开启的瞬间，会有很多流量上来，很有可能把系统打死，预热方式就是把为了保护系统，可慢慢的把流量放进来，慢慢的把阀值增长到设置的阀值



##### （3）排队等待

匀速排队，让请求以均匀的速度通过，阀值类型必须设成QPS，否则无效

设置含义：/testA每秒1次请求，超过的话就排队等待，等待的超时时间为20000毫秒

如下此设置的含义为：代表 1 秒匀速的通过 2 个请求，也就是每个请求平均间隔恒定为 1 / 2 = 0.5 s 也即 500 ms，每一个请求的最长等待时间为20s

同理，如果单机阈值为 1 时，每个请求的平均间隔恒定为 1000/1 = 10000 ms


![image-20220323192430204](https://img-blog.csdnimg.cn/img_convert/5ed5ed06ecfdfea28a4cde0a06182bab.png)

说明：匀速排队，阈值必须设置为QPS

官网：https://github.com/alibaba/Sentinel/wiki/%E6%B5%81%E9%87%8F%E6%8E%A7%E5%88%B6

![image-20220323154314829](https://img-blog.csdnimg.cn/img_convert/0382eefb01107470754696aa739fa9ea.png)

源码：com.alibaba.csp.sentinel.slots.block.flow.controller.RateLimiterController

测试：

![image-20220323193030705](https://img-blog.csdnimg.cn/img_convert/9bd292c299cf73cc0f534dab28d0a703.png)

阈值为2时：

![image-20220323192403691](https://img-blog.csdnimg.cn/img_convert/4824077ba5296648bde2b4536cf4c582.png)

阈值为1时：

![image-20220323192847700](https://img-blog.csdnimg.cn/img_convert/bf255f51a2f52fbddf9945d6a58233ff.png)



### （五）降级规则

官网：https://github.com/alibaba/Sentinel/wiki/%E7%86%94%E6%96%AD%E9%99%8D%E7%BA%A7

#### 1、介绍

![image-20220323155804020](https://img-blog.csdnimg.cn/img_convert/99d0c0d817cd2fcc2aa2472c99158dde.png)

RT（平均响应时间，秒级）

- 平均响应时间**超出阈值**且**在时间窗口内通过的请求>=5**，两个条件同时满足后触发降级
- 窗口期过后关闭断路器
- RT最大4900（更大的需要通过-Dcsp.sentinel.statistic.max.rt=XXXX才能生效）

异常比列（秒级）

- **QPS >= 5**且**异常比例（秒级统计）超过阈值时**，触发降级；时间窗口结束后，关闭降级

异常数（分钟级）

- 异常数（分钟统计）超过阈值时，触发降级；时间窗口结束后，关闭降级

进一步说明：

Sentinel 熔断降级会在调用链路中某个资源出现不稳定状态时（例如调用超时或异常比例升高），对这个资源的调用进行限制，让请求快速失败，避免影响到其它的资源而导致级联错误

当资源被降级后，在接下来的降级时间窗口之内，对该资源的调用都自动熔断（默认行为是抛出 DegradeException）

Sentinel 的断路器是没有半开状态的：

半开的状态系统自动去检测是否请求有异常，没有异常就关闭断路器恢复使用；有异常则继续打开断路器不可用。具体可以参考Hystrix



#### 2、RT

##### （1）介绍

![image-20220323160241638](https://img-blog.csdnimg.cn/img_convert/c4625b8675b290ed6fb57d6bce8ed65f.png)

![image-20220323160504510](https://img-blog.csdnimg.cn/img_convert/59930488a01c10c5640fa347a98dc10a.png)



##### （2）实操

在controller中加入textC：

```java
@GetMapping("/testC")
public String testC() {
    //暂停几秒钟线程
    try {
        TimeUnit.SECONDS.sleep(1);
    } catch (InterruptedException e) {
        e.printStackTrace();
    }
    log.info("testC 测试RT");
    return "------testC";
}
```



配置：

![image-20220323160920116](https://img-blog.csdnimg.cn/img_convert/b206e372436eef0e7d69d12d5d5cb1e7.png)

jmeter压测：

![image-20220323161349348](https://img-blog.csdnimg.cn/img_convert/941cc60ec8220db0753f422922368c7f.png)

压测时再访问 /testC

![image-20220323193614484](https://img-blog.csdnimg.cn/img_convert/e4f3b5a97f18b81688ad9b26403b69cd.png)

停止压测后：

![image-20220323193713925](https://img-blog.csdnimg.cn/img_convert/63d9a1298a237dda49dc0276c0ef9669.png)



结论：

按照上述配置，永远一秒钟打进来10个线程（大于5个了）调用testC，我们希望200毫秒处理完本次任务，如果超过200毫秒还没处理完，在未来1秒钟的时间窗口内，断路器打开(保险丝跳闸)微服务不可用，保险丝跳闸断电了，后续我停止jmeter，没有这么大的访问量了，断路器关闭(保险丝恢复)，微服务恢复OK



#### 3、异常比例

##### （1）介绍

![image-20220323161738085](https://img-blog.csdnimg.cn/img_convert/beb78bedd59adf4b7334c910719922d2.png)

![image-20220323161743863](https://img-blog.csdnimg.cn/img_convert/cf6a5c0a1323e781dd04fb3d15a19b30.png)



##### （2）实操

在controller中加入textD：

```java
@GetMapping("/testD")
public String testD() {
    log.info("testD 测试RT");
    int age = 10 / 0;
    return "------testD";
}
```



配置

![image-20220323161939354](https://img-blog.csdnimg.cn/img_convert/882fd67003a1103b944055436a53ed24.png)

单独一次访问：http://localhost:8401/testD

![image-20220323194543546](https://img-blog.csdnimg.cn/img_convert/9cf0949e652a8f70ddd8dff46fd205f4.png)



开启 jmeter 压测后再次访问：



![image-20220323194532214](https://img-blog.csdnimg.cn/img_convert/fbcfd6186ac592a97f0df1e23e1c8b98.png)

此时的压测还未停止：

![image-20220323194515805](https://img-blog.csdnimg.cn/img_convert/fd376da24b0a35026c477f268b9cf6fa.png)



![image-20220323170720421](https://img-blog.csdnimg.cn/img_convert/de234ae676168ffe316ba8fba7564d69.png)

当停止压测后：

![img](https://img-blog.csdnimg.cn/img_convert/de7510462a3b828e697f19db39cedb32.png)



##### （3）结论

按照上述配置，单独访问一次，必然来一次报错一次(int age = 10/0)，调一次错一次；开启jmeter后，直接高并发发送请求，多次调用达到我们的配置条件了。
断路器开启(保险丝跳闸)，微服务不可用了，不再报错error而是服务降级了





#### 4、异常数

##### （1）介绍

**时间窗口一定要大于等于60秒、异常数是按照分钟统计的**

![image-20220323162208655](https://img-blog.csdnimg.cn/img_convert/b28f2a9a2cc21091cf6cf996be46d1ec.png)

![image-20220323162249143](https://img-blog.csdnimg.cn/img_convert/1bd5266441ff3c9f2cc05c8aa90f8fe5.png)



##### （2）实战

在controller中加入textE：

```java
@GetMapping("/testE")
public String testE() {
    log.info("testE 测试异常比例");
    int age = 10 / 0;
    return "------testE 测试异常比例";
}
```



配置：

![image-20220323162453116](https://img-blog.csdnimg.cn/img_convert/3cc51038f6a2f353bacb46e7f565a1b1.png)

访问：http://localhost:8401/testE，第一次访问绝对报错，因为除数不能为零，我们看到error窗口，但是达到5次报错后，进入熔断后降级

第一次访问：

![image-20220323194645532](https://img-blog.csdnimg.cn/img_convert/0d56158c8279210a758c9c7d0c44aaf8.png)

jmeter压测：

![image-20220323162533138](https://img-blog.csdnimg.cn/img_convert/454e0b5d717e4896b4f77e340085e4d8.png)

此时再访问：

![image-20220323194745727](https://img-blog.csdnimg.cn/img_convert/b0782aef6722ba207c660e75ea496a93.png)

当压测停止后：

![image-20220323194645532](https://img-blog.csdnimg.cn/img_convert/f85fa04f06f182ef55e94bb659abcb65.png)





### （六）热点key限流

#### 1、基本介绍

何为热点：热点即经常访问的数据，很多时候我们希望统计或者限制某个热点数据中访问频次最高的TopN数据，并对其访问进行限流或者其它操作

官网：https://github.com/alibaba/Sentinel/wiki/%E7%83%AD%E7%82%B9%E5%8F%82%E6%95%B0%E9%99%90%E6%B5%81

承上启下复习start：

兜底方法：分为系统默认和客户自定义两种

- 之前的case，限流出问题后，都是用sentinel系统默认的提示：Blocked by Sentinel (flow limiting)

- 我们能不能自定？类似hystrix，某个方法出问题了，就找对应的兜底降级方法？


结论：从 HystrixCommand 到 **@SentinelResource**


#### 2、实操

在controller中加入：

```java
@GetMapping("/testHotKey")
@SentinelResource(value = "testHotKey", blockHandler = "dealHandlerTestHotKey")
public String testHotKey(@RequestParam(value = "p1", required = false) String p1,
                         @RequestParam(value = "p2", required = false) String p2) {
    return "------testHotKey";
}

public String dealHandlerTestHotKey(String p1, String p2, BlockException exception) {
    return "-----dealHandler_testHotKey";
}
```



说明：

- `@SentinelResource`(value = "testHotKey")异常打到了前台用户界面看到，不友好
- `@SentinelResource`(value = "testHotKey",blockHandler = "dealHandlerTestHotKey")方法 testHotKey 里面第一个参数只要QPS超过每秒1次，马上降级处理

配置：

![image-20220323195740604](https://img-blog.csdnimg.cn/img_convert/cf78c97cf6e7627fc10ba452fb1edbfc.png)

![image-20220323200235304](https://img-blog.csdnimg.cn/img_convert/55097ae2cb13675913531b9544d40942.png)

限流模式只支持QPS模式，固定写死了。（这才叫热点）@SentinelResource注解的方法参数索引，0代表第一个参数，1代表第二个参数，以此类推，单机阀值以及统计窗口时长表示在此窗口时间超过阀值就限流。上面的抓图就是第一个参数有值的话，1秒的QPS为1，超过就限流，限流后调用dealHandler_testHotKey支持方法。



压力测试：

error:

- http://localhost:8401/testHotKey?p1=abc
- http://localhost:8401/testHotKey?p1=abc&p2=33

right:

-  http://localhost:8401/testHotKey?p2=abc

http://localhost:8401/testHotKey?p1=abc

![image-20220323195806578](https://img-blog.csdnimg.cn/img_convert/e5a1f8636ed2ebf2ec8f28a734ce759f.png)

http://localhost:8401/testHotKey?p1=abc&p2=33

![image-20220323195834169](https://img-blog.csdnimg.cn/img_convert/089e0414f080379613b54537e1a9ad46.png)

http://localhost:8401/testHotKey?p2=abc

![image-20220323195906415](https://img-blog.csdnimg.cn/img_convert/aa506e77cadcb4d9f5ed89d902fe8c47.png)



#### 3、参数例外项

上述案例演示了第一个参数p1，当QPS超过1秒1次点击后马上被限流

特例情况：我们期望p1参数当它是某个特殊值时，它的限流值和平时不一样

特例：假如当p1的值等于5时，它的阈值可以达到200

热点参数的注意点，参数必须是基本类型或者String

![image-20220324114602998](https://img-blog.csdnimg.cn/img_convert/29c2a46c8c552a173b700f5977cc935a.png)



测试：

http://localhost:8401/testHotKey?p1=5 当p1等于5的时候，阈值变为200

用 JMeter 压测：

这个线程数随便

![image-20220324142444965](https://img-blog.csdnimg.cn/img_convert/a61b07b8d8e78b822c1b0286a41005b7.png)

要指定 QPS 为固定值：

![image-20220324142418091](https://img-blog.csdnimg.cn/img_convert/3dbe4a11ef3728f72853970003d60ce7.png)

![image-20220324142344690](https://img-blog.csdnimg.cn/img_convert/de599d07912cc85463fd6f0a512d0379.png)

压测时我们来访问

![image-20220324142912094](https://img-blog.csdnimg.cn/img_convert/2fa9c6afa1334ec7f91a6ef8a6cdcd78.png)

![image-20220324143007287](https://img-blog.csdnimg.cn/img_convert/66fd503787a5ee84941db90b798fcf6c.png)



如果指定 QPS 为 2000【已经远大于在 Sentinel 中的阈值 200 了】

![image-20220324142736396](https://img-blog.csdnimg.cn/img_convert/fbe3949097e9b7d68177871216dc6d14.png)

![image-20220324142828200](https://img-blog.csdnimg.cn/img_convert/47304624d522e39dbb6a842bec20a828.png)



![image-20220324142713630](https://img-blog.csdnimg.cn/img_convert/ffa9ffc5e1ed2a1b70f69be1ebc6e99f.png)

http://localhost:8401/testHotKey?p1=3 当p1不等于5的时候，阈值就是平常的1

都不用压测，直接手动快速刷新

![image-20220324143113039](https://img-blog.csdnimg.cn/img_convert/d2e1036282cb4f99f4730e415192b525.png)

#### 4、其它

手贱添加异常看看…/(ㄒoㄒ)/~~

@SentinelResource：处理的是Sentinel控制台配置的违规情况，有blockHandler方法配置的兜底处理；

RuntimeException：int age = 10/0,这个是java运行时报出的运行时异常RunTimeException，@SentinelResource不管

总结：@SentinelResource主管配置出错，运行出错该走异常走异常




### （七）系统规则

#### 1、介绍

https://github.com/alibaba/Sentinel/wiki/%E7%B3%BB%E7%BB%9F%E8%87%AA%E9%80%82%E5%BA%94%E9%99%90%E6%B5%81

#### 2、各项配置参数说明

![image-20220324143938881](https://img-blog.csdnimg.cn/img_convert/b70801d29e481ffb5916cf170762d5b9.png)

![image-20220324144124506](https://img-blog.csdnimg.cn/img_convert/c5448aabe06e373218b67e8f940fbc0a.png)

可以配置全局QPS





### @SentinelResource

##### （1）按资源名称限流+后续处理

- 启动Nacos成功：http://localhost:8848/nacos/#/login
- 启动Sentinel成功：http://localhost:8080/
- 修改 cloudalibaba-sentinel-service8401

###### ① pom.xml

增加

```xml
  <dependency>
            <groupId>com.xiaoliu</groupId>
            <artifactId>cloud-api-commons</artifactId>
            <version>1.0-SNAPSHOT</version>
        </dependency>
```



###### ② 新增业务类RateLimitController

```java
@RestController
public class RateLimitController {
    @GetMapping("/byResource")
    @SentinelResource(value = "byResource", blockHandler = "handleException")
    public CommonResult byResource() {
        return new CommonResult(200, "按资源名称限流测试OK", new Payment(2020L, "serial001"));
    }

    public CommonResult handleException(BlockException exception) {
        return new CommonResult(444, exception.getClass().getCanonicalName() + "\t 服务不可用");
    }
}
```



###### ③ 配置流控规则

先访问：http://localhost:8401/byResource

![image-20220324145436122](https://img-blog.csdnimg.cn/img_convert/3eaa31aeb0f79c5441d050476cb8f80e.png)



簇点链路：byResource 是资源

![image-20220324145412281](https://img-blog.csdnimg.cn/img_convert/3cba9fbef85fb08a4009195972e0f9ab.png)

除了在流控规则中，还可以直接在资源这里设置流控：

![image-20220324145606669](https://img-blog.csdnimg.cn/img_convert/cf04b101e27e22ad8afe6fb4b58d653a.png)

![image-20220324150027892](https://img-blog.csdnimg.cn/img_convert/a7b22f8b6f90f380b22ba7eb90acf604.png)

图形配置和代码关系：

![image-20220324150130344](https://img-blog.csdnimg.cn/img_convert/50aff9592dea3f08440985b3ad0eddfc.png)



表示1秒钟内查询次数大于1，就跑到我们自定义的处流，限流

测试：

1秒钟点击1下，OK：

![image-20220324150240371](https://img-blog.csdnimg.cn/img_convert/d3c46a63c836dcb040bf5f51c0d2f7cd.png)

超过上述，疯狂点击，返回了自己定义的限流处理信息，限流发生：

![image-20220324150407659](https://img-blog.csdnimg.cn/img_convert/036654a0f07c4a53628c9c0aa134ed2b.png)



###### ④ 额外问题

此时关闭问服务8401看看：Sentinel控制台，流控规则消失了？？？？？临时/持久？

![image-20220324150527714](https://img-blog.csdnimg.cn/img_convert/68aea8fb7c394c151e27f144aff9d032.png)



##### （2）按照Url地址限流+后续处理

通过访问的URL来限流，会返回Sentinel自带默认的限流处理信息

###### ① 修改业务类RateLimitController

新增：

```java
@GetMapping("/rateLimit/byUrl")
@SentinelResource(value = "byUrl")
public CommonResult byUrl() {
    return new CommonResult(200, "按url限流测试OK", new Payment(2020L, "serial002"));
}
```



访问：http://localhost:8401/rateLimit/byUrl

![image-20220324150822137](https://img-blog.csdnimg.cn/img_convert/33015157cf936a517a2661aa90da60a0.png)



簇点链路：

byUrl 是资源

![image-20220324150935954](https://img-blog.csdnimg.cn/img_convert/4f9e5a1e6e7dbfa24cc4ea7ccbddb84c.png)

###### ② Sentinel控制台配置

![image-20220324151021468](https://img-blog.csdnimg.cn/img_convert/f7698c6ff9c389886755a6d678b80b1e.png)

测试，疯狂点击 http://localhost:8401/rateLimit/byUrl

![image-20220324151102496](https://img-blog.csdnimg.cn/img_convert/9def33d6fb065a4c025ceefab72842ac.png)



##### （3）上面兜底方案面临的问题

1. 系统默认的，没有体现我们自己的业务要求
2. 依照现有条件，我们自定义的处理方法又和业务代码耦合在一块，不直观
3. 每个业务方法都添加一个兜底的，那代码膨胀加剧
4. 全局统一的处理方法没有体现





##### （4）客户自定义限流处理逻辑

###### ① 新建 CustomerBlockHandler

创建 CustomerBlockHandler 类用于自定义限流处理逻辑

```java
public class CustomerBlockHandler {
    public static CommonResult handleException(BlockException exception) {
        return new CommonResult(2020, "自定义的限流处理信息......CustomerBlockHandler");
    }

    public static CommonResult handleException2(BlockException exception) {
        return new CommonResult(2020, "自定义的限流处理信息2......CustomerBlockHandler2");
    }
}
```



###### ② 修改 RateLimitController

新增

```java
/**
 * 自定义通用的限流处理逻辑
 * blockHandlerClass = CustomerBlockHandler.class
 * blockHandler = handleException2
 * 上述配置：找CustomerBlockHandler类里的handleException2方法进行兜底处理
 *
 * @return
 */
@GetMapping("/rateLimit/customerBlockHandler")
@SentinelResource(value = "customerBlockHandler",
        blockHandlerClass = CustomerBlockHandler.class, blockHandler = "handleException2")
public CommonResult customerBlockHandler() {
    return new CommonResult(200, "按客户自定义限流处理逻辑");
}
```



###### ③ 测试

启动微服务后先调用一次：http://localhost:8401/rateLimit/customerBlockHandler

![image-20220324152255800](https://img-blog.csdnimg.cn/img_convert/0d15f390f5e6f10198d248725279dbfc.png)

簇点链路：

![image-20220324152321640](https://img-blog.csdnimg.cn/img_convert/0bd0ad649ecc7135665544e29a0501b6.png)

Sentinel控制台配置：

![image-20220324152419260](https://img-blog.csdnimg.cn/img_convert/23b44bb9ec95a935f53d15c78fbef01e.png)

疯狂刷新：

![image-20220324152441008](https://img-blog.csdnimg.cn/img_convert/1746fe72bb2e974409addc083e92b683.png)





##### （5）更多注解属性说明

@SentinelResource注解最主要的两个用法：限流控制和熔断降级的具体使用案例介绍完了。另外，该注解还有一些其他更精细化的配置，比如忽略某些异常的配置、默认降级函数等等，具体可见如下说明：

- value：资源名称，必需项（不能为空）
- entryType：entry类型，可选项（默认为 EntryType.OUT）
- fallback：fallback函数名称，可选项，用于在抛出异常的时候提供 fallback处理逻辑。fallback函数可以针对所有类型的异常（除了exceptionsToIgnore里面排除掉的异常类型）进行处理。fallback函数签名和位置要求： 返回值类型必须与原函数返回值类型一致；方法参数列表需要和原函数一致，或者可以额外多一个 Throwable类型的参数用于接收对应的异常。
- fallback函数默认需要和原方法在同一个类中。若希望使用其他类的函数，则可以指定 fallbackClass为对应的类的 Class 对象，注意对应的函数必需为 static函数，否则无法解析。 defaultFallback（since 1.6.0）：默认的 fallback函数名称，可选项，通常用于通用的 fallback逻辑（即可以用于很多服务或方法）。默认 fallback函数可以针对所有类型的异常（除了exceptionsToIgnore里面排除掉的异常类型）进行处理。若同时配置了 fallback和 defaultFallback，则只有 fallback会生效。defaultFallback函数签名要求：返回值类型必须与原函数返回值类型一致；
- 方法参数列表需要为空，或者可以额外多一个 Throwable 类型的参数用于接收对应的异常。
- defaultFallback函数默认需要和原方法在同一个类中。若希望使用其他类的函数，则可以指定 fallbackClass为对应的类的 Class 对象，注意对应的函数必需为 static 函数，否则无法解析。
- exceptionsToIgnore（since 1.6.0）：用于指定哪些异常被排除掉，不会计入异常统计中，也不会进入 fallback 逻辑中，而是会原样抛出。

这篇帖子也不错：https://blog.csdn.net/liuerchong/article/details/114534166

多说一句：所有的代码都要用try-catch-finally方式进行处理，o(╥﹏╥)o

![image-20220324153257572](https://img-blog.csdnimg.cn/img_convert/00f78f1ccd9e47334ab2d2eab84f9f95.png)

Sentinel主要有三个核心Api：

- SphU定义资源
- Tracer定义统计
- ContextUtil定义了上下文





### 服务熔断功能

sentinel整合ribbon+openFeign+fallback

#### （1）Ribbon系列——提供者9003/9004

启动nacos和sentinel，新建cloudalibaba-provider-payment9003/9004两个一样的做法

##### ① pom.xml

```xml
<dependencies>
        <!--SpringCloud ailibaba nacos -->
        <dependency>
            <groupId>com.alibaba.cloud</groupId>
            <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
        </dependency>
        <dependency><!-- 引入自己定义的api通用包，可以使用Payment支付Entity -->
            <groupId>com.atguigu.springcloud</groupId>
            <artifactId>cloud-api-commons</artifactId>
            <version>${project.version}</version>
        </dependency>
        <!-- SpringBoot整合Web组件 -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
        <!--日常通用jar包配置-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>
```



##### ② application.yml

记得修改不同的端口号

```yaml
server:
  port: 9003

spring:
  application:
    name: nacos-payment-provider
  cloud:
    nacos:
      discovery:
        server-addr: localhost:8848 #配置Nacos地址

management:
  endpoints:
    web:
      exposure:
        include: '*'
```



##### ③ 主启动

```java
@SpringBootApplication
@EnableDiscoveryClient
public class PaymentMain9003 {
    public static void main(String[] args) {
        SpringApplication.run(PaymentMain9003.class, args);
    }
}
```





##### ④ 业务类

```java
@RestController
public class PaymentController {
    @Value("${server.port}")
    private String serverPort;

    eeeeeeeeeeeeeeeeeeeeeeeeeee

    static {
        hashMap.put(1L, new Payment(1L, "28a8c1e3bc2742d8848569891fb42181"));
        hashMap.put(2L, new Payment(2L, "bba8c1e3bc2742d8848569891ac32182"));
        hashMap.put(3L, new Payment(3L, "6ua8c1e3bc2742d8848569891xt92183"));
    }

    @GetMapping(value = "/paymentSQL/{id}")
    public CommonResult<Payment> paymentSQL(@PathVariable("id") Long id) {
        Payment payment = hashMap.get(id);
        CommonResult<Payment> result = new CommonResult(200, "from mysql,serverPort:  " + serverPort, payment);
        return result;
    }
}
```



测试地址：http://localhost:9003/paymentSQL/1

![image-20220324155343937](https://img-blog.csdnimg.cn/img_convert/5ee94d695fc09b59142033075209fe0e.png)



#### 2）Ribbon系列——消费者84

新建cloudalibaba-consumer-nacos-order84

##### ① pom.xml

```xml
<dependencies>
        <!--SpringCloud ailibaba nacos -->
        <dependency>
            <groupId>com.alibaba.cloud</groupId>
            <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
        </dependency>
        <!--SpringCloud ailibaba sentinel -->
        <dependency>
            <groupId>com.alibaba.cloud</groupId>
            <artifactId>spring-cloud-starter-alibaba-sentinel</artifactId>
        </dependency>
        <!-- 引入自己定义的api通用包，可以使用Payment支付Entity -->
        <dependency>
            <groupId>com.xiaoliu</groupId>
            <artifactId>cloud-api-commons</artifactId>
            <version>${project.version}</version>
        </dependency>
        <!-- SpringBoot整合Web组件 -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
        <!--日常通用jar包配置-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>
```



##### ② application.yml

```yaml
server:
  port: 84

spring:
  application:
    name: nacos-order-consumer
  cloud:
    nacos:
      discovery:
        server-addr: localhost:8848
    sentinel:
      transport:
        #配置Sentinel dashboard地址
        dashboard: localhost:8080
        #默认8719端口，假如被占用会自动从8719开始依次+1扫描,直至找到未被占用的端口
        port: 8719


#消费者将要去访问的微服务名称(注册成功进nacos的微服务提供者)
service-url:
  nacos-user-service: http://nacos-payment-provider
```





##### ③ 主启动

```java
@EnableDiscoveryClient
@SpringBootApplication
public class OrderNacosMain84 {
    public static void main(String[] args) {
        SpringApplication.run(OrderNacosMain84.class, args);
    }
}
```



##### ④ 业务类 ApplicationContextConfig

``` java
@Configuration
public class ApplicationContextConfig {

    @Bean
    @LoadBalanced
    public RestTemplate getRestTemplate() {
        return new RestTemplate();
    }
}
```



##### ⑤ 业务类 CircleBreakerController

```java
@RestController
@Slf4j
public class CircleBreakerController {
    public static final String SERVICE_URL = "http://nacos-payment-provider";

    @Resource
    private RestTemplate restTemplate;

    @RequestMapping("/consumer/fallback/{id}")
    @SentinelResource(value = "fallback")
    public CommonResult<Payment> fallback(@PathVariable Long id) {
        CommonResult<Payment> result = restTemplate.getForObject(SERVICE_URL + "/paymentSQL/" + id, CommonResult.class, id);

        if (id == 4) {
            throw new IllegalArgumentException("IllegalArgumentException,非法参数异常....");
        } else if (result.getData() == null) {
            throw new NullPointerException("NullPointerException,该ID没有对应记录,空指针异常");
        }

        return result;
    }
}
```



修改后请重启微服务：热部署对java代码级生效及时，对@SentinelResource注解内属性，有时效果不好

目的：fallback管运行异常、blockHandler管配置违规

测试地址：

http://localhost:84/consumer/fallback/1

![image-20220324161143250](https://img-blog.csdnimg.cn/img_convert/67a08292ec5d1062f3643e2e9c3b26a4.png)

http://localhost:84/consumer/fallback/4 给客户error页面，不友好

![image-20220324160515423](https://img-blog.csdnimg.cn/img_convert/eae1ec931f1b7e5c5efa07de49bcd355.png)

http://localhost:84/consumer/fallback/15645616165456

![image-20220324160709521](https://img-blog.csdnimg.cn/img_convert/1a07cd9d6c7b56653f399e2c13425ed2.png)



##### ⑥ 只配置fallback

本例sentinel无配置

```java
@RestController
@Slf4j
public class CircleBreakerController {
    public static final String SERVICE_URL = "http://nacos-payment-provider";

    @Resource
    private RestTemplate restTemplate;

    @RequestMapping("/consumer/fallback/{id}")
    @SentinelResource(value = "fallback", fallback = "handlerFallback")
    public CommonResult<Payment> fallback(@PathVariable Long id) {
        CommonResult<Payment> result = restTemplate.getForObject(SERVICE_URL + "/paymentSQL/" + id, CommonResult.class, id);

        if (id == 4) {
            throw new IllegalArgumentException("IllegalArgumentException,非法参数异常....");
        } else if (result.getData() == null) {
            throw new NullPointerException("NullPointerException,该ID没有对应记录,空指针异常");
        }

        return result;
    }

    public CommonResult handlerFallback(@PathVariable Long id, Throwable e) {
        Payment payment = new Payment(id, "null");
        return new CommonResult<>(444, "兜底异常handlerFallback,exception内容  " + e.getMessage(), payment);
    }
}
```



测试：

http://localhost:84/consumer/fallback/4

![image-20220324161217507](https://img-blog.csdnimg.cn/img_convert/fac2de9a03e2165dd480eb39a12d9d80.png)

http://localhost:84/consumer/fallback/15645616165456

![image-20220324161253947](https://img-blog.csdnimg.cn/img_convert/6673b4400b8c77490ab66e184b99f0bc.png)



##### ⑦ 只配置blockHandler

![image-20220324161503031](https://img-blog.csdnimg.cn/img_convert/3c430ba508daffae9fce6409b0c3d9b7.png)



```java
@RestController
@Slf4j
public class CircleBreakerController {
    public static final String SERVICE_URL = "http://nacos-payment-provider";

    @Resource
    private RestTemplate restTemplate;

    @RequestMapping("/consumer/fallback/{id}")
//    @SentinelResource(value = "fallback", fallback = "handlerFallback")
    @SentinelResource(value = "fallback", blockHandler = "blockHandler")
    public CommonResult<Payment> fallback(@PathVariable Long id) {
        CommonResult<Payment> result = restTemplate.getForObject(SERVICE_URL + "/paymentSQL/" + id, CommonResult.class, id);

        if (id == 4) {
            throw new IllegalArgumentException("IllegalArgumentException,非法参数异常....");
        } else if (result.getData() == null) {
            throw new NullPointerException("NullPointerException,该ID没有对应记录,空指针异常");
        }

        return result;
    }

    public CommonResult handlerFallback(@PathVariable Long id, Throwable e) {
        Payment payment = new Payment(id, "null");
        return new CommonResult<>(444, "兜底异常handlerFallback,exception内容  " + e.getMessage(), payment);
    }

    public CommonResult blockHandler(@PathVariable Long id, BlockException blockException) {
        Payment payment = new Payment(id, "null");
        return new CommonResult<>(445, "blockHandler-sentinel限流,无此流水: blockException  " + blockException.getMessage(), payment);
    }
}
```



本例sentinel需配置：

簇点链路：

![image-20220324161928613](https://img-blog.csdnimg.cn/img_convert/70af25e14e1d0a9a78f080fed0407186.png)



服务降级：

异常超过2次后，断路器打开，断电跳闸，系统被保护

![image-20220324162013617](https://img-blog.csdnimg.cn/img_convert/9fb5014f51abae0dbdf818dc8f2bd45c.png)

第一次和第二次访问还是报异常：

![image-20220324162228438](https://img-blog.csdnimg.cn/img_convert/c999584692b2397ab91d59e617b4537a.png)

第三、四次···访问：

![image-20220324162101918](https://img-blog.csdnimg.cn/img_convert/9e3cda83201c95e9f7caf0ab70831c3a.png)

时间窗口期70s过了之后：

![image-20220324162226665](https://img-blog.csdnimg.cn/img_convert/5e662940e18a54939de6aa81b0f4cf74.png)





##### ⑧ fallback和blockHandler都配置

![image-20220324162558106](https://img-blog.csdnimg.cn/img_convert/1b67a61828bf3c3181b63065a2add4b9.png)

![image-20220324162613489](https://img-blog.csdnimg.cn/img_convert/eb86d9620193902c45212695ba2d9867.png)

```java
@RestController
@Slf4j
public class CircleBreakerController {
    public static final String SERVICE_URL = "http://nacos-payment-provider";

    @Resource
    private RestTemplate restTemplate;

    @RequestMapping("/consumer/fallback/{id}")
//    @SentinelResource(value = "fallback", fallback = "handlerFallback")
//    @SentinelResource(value = "fallback", blockHandler = "blockHandler")
    @SentinelResource(value = "fallback", fallback = "handlerFallback", blockHandler = "blockHandler")
    public CommonResult<Payment> fallback(@PathVariable Long id) {
        CommonResult<Payment> result = restTemplate.getForObject(SERVICE_URL + "/paymentSQL/" + id, CommonResult.class, id);

        if (id == 4) {
            throw new IllegalArgumentException("IllegalArgumentException,非法参数异常....");
        } else if (result.getData() == null) {
            throw new NullPointerException("NullPointerException,该ID没有对应记录,空指针异常");
        }

        return result;
    }

    public CommonResult handlerFallback(@PathVariable Long id, Throwable e) {
        Payment payment = new Payment(id, "null");
        return new CommonResult<>(444, "fallback,无此流水,exception  " + e.getMessage(), payment);
    }

    public CommonResult blockHandler(@PathVariable Long id, BlockException blockException) {
        Payment payment = new Payment(id, "null");
        return new CommonResult<>(445, "blockHandler-sentinel限流,无此流水: blockException  " + blockException.getMessage(), payment);
    }
}
```



本例sentinel需配置：

http://localhost:84/consumer/fallback/4

![image-20220324162817089](https://img-blog.csdnimg.cn/img_convert/6573d05bc873bf8ab5cbfd12a78faf04.png)

第一、二次访问：

![image-20220324162739258](https://img-blog.csdnimg.cn/img_convert/a24e35f2b296f85b0326ca482c464533.png)

第三、四次访问【时间窗口期结束前】：

![image-20220324162905995](https://img-blog.csdnimg.cn/img_convert/ab3da2ee51fb45329d691231fec3bfe8.png)

结论：若 blockHandler 和 fallback 都进行了配置，则被限流降级而抛出 BlockException 时只会进入 blockHandler 处理逻辑



##### ⑨ 忽略属性

```java
@SentinelResource(value = "fallback", fallback = "handlerFallback", blockHandler = "blockHandler", exceptionsToIgnore = {IllegalArgumentException.class})
```



##### ⑩ OpenFeign

###### 1.改pom

添加

```xml
  <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-openfeign</artifactId>
        </dependency>
```



###### 2.改yml

添加

```yaml
#激活sentinel对feign的支持
feign:
  sentinel:
    enabled: true
```



###### 3.业务层**PaymentService**、**PaymentFallbackService**

```java
@FeignClient(value = "nacos-payment-provider",fallback = PaymentFallbackService.class)
public interface PaymentService {

    @GetMapping(value = "/paymentSQL/{id}")
    CommonResult<Payment> paymentSQL(@PathVariable("id") Long id);
}
```

```java
@Component
public class PaymentFallbackService implements PaymentService {
    @Override
    public CommonResult<Payment> paymentSQL(Long id) {
        return new CommonResult<>(4444,"服务降级返回，-----PaymentFallbackService",new Payment(id,"errorServer"));
    }
}
```



###### 4.主启动

```java
@SpringBootApplication
@EnableDiscoveryClient
@EnableFeignClients
public class OrderNacosMain84 {
    public static void main(String[] args) {
        SpringApplication.run(OrderNacosMain84.class,args);
    }
}
```



###### 5.Controller

添加

```java
    //==========================OpenFeign
    @Resource
    private PaymentService paymentService;

    @GetMapping(value = "/consumer/paymentSQL/{id}")
    public CommonResult<Payment> paymentSQL(@PathVariable("id") Long id) {

        return paymentService.paymentSQL(id);
    }
```



使用OpenFeign添加全局配置兜底设置





### sentinel持久化配置

将限流配置规则持久化建nacos保存，只要刷新某个rest地址，sentinel控制台的流控规则就能看到，只要nacos里面的配置不删除，sentinel的流控规则持久有效



#### 1持久化配置

目前的sentinel 当重启以后，数据都会丢失，和 nacos 类似原理。需要持久化。它可以被持久化到nacos 的数据库中。
在alibaba-sentinel-service8401模块

1.pom

```xml
<dependency>
    <groupId>com.alibaba.csp</groupId>
    <artifactId>sentinel-datasource-nacos</artifactId>
</dependency>
```



2.yml

```yaml
spring:
  cloud:
    sentinel:
      datasource:
        ds1:  
          nacos:
            server-addr: localhost:8848
            dataId: ${spring.application.name}
            group: DEFAULT_GROUP
            data-type: json
            rule-type: flow
```



3.去nacos上创建一个dataid ,名字和yml配置的一致，json格式，内容如下：

```json
[
    {
        "resource": "/testA",
        "limitApp": "default",
        "grade": 1,
        "count": 1,
        "strategy": 0,
        "controlBehavior": 0,
        "clusterMode": false
    }
]
```

- resource：资源名称
- limitApp：来源应用
- grade：阈值类型，0表示线程数，1表示QPS，
- count：单机阈值，
- strategy：流控模式，0表示直接，1表示关联，2表示链路
- controlBehavior:流控效果，0表示快速失败，1表示Warm Up,2表示排队等待；
- cIusterM0de: 是否集群。

启动应用，发现存在 关于 /testA 请求路径的流控规则。
总结: 就是在 sentinel 启动的时候，去 nacos 上读取相关规则配置信息，实际上它规则的持久化，就是第三步，粘贴到nacos上保存下来，就算以后在 sentinel 上面修改了，重启应用以后也是无效的。



## Seate

### seate处理分布式事务

单体应用应用被拆成微服务应用，原来的三个模块被拆成三个独立的应用，分别使用三个独立的数据源，业务操作需要三个服务来完成，此时每个服务内部的一致性有本地事务来保证，但全局事务的一致性无法保证
一次事务操作需要跨多个数据源或需要跨多个系统进行远程调用，就会产生分布式事务问题



### 1 seate简介

Seate是一款开源的分布式事务解决方案，致力于微服务构架下提供高性能和简单易用的分布式事务服务



### 2分布式事务处理过程

seate是一个典型的分布式事务处理过程，由一个ID和三组件模型组成
一个ID：全局唯一的事务ID
三组件：

- TC (Transaction Coordinator) - 事务协调者

- 维护全局和分支事务的状态，驱动全局事务提交或回滚。

- TM (Transaction Manager) - 事务管理器

  定义全局事务的范围：开始全局事务、提交或回滚全局事务。

- RM (Resource Manager) - 资源管理器,管理分支事务处理的资源，与TC交谈以注册分支事务和报告分支事务的状态，并驱动分支事务提交或回滚。



**过程**

1. TM向TC申请开启一个全局事务，全局事务创建成功并生成一个全局唯一的XID;
2. XID在微服务调用链路的上下文中传播；
3. RM向TC汪册分支事务，将其纳入XID对应全局事务的管辖；
4. TM向TC发起针对XID的全局提交或回滚决议；
5. TC调度XID下管辖的全部分支事务完成提交或回请求。



![在这里插入图片描述](https://img-blog.csdnimg.cn/20201110200914932.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaTE5ODYyMQ==,size_16,color_FFFFFF,t_70#pic_center)



![在这里插入图片描述](https://img-blog.csdnimg.cn/20201110200929750.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaTE5ODYyMQ==,size_16,color_FFFFFF,t_70#pic_center)

### 3 seate下载

地址`https://github.com/seata/seata/releases/download/v1.0.0/seata-server-1.0.0.zip`



### 4 seate安装

#### 1下载seata-server-1.0.0.zip解压到指定目录并修改conf目录下的file. conf配置文件

1.备份file.conf文件

2.service模块
将模式改成db

![在这里插入图片描述](https://img-blog.csdnimg.cn/f944ad9399ab47c786b2e82ec10f2dcf.png)



3.配置数据库的信息

![在这里插入图片描述](https://img-blog.csdnimg.cn/2fe138ed67a64559ac6eb2ff0dbaa44e.png)

```properties
driver-class-name = "com.mysql.jdbc.Driver"
    url = "jdbc:mysql://127.0.0.1:3306/seata"
    user = "root"
    password = "root"
```



4.创建一个名为seata的数据库

5.在seata下的conf目录选择db_store_sql里面的SQL语句并运行
由于seata-server-1.0.0没有这个SQL语句，器SQL语句如下

```sql
DROP TABLE IF EXISTS `branch_table`;
CREATE TABLE `branch_table`  (
  `branch_id` bigint(20) NOT NULL,
  `xid` varchar(128) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL,
  `transaction_id` bigint(20) NULL DEFAULT NULL,
  `resource_group_id` varchar(32) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
  `resource_id` varchar(256) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
  `branch_type` varchar(8) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
  `status` tinyint(4) NULL DEFAULT NULL,
  `client_id` varchar(64) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
  `application_data` varchar(2000) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
  `gmt_create` datetime(0) NULL DEFAULT NULL,
  `gmt_modified` datetime(0) NULL DEFAULT NULL,
  PRIMARY KEY (`branch_id`) USING BTREE,
  INDEX `idx_xid`(`xid`) USING BTREE
) ENGINE = InnoDB CHARACTER SET = utf8 COLLATE = utf8_general_ci ROW_FORMAT = Dynamic;
 
-- ----------------------------
-- Table structure for global_table
-- ----------------------------
DROP TABLE IF EXISTS `global_table`;
CREATE TABLE `global_table`  (
  `xid` varchar(128) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL,
  `transaction_id` bigint(20) NULL DEFAULT NULL,
  `status` tinyint(4) NOT NULL,
  `application_id` varchar(32) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
  `transaction_service_group` varchar(32) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
  `transaction_name` varchar(128) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
  `timeout` int(11) NULL DEFAULT NULL,
  `begin_time` bigint(20) NULL DEFAULT NULL,
  `application_data` varchar(2000) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
  `gmt_create` datetime(0) NULL DEFAULT NULL,
  `gmt_modified` datetime(0) NULL DEFAULT NULL,
  PRIMARY KEY (`xid`) USING BTREE,
  INDEX `idx_gmt_modified_status`(`gmt_modified`, `status`) USING BTREE,
  INDEX `idx_transaction_id`(`transaction_id`) USING BTREE
) ENGINE = InnoDB CHARACTER SET = utf8 COLLATE = utf8_general_ci ROW_FORMAT = Dynamic;
 
-- ----------------------------
-- Table structure for lock_table
-- ----------------------------
DROP TABLE IF EXISTS `lock_table`;
CREATE TABLE `lock_table`  (
  `row_key` varchar(128) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL,
  `xid` varchar(96) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
  `transaction_id` bigint(20) NULL DEFAULT NULL,
  `branch_id` bigint(20) NOT NULL,
  `resource_id` varchar(256) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
  `table_name` varchar(32) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
  `pk` varchar(36) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
  `gmt_create` datetime(0) NULL DEFAULT NULL,
  `gmt_modified` datetime(0) NULL DEFAULT NULL,
  PRIMARY KEY (`row_key`) USING BTREE,
  INDEX `idx_branch_id`(`branch_id`) USING BTREE
) ENGINE = InnoDB CHARACTER SET = utf8 COLLATE = utf8_general_ci ROW_FORMAT = Dynamic;

```



6.修改conf目录下的registry.conf配置文件
指明注册中心为nacos及修改nacos的连接信息

![在这里插入图片描述](https://img-blog.csdnimg.cn/756b2fb3cb624e24a9381ccf6224b195.png)

7.先启动nacos

8.启动seata，点击seata-server.bat
出现一下信息说明启动成功

![在这里插入图片描述](https://img-blog.csdnimg.cn/304ce1649de44efdb6ed6bed3de9503c.png)





### 5.Seata实例

#### 1业务声明

这里我们创建三个服务，一个订单服务，一个库存服务，一个账户服务。当用户下单时，会在订单服务中创建一个订单，然后通过远程调用库存服务来扣减下单商品的库存，再通过远程调用账户服务来扣减用户账户里面的余额，最后在订单服务中修改订单状态为已完成。该操作跨越三个数据库，有两次远程调用，很明显会有分布式事务问题。

#### 2数据库准备

首先我们创建数据库

```sql
create database seata_order;
create database seata_storage;
create database seata_account;
```



然后分别在对应的库下面建立相应的表

```sql
USE
seata_order;
DROP TABLE IF EXISTS `t_order`;
CREATE TABLE `t_order`
(
    `int`        bigint(11) NOT NULL AUTO_INCREMENT,
    `user_id`    bigint(20) DEFAULT NULL COMMENT '用户id',
    `product_id` bigint(11) DEFAULT NULL COMMENT '产品id',
    `count`      int(11) DEFAULT NULL COMMENT '数量',
    `money`      decimal(11, 0) DEFAULT NULL COMMENT '金额',
    `status`     int(1) DEFAULT NULL COMMENT '订单状态:  0:创建中 1:已完结',
    PRIMARY KEY (`int`) USING BTREE
) ENGINE = InnoDB CHARACTER SET = utf8 COLLATE = utf8_general_ci COMMENT = '订单表' ROW_FORMAT = Dynamic;
```

```sql
USE
seata_storage;
DROP TABLE IF EXISTS `t_storage`;
CREATE TABLE `t_storage`
(
    `int`        bigint(11) NOT NULL AUTO_INCREMENT,
    `product_id` bigint(11) DEFAULT NULL COMMENT '产品id',
    `total`      int(11) DEFAULT NULL COMMENT '总库存',
    `used`       int(11) DEFAULT NULL COMMENT '已用库存',
    `residue`    int(11) DEFAULT NULL COMMENT '剩余库存',
    PRIMARY KEY (`int`) USING BTREE
) ENGINE = InnoDB CHARACTER SET = utf8 COLLATE = utf8_general_ci COMMENT = '库存' ROW_FORMAT = Dynamic;
INSERT INTO `t_storage`
VALUES (1, 1, 100, 0, 100);
```

```sql
USE
seata_account;
DROP TABLE IF EXISTS `t_account`;
CREATE TABLE `t_account`
(
    `id`      bigint(11) NOT NULL COMMENT 'id',
    `user_id` bigint(11) DEFAULT NULL COMMENT '用户id',
    `total`   decimal(10, 0) DEFAULT NULL COMMENT '总额度',
    `used`    decimal(10, 0) DEFAULT NULL COMMENT '已用余额',
    `residue` decimal(10, 0) DEFAULT NULL COMMENT '剩余可用额度',
    PRIMARY KEY (`id`) USING BTREE
) ENGINE = InnoDB CHARACTER SET = utf8 COLLATE = utf8_general_ci COMMENT = '账户表' ROW_FORMAT = Dynamic;
INSERT INTO `t_account`
VALUES (1, 1, 1000, 0, 1000);
```



然后分别建立相应的回滚日志

```sql
DROP TABLE IF EXISTS `undo_log`;
CREATE TABLE `undo_log`
(
    `id`            bigint(20) NOT NULL AUTO_INCREMENT,
    `branch_id`     bigint(20) NOT NULL,
    `xid`           varchar(100) NOT NULL,
    `context`       varchar(128) NOT NULL,
    `rollback_info` longblob     NOT NULL,
    `log_status`    int(11) NOT NULL,
    `log_created`   datetime     NOT NULL,
    `log_modified`  datetime     NOT NULL,
    `ext`           varchar(100) DEFAULT NULL,
    PRIMARY KEY (`id`),
    UNIQUE KEY `ux_undo_log` (`xid`,`branch_id`)
) ENGINE=InnoDB AUTO_INCREMENT=1 DEFAULT CHARSET=utf8;
```



最后数据库结构应该是这样的

![image-20220517183224903](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220517183224903.png)



#### 3业务逻辑编写

##### 1 seata-order-service

新建一个module端口号为2001。

pom.xml

```xml
<dependencies>
        <!-- nacos -->
        <dependency>
            <groupId>com.alibaba.cloud</groupId>
            <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
        </dependency>
        <!-- seata -->
        <dependency>
            <groupId>com.alibaba.cloud</groupId>
            <artifactId>spring-cloud-starter-alibaba-seata</artifactId>
            <exclusions>
                <exclusion>
                    <artifactId>seata-all</artifactId>
                    <groupId>io.seata</groupId>
                </exclusion>
            </exclusions>
        </dependency>
        <dependency>
            <groupId>io.seata</groupId>
            <artifactId>seata-all</artifactId>
            <version>1.0.0</version>
        </dependency>
        <!-- feign -->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-openfeign</artifactId>
        </dependency>
        <!-- web-actuator -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
        <!-- mysql-druid -->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>5.1.37</version>
        </dependency>
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>druid-spring-boot-starter</artifactId>
            <version>1.1.10</version>
        </dependency>
        <dependency>
            <groupId>org.mybatis.spring.boot</groupId>
            <artifactId>mybatis-spring-boot-starter</artifactId>
            <version>2.0.0</version>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
    </dependencies>
```

这个pom文件一定要加上这三个依赖，nacos，seata，feign，我们将seata注册到nacos里，所以得有nacos，通过feign调用微服务。

yml文件

```yaml
server:
  port: 2001


spring:
  application:
    name: seata-order-service
  cloud:
    alibaba:
      seata:
        tx-service-group: fsp_tx_group #自定义事务组名称需要与seata-server中的对应
    nacos:
      discovery:
        server-addr: localhost:8848
  datasource:
    type: com.alibaba.druid.pool.DruidDataSource
    driver-class-name: org.gjt.mm.mysql.Driver
    url: jdbc:mysql://localhost:3306/seata_order?useUnicode=true&characterEncoding=utf-8&useSSL=false
    username: root
    password: root

feign:
  hystrix:
    enabled: false

logging:
  level:
    io:
      seata: info

mybatis:
  mapperLocations: classpath:mapper/*.xml
```

除了要填加yml文件以外seata还要配置file.conf，registry.conf，这两个文件就是一开始seata-server服务器得配置文件

file.conf

```properties
service {
  #transaction service group mapping
  vgroup_mapping.fsp_tx_group = "default" #修改自定义事务组名称
  #only support when registry.type=file, please don't set multiple addresses
  default.grouplist = "127.0.0.1:8091"
  #disable seata
  disableGlobalTransaction = false
}

## transaction log store, only used in seata-server
store {
  ## store mode: file、db
  mode = "db"

  ## file store property
  file {
    ## store location dir
    dir = "sessionStore"
  }

  ## database store property
  db {
    ## the implement of javax.sql.DataSource, such as DruidDataSource(druid)/BasicDataSource(dbcp) etc.
    datasource = "dbcp"
    ## mysql/oracle/h2/oceanbase etc.
    db-type = "mysql"
    driver-class-name = "com.mysql.jdbc.Driver"
    url = "jdbc:mysql://localhost:3306/seata"
    user = "root"
    password = "root"
  }
}
```

registry.conf

```properties
registry {
  # file 、nacos 、eureka、redis、zk、consul、etcd3、sofa
  type = "nacos"

  nacos {
    serverAddr = "localhost:8848"
    namespace = ""
    cluster = "default"
  }
  eureka {
    serviceUrl = "http://localhost:8761/eureka"
    application = "default"
    weight = "1"
  }
  redis {
    serverAddr = "localhost:6379"
    db = "0"
  }
  zk {
    cluster = "default"
    serverAddr = "127.0.0.1:2181"
    session.timeout = 6000
    connect.timeout = 2000
  }
  consul {
    cluster = "default"
    serverAddr = "127.0.0.1:8500"
  }
  etcd3 {
    cluster = "default"
    serverAddr = "http://localhost:2379"
  }
  sofa {
    serverAddr = "127.0.0.1:9603"
    application = "default"
    region = "DEFAULT_ZONE"
    datacenter = "DefaultDataCenter"
    cluster = "default"
    group = "SEATA_GROUP"
    addressWaitTime = "3000"
  }
  file {
    name = "file.conf"
  }
}

config {
  # file、nacos 、apollo、zk、consul、etcd3
  type = "file"

  nacos {
    serverAddr = "localhost"
    namespace = ""
  }
  consul {
    serverAddr = "127.0.0.1:8500"
  }
  apollo {
    app.id = "seata-server"
    apollo.meta = "http://192.168.1.204:8801"
  }
  zk {
    serverAddr = "127.0.0.1:2181"
    session.timeout = 6000
    connect.timeout = 2000
  }
  etcd3 {
    serverAddr = "http://localhost:2379"
  }
  file {
    name = "file.conf"
  }
}
```

然后接下来实现我们的业务方法，我们的业务是这样的，下订单之后我们要做两个操作1.新建订单2.修改订单状态从0改为1

```java
@Mapper
public interface OrderDao {
    //1 新建订单
    void create(Order order);

    //2 修改订单状态，从零改为1
    void update(@Param("userId") Long userId, @Param("status") Integer status);
}
```

mapper.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.wjz.springcloud.alibaba.dao.OrderDao">

    <resultMap id="order" type="com.wjz.springcloud.alibaba.domain.Order">
        <result property="id" column="id" jdbcType="BIGINT"/>
        <result property="userId" column="user_id" jdbcType="BIGINT"/>
        <result property="productId" column="product_id" jdbcType="BIGINT"/>
        <result property="count" column="count" jdbcType="INTEGER"/>
        <result property="money" column="money" jdbcType="BIGINT"/>
        <result property="status" column="status" jdbcType="INTEGER"/>
    </resultMap>


    <insert id="create">
        insert into t_order(user_id, product_id, count, money, status)
            value (#{userId},#{productId},#{count},#{money},0)
    </insert>

    <update id="update">
        update t_order
        set status = 1
        where user_id = #{userId}
          and status = #{status}
    </update>
</mapper>
```



然后是order的service层和Impl层

```java
public interface OrderService {
    void create(Order order);
}
@Service
@Slf4j
public class OrderServiceImpl implements OrderService {
    @Resource
    private OrderDao orderDao;
    @Resource
    private StorageService storageService;
    @Resource
    private AccountService accountService;

    /**
     * 创建订单->调用库存服务扣减库存->调用账户服务扣减账户余额->修改订单状态
     * 简单说：下订单->扣库存->减余额->改状态
     * 注释掉 @GlobalTransactional 的时候，需要注意下方这个方法里面手动模拟了延时，也需要注释掉
     * com.atguigu.springcloud.alibaba.service.impl.AccountServiceImpl#decrease(java.lang.Long, java.math.BigDecimal)
     */
    @Override
    public void create(Order order) {
        log.info("----->开始新建订单");
        //1 新建订单
        orderDao.create(order);

        //2 扣减库存
        log.info("----->订单微服务开始调用库存，做扣减Count");
        storageService.decrease(order.getProductId(), order.getCount());
        log.info("----->订单微服务开始调用库存，做扣减end");

        //3 扣减账户
        log.info("----->订单微服务开始调用账户，做扣减Money");
        accountService.decrease(order.getUserId(), order.getMoney());
        log.info("----->订单微服务开始调用账户，做扣减end");

        //4 修改订单状态，从零到1,1代表已经完成
        log.info("----->修改订单状态开始");
        orderDao.update(order.getUserId(), 0);
        log.info("----->修改订单状态结束");

        log.info("----->下订单结束了，O(∩_∩)O哈哈~");

    }
}
```



新建订单之后我们要扣减库存和扣减账户所以我们要写storageService和accountService这两个的实现。

```java
@FeignClient(value = "seata-storage-service")
public interface StorageService {

    @PostMapping(value = "/storage/decrease")
    CommonResult decrease(@RequestParam("productId") Long productId, @RequestParam("count") Integer count);

}
```

````java
@FeignClient(value = "seata-account-service")
public interface AccountService {
    /**
     * @param userId
     * @param money
     * @return
     */
    @PostMapping(value = "/account/decrease")
    CommonResult decrease(@RequestParam("userId") Long userId, @RequestParam("money") BigDecimal money);

}
````

减库存和扣减账户我们通过远程调用这两个的微服务来实现。然后是controller

```java
@RestController
public class OrderController {
    @Resource
    private OrderService orderService;


    @GetMapping("/order/create")//这个浏览器只能用get请求访问，我们底层调用微服务的时候会使用PostMapping
    public CommonResult create(Order order) {
        orderService.create(order);
        return new CommonResult(200, "订单创建成功");
    }
}
```

然后就是一些配置类使用Seata对我们的数据源进行代理

```java
@Configuration
public class DataSourceProxyConfig {

    @Value("${mybatis.mapperLocations}")
    private String mapperLocations;

    @Bean
    @ConfigurationProperties(prefix = "spring.datasource")
    public DataSource druidDataSource() {
        return new DruidDataSource();
    }

    @Bean
    public DataSourceProxy dataSourceProxy(DataSource dataSource) {
        return new DataSourceProxy(dataSource);
    }

    @Bean
    public SqlSessionFactory sqlSessionFactoryBean(DataSourceProxy dataSourceProxy) throws Exception {
        SqlSessionFactoryBean sqlSessionFactoryBean = new SqlSessionFactoryBean();
        sqlSessionFactoryBean.setDataSource(dataSourceProxy);
        sqlSessionFactoryBean.setMapperLocations(new PathMatchingResourcePatternResolver().getResources(mapperLocations));
        sqlSessionFactoryBean.setTransactionFactory(new SpringManagedTransactionFactory());
        return sqlSessionFactoryBean.getObject();
    }

}
```

```java
@Configuration
@MapperScan({"com.wjz.springcloud.alibaba.dao"})
public class MyBatisConfig {
}
```



最后还有启动类

```java
@EnableDiscoveryClient
@EnableFeignClients
@SpringBootApplication(exclude = DataSourceAutoConfiguration.class)//一定要加这个忽略掉之前用我们配置的Seata代理
public class SeataMainApp2001 {

    public static void main(String[] args) {
        SpringApplication.run(SeataMainApp2001.class, args);
        System.out.println("启动成功");
    }
}
```



##### 2 seata-storage-service

pom文件

```xml
<dependencies>
        <!-- nacos -->
        <dependency>
            <groupId>com.alibaba.cloud</groupId>
            <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
        </dependency>
        <!-- seata -->
        <dependency>
            <groupId>com.alibaba.cloud</groupId>
            <artifactId>spring-cloud-starter-alibaba-seata</artifactId>
            <exclusions>
                <exclusion>
                    <artifactId>seata-all</artifactId>
                    <groupId>io.seata</groupId>
                </exclusion>
            </exclusions>
        </dependency>
        <dependency>
            <groupId>io.seata</groupId>
            <artifactId>seata-all</artifactId>
            <version>1.0.0</version>
        </dependency>
        <!-- feign -->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-openfeign</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>org.mybatis.spring.boot</groupId>
            <artifactId>mybatis-spring-boot-starter</artifactId>
            <version>2.0.0</version>
        </dependency>
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>5.1.37</version>
        </dependency>
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>druid-spring-boot-starter</artifactId>
            <version>1.1.10</version>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
    </dependencies>
```



yml文件

```yaml
server:
  port: 2002

spring:
  application:
    name: seata-storage-service
  cloud:
    alibaba:
      seata:
        tx-service-group: fsp_tx_group #自定义事务组名称需要与seata-server中的对应
    nacos:
      discovery:
        server-addr: localhost:8848
  datasource:
    driver-class-name: com.mysql.jdbc.Driver
    url: jdbc:mysql://localhost:3306/seata_storage
    username: root
    password: root

logging:
  level:
    io:
      seata: info

mybatis:
  mapperLocations: classpath:mapper/*.xml
```



file.conf文件

```properties
transport {
  # tcp udt unix-domain-socket
  type = "TCP"
  #NIO NATIVE
  server = "NIO"
  #enable heartbeat
  heartbeat = true
  #thread factory for netty
  thread-factory {
    boss-thread-prefix = "NettyBoss"
    worker-thread-prefix = "NettyServerNIOWorker"
    server-executor-thread-prefix = "NettyServerBizHandler"
    share-boss-worker = false
    client-selector-thread-prefix = "NettyClientSelector"
    client-selector-thread-size = 1
    client-worker-thread-prefix = "NettyClientWorkerThread"
    # netty boss thread size,will not be used for UDT
    boss-thread-size = 1
    #auto default pin or 8
    worker-thread-size = 8
  }
  shutdown {
    # when destroy server, wait seconds
    wait = 3
  }
  serialization = "seata"
  compressor = "none"
}

service {
  #vgroup->rgroup
  vgroup_mapping.fsp_tx_group = "default" #修改自定义事务组名称
  #only support single node
  default.grouplist = "127.0.0.1:8091"
  #degrade current not support
  enableDegrade = false
  #disable
  disable = false
  #unit ms,s,m,h,d represents milliseconds, seconds, minutes, hours, days, default permanent
  max.commit.retry.timeout = "-1"
  max.rollback.retry.timeout = "-1"
  disableGlobalTransaction = false
}

client {
  async.commit.buffer.limit = 10000
  lock {
    retry.internal = 10
    retry.times = 30
  }
  report.retry.count = 5
  tm.commit.retry.count = 1
  tm.rollback.retry.count = 1
}

transaction {
  undo.data.validation = true
  undo.log.serialization = "jackson"
  undo.log.save.days = 7
  #schedule delete expired undo_log in milliseconds
  undo.log.delete.period = 86400000
  undo.log.table = "undo_log"
}

support {
  ## spring
  spring {
    # auto proxy the DataSource bean
    datasource.autoproxy = false
  }
}
```



registry.conf

```properties
registry {
  # file 、nacos 、eureka、redis、zk
  type = "nacos"

  nacos {
    serverAddr = "localhost:8848"
    namespace = ""
    cluster = "default"
  }
  eureka {
    serviceUrl = "http://localhost:8761/eureka"
    application = "default"
    weight = "1"
  }
  redis {
    serverAddr = "localhost:6381"
    db = "0"
  }
  zk {
    cluster = "default"
    serverAddr = "127.0.0.1:2181"
    session.timeout = 6000
    connect.timeout = 2000
  }
  file {
    name = "file.conf"
  }
}

config {
  # file、nacos 、apollo、zk
  type = "file"

  nacos {
    serverAddr = "localhost"
    namespace = ""
    cluster = "default"
  }
  apollo {
    app.id = "fescar-server"
    apollo.meta = "http://192.168.1.204:8801"
  }
  zk {
    serverAddr = "127.0.0.1:2181"
    session.timeout = 6000
    connect.timeout = 2000
  }
  file {
    name = "file.conf"
  }
}
```



controller类

```java
@RestController
public class StorageController {

    @Resource
    private StorageService storageService;

    /**
     * 扣减库存
     */
    @RequestMapping("/storage/decrease")
    public CommonResult decrease(Long productId, Integer count) {
        storageService.decrease(productId, count);
        return new CommonResult(200, "扣减库存成功！");
    }
}
```



service类

```java
public interface StorageService {
    /**
     * 扣减库存
     *
     * @param productId
     * @param count
     */
    void decrease(Long productId, Integer count);
}
```



impl类

```java
@Service
public class StorageServiceImpl implements StorageService {

    private static final Logger LOGGER = LoggerFactory.getLogger(StorageServiceImpl.class);

    @Resource
    private StorageDao storageDao;

    /**
     * 扣减库存
     */
    @Override
    public void decrease(Long productId, Integer count) {
        LOGGER.info("------->storage-service中扣减库存开始");
        storageDao.decrease(productId, count);
        LOGGER.info("------->storage-service中扣减库存结束");
    }
}
```



mapper类

```java
@Mapper
public interface StorageDao {

    //扣减库存
    void decrease(@Param("productId") Long productId, @Param("count") Integer count);
}
```



xml

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" "http://mybatis.org/dtd/mybatis-3-mapper.dtd" >


<mapper namespace="com.wjz.springcloud.alibaba.dao.StorageDao">

    <resultMap id="BaseResultMap" type="com.wjz.springcloud.alibaba.domain.Storage">
        <id column="id" property="id" jdbcType="BIGINT"/>
        <result column="product_id" property="productId" jdbcType="BIGINT"/>
        <result column="total" property="total" jdbcType="INTEGER"/>
        <result column="used" property="used" jdbcType="INTEGER"/>
        <result column="residue" property="residue" jdbcType="INTEGER"/>
    </resultMap>

    <update id="decrease">
        UPDATE
            t_storage
        SET used    = used + #{count},
            residue = residue - #{count}
        WHERE product_id = #{productId}
    </update>

</mapper>
```



domain（实体类）

```java
@Data
@AllArgsConstructor
@NoArgsConstructor
public class Storage {

    private Long id;

    /**
     * 产品id
     */
    private Long productId;

    /**
     * 总库存
     */
    private Integer total;

    /**
     * 已用库存
     */
    private Integer used;

    /**
     * 剩余库存
     */
    private Integer residue;
}
```



##### 3seata-account-service

yml文件改个端口号和文件名就行了，conf文件和2002一样，config文件和2002一样，唯一不同的就是业务类。

controller类

```java
@RestController
public class AccountController {

    @Resource
    AccountService accountService;

    /**
     * 扣减账户余额
     */
    @RequestMapping("/account/decrease")
    public CommonResult decrease(@RequestParam("userId") Long userId, @RequestParam("money") BigDecimal money){
        accountService.decrease(userId,money);
        return new CommonResult(200,"扣减账户余额成功！");
    }
}
```



service类

```java
public interface AccountService {

    /**
     * 扣减账户余额
     * @param userId 用户id
     * @param money 金额
     */
    void decrease(@RequestParam("userId") Long userId, @RequestParam("money") BigDecimal money);
}
```



impl类

```java
@Service
public class AccountServiceImpl implements AccountService {
    private static final Logger LOGGER = LoggerFactory.getLogger(AccountServiceImpl.class);


    @Resource
    AccountDao accountDao;

    /**
     * 扣减账户余额
     */
    @Override
    public void decrease(Long userId, BigDecimal money) {
        LOGGER.info("------->account-service中扣减账户余额开始");
        accountDao.decrease(userId, money);
        LOGGER.info("------->account-service中扣减账户余额结束");
    }
}
```



domain(实体类)

```java
@Data
@AllArgsConstructor
@NoArgsConstructor
public class Account {

    private Long id;

    /**
     * 用户id
     */
    private Long userId;

    /**
     * 总额度
     */
    private BigDecimal total;

    /**
     * 已用额度
     */
    private BigDecimal used;

    /**
     * 剩余额度
     */
    private BigDecimal residue;
}
```



mapper类

```java
@Mapper
public interface AccountDao {

    /**
     * 扣减账户余额
     */
    void decrease(@Param("userId") Long userId, @Param("money") BigDecimal money);
}
```

xml文件

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" "http://mybatis.org/dtd/mybatis-3-mapper.dtd" >

<mapper namespace="com.wjz.springcloud.alibaba.dao.AccountDao">

    <resultMap id="BaseResultMap" type="com.wjz.springcloud.alibaba.domain.Account">
        <id column="id" property="id" jdbcType="BIGINT"/>
        <result column="user_id" property="userId" jdbcType="BIGINT"/>
        <result column="total" property="total" jdbcType="DECIMAL"/>
        <result column="used" property="used" jdbcType="DECIMAL"/>
        <result column="residue" property="residue" jdbcType="DECIMAL"/>
    </resultMap>

    <update id="decrease">
        UPDATE t_account
        SET residue = residue - #{money},
            used    = used + #{money}
        WHERE user_id = #{userId};
    </update>

</mapper>
```

主启动类上面要加上@SpringBootApplication(exclude = DataSourceAutoConfiguration.class)，@EnableDiscoveryClient，@EnableFeignClients注解。



### 6.Seata@GlobalTranscational验证

我们要对比一下没加这个注解之前出异常的结果和加注解之后出异常了如何处理。我们先启动2001,2002,2003这个三个微服务然后访问2001的下订单的接口。

我们先看一下数据库的初始情况

![在这里插入图片描述](https://img-blog.csdnimg.cn/3edb95f0ba994350a27bb8a01e46660f.png#pic_center)

这个是订单表，因为一开始没人下单所以一开始的数据都是空的。

![在这里插入图片描述](https://img-blog.csdnimg.cn/0c7ccbb87d8a4b08bd906e803bcf89f9.png#pic_center)

库存表之前的总库存是100，已用库存为0，剩余库存也是100

![在这里插入图片描述](https://img-blog.csdnimg.cn/215486cc10cc49da99ba670c040f99a5.png#pic_center)



这张是账户表因为啥也没买所以used为0



#### 1没加@GlobalTranscational

然后我们先下一个订单观察数据库的变化。

![在这里插入图片描述](https://img-blog.csdnimg.cn/611abb88d5df4922acdf9a39ee348ff7.png#pic_center)

![在这里插入图片描述](https://img-blog.csdnimg.cn/38b1c202276841eab53d7dead831cc07.png#pic_center)



1号顾客买了1号商品数量是10个，花了100元状态是1已完成。

![在这里插入图片描述](https://img-blog.csdnimg.cn/2313da0504e64a8c81eeed49e5e7c9bd.png#pic_center)

库存还剩90个。

![在这里插入图片描述](https://img-blog.csdnimg.cn/6d61fc4bd558495e99e4e7d53a8d3fcd.png#pic_center)



账户表花了100还剩900。

然后我们模拟一下超时异常在Account账户减少这块让他睡20秒钟。

```java
@Service
public class AccountServiceImpl implements AccountService {
    private static final Logger LOGGER = LoggerFactory.getLogger(AccountServiceImpl.class);


    @Resource
    AccountDao accountDao;

    /**
     * 扣减账户余额
     */
    @Override
    public void decrease(Long userId, BigDecimal money) {
        LOGGER.info("------->account-service中扣减账户余额开始");
        //模拟超时异常
        try {
            TimeUnit.SECONDS.sleep(20);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        accountDao.decrease(userId, money);
        LOGGER.info("------->account-service中扣减账户余额结束");
    }
}
```



![在这里插入图片描述](https://img-blog.csdnimg.cn/2049c655900748ab8bd4eefb44749be5.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5ripSlo=,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)

可以发现我们访问同样的地址由于存在超时异常所以会报错。

![在这里插入图片描述](https://img-blog.csdnimg.cn/788eb9b4a6054cba99545f691125dc77.png#pic_center)



那既然在支付的时候超时了那么这一单肯定是失败的所以status是0下单失败。然后我们看库存表，

![在这里插入图片描述](https://img-blog.csdnimg.cn/f46c9113daa94a4ba320f35e8f51dc8b.png#pic_center)

既然这一单失败了他居然减少了10就剩80了，这肯定是不对的。然后看看账户表

![在这里插入图片描述](https://img-blog.csdnimg.cn/8e0de9b228264523958472ae6b6af412.png#pic_center)



下单失败结果我还被扣钱了，这也是不对滴。



#### 2加上@GlobalTranscational之后

既然没加这个注解会产生问题，那么我们再看看加上之后对全局事务进行控制看看能不能解决问题

@Service
@Slf4j
public class OrderServiceImpl implements OrderService {
    @Resource
    private OrderDao orderDao;
    @Resource
    private StorageService storageService;
    @Resource
    private AccountService accountService;


```java
@Override
@GlobalTransactional(name = "fsp-create-order", rollbackFor = Exception.class)
public void create(Order order) {
    log.info("----->开始新建订单");
    //1 新建订单
    orderDao.create(order);

    //2 扣减库存
    log.info("----->订单微服务开始调用库存，做扣减Count");
    storageService.decrease(order.getProductId(), order.getCount());
    log.info("----->订单微服务开始调用库存，做扣减end");

    //3 扣减账户
    log.info("----->订单微服务开始调用账户，做扣减Money");
    accountService.decrease(order.getUserId(), order.getMoney());
    log.info("----->订单微服务开始调用账户，做扣减end");

    //4 修改订单状态，从零到1,1代表已经完成
    log.info("----->修改订单状态开始");
    orderDao.update(order.getUserId(), 0);
    log.info("----->修改订单状态结束");

    log.info("----->下订单结束了，O(∩_∩)O哈哈~");

}
```


然后我们再访问之前的接口

![在这里插入图片描述](https://img-blog.csdnimg.cn/03817b07d2ae42a3b8229f0e67fb84e7.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5ripSlo=,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)

加了这个全局事务控制的注解并不会改变什么依然报错但是我们来看看数据库

![在这里插入图片描述](https://img-blog.csdnimg.cn/73e43f6f1f404c71bd30972bef2807a2.png#pic_center)

发现这次出现异常的订单根本不会被落库。因为你出现异常了我就会回滚导致没有错误数据进库。
