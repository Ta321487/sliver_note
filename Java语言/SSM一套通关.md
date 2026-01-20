<!-- TOC -->

- [SSM一套通关](#ssm%E4%B8%80%E5%A5%97%E9%80%9A%E5%85%B3)
  - [Mybatis](#mybatis)
    - [Mybatis简介](#mybatis%E7%AE%80%E4%BB%8B)
      - [Mybatis历史](#mybatis%E5%8E%86%E5%8F%B2)
      - [Mybaits特性](#mybaits%E7%89%B9%E6%80%A7)
      - [Mybatis下载](#mybatis%E4%B8%8B%E8%BD%BD)
    - [mybatis_helloworld](#mybatis_helloworld)
      - [创建工程](#%E5%88%9B%E5%BB%BA%E5%B7%A5%E7%A8%8B)
      - [创建数据库](#%E5%88%9B%E5%BB%BA%E6%95%B0%E6%8D%AE%E5%BA%93)
      - [创建实体类](#%E5%88%9B%E5%BB%BA%E5%AE%9E%E4%BD%93%E7%B1%BB)
      - [Mybatis的核心配置文件](#mybatis%E7%9A%84%E6%A0%B8%E5%BF%83%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6)
      - [创建mapper接口](#%E5%88%9B%E5%BB%BAmapper%E6%8E%A5%E5%8F%A3)
      - [创建映射文件](#%E5%88%9B%E5%BB%BA%E6%98%A0%E5%B0%84%E6%96%87%E4%BB%B6)
      - [编写测试类（插入用户信息）](#%E7%BC%96%E5%86%99%E6%B5%8B%E8%AF%95%E7%B1%BB%E6%8F%92%E5%85%A5%E7%94%A8%E6%88%B7%E4%BF%A1%E6%81%AF)
      - [添加log4j日志文件](#%E6%B7%BB%E5%8A%A0log4j%E6%97%A5%E5%BF%97%E6%96%87%E4%BB%B6)
      - [将有关SqlSession的内容提取为一个工具类（Util）](#%E5%B0%86%E6%9C%89%E5%85%B3sqlsession%E7%9A%84%E5%86%85%E5%AE%B9%E6%8F%90%E5%8F%96%E4%B8%BA%E4%B8%80%E4%B8%AA%E5%B7%A5%E5%85%B7%E7%B1%BButil)
      - [修改用户信息](#%E4%BF%AE%E6%94%B9%E7%94%A8%E6%88%B7%E4%BF%A1%E6%81%AF)
      - [删除用户信息](#%E5%88%A0%E9%99%A4%E7%94%A8%E6%88%B7%E4%BF%A1%E6%81%AF)
      - [查询一条员工信息（根据员工ID）](#%E6%9F%A5%E8%AF%A2%E4%B8%80%E6%9D%A1%E5%91%98%E5%B7%A5%E4%BF%A1%E6%81%AF%E6%A0%B9%E6%8D%AE%E5%91%98%E5%B7%A5id)
      - [查询所有员工信息](#%E6%9F%A5%E8%AF%A2%E6%89%80%E6%9C%89%E5%91%98%E5%B7%A5%E4%BF%A1%E6%81%AF)
      - [利用IDEA的文件模板工具，快速生成框架](#%E5%88%A9%E7%94%A8idea%E7%9A%84%E6%96%87%E4%BB%B6%E6%A8%A1%E6%9D%BF%E5%B7%A5%E5%85%B7%E5%BF%AB%E9%80%9F%E7%94%9F%E6%88%90%E6%A1%86%E6%9E%B6)
    - [mybatis获取参数值的方式](#mybatis%E8%8E%B7%E5%8F%96%E5%8F%82%E6%95%B0%E5%80%BC%E7%9A%84%E6%96%B9%E5%BC%8F)
      - [mybatis的查询功能](#mybatis%E7%9A%84%E6%9F%A5%E8%AF%A2%E5%8A%9F%E8%83%BD)
      - [特殊SQL的执行](#%E7%89%B9%E6%AE%8Asql%E7%9A%84%E6%89%A7%E8%A1%8C)
    - [自定义映射：resultMap](#%E8%87%AA%E5%AE%9A%E4%B9%89%E6%98%A0%E5%B0%84resultmap)
      - [字段名和实体类中的属性名不一致](#%E5%AD%97%E6%AE%B5%E5%90%8D%E5%92%8C%E5%AE%9E%E4%BD%93%E7%B1%BB%E4%B8%AD%E7%9A%84%E5%B1%9E%E6%80%A7%E5%90%8D%E4%B8%8D%E4%B8%80%E8%87%B4)
      - [多对一关系](#%E5%A4%9A%E5%AF%B9%E4%B8%80%E5%85%B3%E7%B3%BB)
      - [一对多关系](#%E4%B8%80%E5%AF%B9%E5%A4%9A%E5%85%B3%E7%B3%BB)
    - [动态SQL](#%E5%8A%A8%E6%80%81sql)
    - [Mybatis的缓存](#mybatis%E7%9A%84%E7%BC%93%E5%AD%98)
      - [Mybatis的一级缓存](#mybatis%E7%9A%84%E4%B8%80%E7%BA%A7%E7%BC%93%E5%AD%98)
      - [MyBatis的二级缓存](#mybatis%E7%9A%84%E4%BA%8C%E7%BA%A7%E7%BC%93%E5%AD%98)
      - [Mybatis缓存查询的顺序](#mybatis%E7%BC%93%E5%AD%98%E6%9F%A5%E8%AF%A2%E7%9A%84%E9%A1%BA%E5%BA%8F)
      - [整合第三方缓存EHCache](#%E6%95%B4%E5%90%88%E7%AC%AC%E4%B8%89%E6%96%B9%E7%BC%93%E5%AD%98ehcache)
    - [Mybatis的逆向工程](#mybatis%E7%9A%84%E9%80%86%E5%90%91%E5%B7%A5%E7%A8%8B)
      - [创建逆向工程的步骤](#%E5%88%9B%E5%BB%BA%E9%80%86%E5%90%91%E5%B7%A5%E7%A8%8B%E7%9A%84%E6%AD%A5%E9%AA%A4)
    - [分页功能](#%E5%88%86%E9%A1%B5%E5%8A%9F%E8%83%BD)
      - [分页功能分析](#%E5%88%86%E9%A1%B5%E5%8A%9F%E8%83%BD%E5%88%86%E6%9E%90)
      - [分页插件](#%E5%88%86%E9%A1%B5%E6%8F%92%E4%BB%B6)
  - [Spring](#spring)
    - [Spring简介](#spring%E7%AE%80%E4%BB%8B)
      - [Spring概述](#spring%E6%A6%82%E8%BF%B0)
      - [Spring家族](#spring%E5%AE%B6%E6%97%8F)
      - [Spring Framework](#spring-framework)
        - [Spring Framework特性](#spring-framework%E7%89%B9%E6%80%A7)
        - [Spring Framework 五大功能模块](#spring-framework-%E4%BA%94%E5%A4%A7%E5%8A%9F%E8%83%BD%E6%A8%A1%E5%9D%97)
    - [IOC](#ioc)
      - [IOC容器](#ioc%E5%AE%B9%E5%99%A8)
        - [IOC思想](#ioc%E6%80%9D%E6%83%B3)
        - [IOC容器在Spring中的实现](#ioc%E5%AE%B9%E5%99%A8%E5%9C%A8spring%E4%B8%AD%E7%9A%84%E5%AE%9E%E7%8E%B0)
      - [基于XML管理bean](#%E5%9F%BA%E4%BA%8Exml%E7%AE%A1%E7%90%86bean)
        - [实验一：入门案例](#%E5%AE%9E%E9%AA%8C%E4%B8%80%E5%85%A5%E9%97%A8%E6%A1%88%E4%BE%8B)
        - [实验二：获取bean](#%E5%AE%9E%E9%AA%8C%E4%BA%8C%E8%8E%B7%E5%8F%96bean)
        - [实验三：依赖注入——setter注入](#%E5%AE%9E%E9%AA%8C%E4%B8%89%E4%BE%9D%E8%B5%96%E6%B3%A8%E5%85%A5setter%E6%B3%A8%E5%85%A5)
        - [实验四：依赖注入——构造器注入](#%E5%AE%9E%E9%AA%8C%E5%9B%9B%E4%BE%9D%E8%B5%96%E6%B3%A8%E5%85%A5%E6%9E%84%E9%80%A0%E5%99%A8%E6%B3%A8%E5%85%A5)
        - [实验五：特殊值处理](#%E5%AE%9E%E9%AA%8C%E4%BA%94%E7%89%B9%E6%AE%8A%E5%80%BC%E5%A4%84%E7%90%86)
        - [实验六：为类类型变量赋值](#%E5%AE%9E%E9%AA%8C%E5%85%AD%E4%B8%BA%E7%B1%BB%E7%B1%BB%E5%9E%8B%E5%8F%98%E9%87%8F%E8%B5%8B%E5%80%BC)
        - [实验七：为数组、集合类型赋值](#%E5%AE%9E%E9%AA%8C%E4%B8%83%E4%B8%BA%E6%95%B0%E7%BB%84%E9%9B%86%E5%90%88%E7%B1%BB%E5%9E%8B%E8%B5%8B%E5%80%BC)
        - [实验八：p命名空间为成员变量赋值](#%E5%AE%9E%E9%AA%8C%E5%85%ABp%E5%91%BD%E5%90%8D%E7%A9%BA%E9%97%B4%E4%B8%BA%E6%88%90%E5%91%98%E5%8F%98%E9%87%8F%E8%B5%8B%E5%80%BC)
        - [实验九：引入外部属性文件](#%E5%AE%9E%E9%AA%8C%E4%B9%9D%E5%BC%95%E5%85%A5%E5%A4%96%E9%83%A8%E5%B1%9E%E6%80%A7%E6%96%87%E4%BB%B6)
        - [实验十：bean的作用域](#%E5%AE%9E%E9%AA%8C%E5%8D%81bean%E7%9A%84%E4%BD%9C%E7%94%A8%E5%9F%9F)
        - [实验十一：bean的生命周期](#%E5%AE%9E%E9%AA%8C%E5%8D%81%E4%B8%80bean%E7%9A%84%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F)
        - [实验十三：FactoryBean](#%E5%AE%9E%E9%AA%8C%E5%8D%81%E4%B8%89factorybean)
        - [实验十四：基于XML的自动装配](#%E5%AE%9E%E9%AA%8C%E5%8D%81%E5%9B%9B%E5%9F%BA%E4%BA%8Exml%E7%9A%84%E8%87%AA%E5%8A%A8%E8%A3%85%E9%85%8D)
      - [基于注解管理bean](#%E5%9F%BA%E4%BA%8E%E6%B3%A8%E8%A7%A3%E7%AE%A1%E7%90%86bean)
        - [实验一：标记与扫描](#%E5%AE%9E%E9%AA%8C%E4%B8%80%E6%A0%87%E8%AE%B0%E4%B8%8E%E6%89%AB%E6%8F%8F)
        - [实验二：基于注解的自动装配](#%E5%AE%9E%E9%AA%8C%E4%BA%8C%E5%9F%BA%E4%BA%8E%E6%B3%A8%E8%A7%A3%E7%9A%84%E8%87%AA%E5%8A%A8%E8%A3%85%E9%85%8D)
    - [AOP](#aop)
      - [场景模拟](#%E5%9C%BA%E6%99%AF%E6%A8%A1%E6%8B%9F)
        - [声明接口](#%E5%A3%B0%E6%98%8E%E6%8E%A5%E5%8F%A3)
        - [创建实现类](#%E5%88%9B%E5%BB%BA%E5%AE%9E%E7%8E%B0%E7%B1%BB)
        - [创建带日志功能的实现类](#%E5%88%9B%E5%BB%BA%E5%B8%A6%E6%97%A5%E5%BF%97%E5%8A%9F%E8%83%BD%E7%9A%84%E5%AE%9E%E7%8E%B0%E7%B1%BB)
        - [提出问题](#%E6%8F%90%E5%87%BA%E9%97%AE%E9%A2%98)
      - [代理模式](#%E4%BB%A3%E7%90%86%E6%A8%A1%E5%BC%8F)
        - [概念](#%E6%A6%82%E5%BF%B5)
        - [静态代理](#%E9%9D%99%E6%80%81%E4%BB%A3%E7%90%86)
        - [动态代理](#%E5%8A%A8%E6%80%81%E4%BB%A3%E7%90%86)
      - [AOP概念及相关术语](#aop%E6%A6%82%E5%BF%B5%E5%8F%8A%E7%9B%B8%E5%85%B3%E6%9C%AF%E8%AF%AD)
        - [概述](#%E6%A6%82%E8%BF%B0)
        - [相关术语](#%E7%9B%B8%E5%85%B3%E6%9C%AF%E8%AF%AD)
        - [作用](#%E4%BD%9C%E7%94%A8)
      - [基于注解的AOP](#%E5%9F%BA%E4%BA%8E%E6%B3%A8%E8%A7%A3%E7%9A%84aop)
        - [技术说明](#%E6%8A%80%E6%9C%AF%E8%AF%B4%E6%98%8E)
        - [准备工作](#%E5%87%86%E5%A4%87%E5%B7%A5%E4%BD%9C)
        - [创建切面类并配置](#%E5%88%9B%E5%BB%BA%E5%88%87%E9%9D%A2%E7%B1%BB%E5%B9%B6%E9%85%8D%E7%BD%AE)
        - [各种通知](#%E5%90%84%E7%A7%8D%E9%80%9A%E7%9F%A5)
        - [切入点表达式语法](#%E5%88%87%E5%85%A5%E7%82%B9%E8%A1%A8%E8%BE%BE%E5%BC%8F%E8%AF%AD%E6%B3%95)
        - [重用切入点表达式](#%E9%87%8D%E7%94%A8%E5%88%87%E5%85%A5%E7%82%B9%E8%A1%A8%E8%BE%BE%E5%BC%8F)
        - [获取通知的相关信息](#%E8%8E%B7%E5%8F%96%E9%80%9A%E7%9F%A5%E7%9A%84%E7%9B%B8%E5%85%B3%E4%BF%A1%E6%81%AF)
        - [环绕通知](#%E7%8E%AF%E7%BB%95%E9%80%9A%E7%9F%A5)
        - [切面的优先级](#%E5%88%87%E9%9D%A2%E7%9A%84%E4%BC%98%E5%85%88%E7%BA%A7)
      - [基于XML的AOP（了解）](#%E5%9F%BA%E4%BA%8Exml%E7%9A%84aop%E4%BA%86%E8%A7%A3)
        - [准备工作（参考基于注解的AOP环境）](#%E5%87%86%E5%A4%87%E5%B7%A5%E4%BD%9C%E5%8F%82%E8%80%83%E5%9F%BA%E4%BA%8E%E6%B3%A8%E8%A7%A3%E7%9A%84aop%E7%8E%AF%E5%A2%83)
        - [实现](#%E5%AE%9E%E7%8E%B0)
    - [声明式事务](#%E5%A3%B0%E6%98%8E%E5%BC%8F%E4%BA%8B%E5%8A%A1)
      - [JDBCTemplate](#jdbctemplate)
        - [简介](#%E7%AE%80%E4%BB%8B)
        - [准备工作](#%E5%87%86%E5%A4%87%E5%B7%A5%E4%BD%9C)
        - [测试](#%E6%B5%8B%E8%AF%95)
      - [声明式事务概念](#%E5%A3%B0%E6%98%8E%E5%BC%8F%E4%BA%8B%E5%8A%A1%E6%A6%82%E5%BF%B5)
        - [编程式事务](#%E7%BC%96%E7%A8%8B%E5%BC%8F%E4%BA%8B%E5%8A%A1)
        - [声明式事务](#%E5%A3%B0%E6%98%8E%E5%BC%8F%E4%BA%8B%E5%8A%A1)
      - [基于注解的声明式事务](#%E5%9F%BA%E4%BA%8E%E6%B3%A8%E8%A7%A3%E7%9A%84%E5%A3%B0%E6%98%8E%E5%BC%8F%E4%BA%8B%E5%8A%A1)
        - [准备工作](#%E5%87%86%E5%A4%87%E5%B7%A5%E4%BD%9C)
        - [测试无事务情况](#%E6%B5%8B%E8%AF%95%E6%97%A0%E4%BA%8B%E5%8A%A1%E6%83%85%E5%86%B5)
        - [加入事务](#%E5%8A%A0%E5%85%A5%E4%BA%8B%E5%8A%A1)
        - [@Transactional注解标识的位置](#transactional%E6%B3%A8%E8%A7%A3%E6%A0%87%E8%AF%86%E7%9A%84%E4%BD%8D%E7%BD%AE)
        - [事务属性：只读](#%E4%BA%8B%E5%8A%A1%E5%B1%9E%E6%80%A7%E5%8F%AA%E8%AF%BB)
        - [事务属性：超时](#%E4%BA%8B%E5%8A%A1%E5%B1%9E%E6%80%A7%E8%B6%85%E6%97%B6)
        - [事务属性：回滚策略](#%E4%BA%8B%E5%8A%A1%E5%B1%9E%E6%80%A7%E5%9B%9E%E6%BB%9A%E7%AD%96%E7%95%A5)
        - [事务属性：事务隔离级别](#%E4%BA%8B%E5%8A%A1%E5%B1%9E%E6%80%A7%E4%BA%8B%E5%8A%A1%E9%9A%94%E7%A6%BB%E7%BA%A7%E5%88%AB)
        - [事务属性：事务传播行为](#%E4%BA%8B%E5%8A%A1%E5%B1%9E%E6%80%A7%E4%BA%8B%E5%8A%A1%E4%BC%A0%E6%92%AD%E8%A1%8C%E4%B8%BA)
      - [基于XML的声明式事务](#%E5%9F%BA%E4%BA%8Exml%E7%9A%84%E5%A3%B0%E6%98%8E%E5%BC%8F%E4%BA%8B%E5%8A%A1)
        - [场景模拟（参考基于注解的声明式事务）](#%E5%9C%BA%E6%99%AF%E6%A8%A1%E6%8B%9F%E5%8F%82%E8%80%83%E5%9F%BA%E4%BA%8E%E6%B3%A8%E8%A7%A3%E7%9A%84%E5%A3%B0%E6%98%8E%E5%BC%8F%E4%BA%8B%E5%8A%A1)
        - [修改Spring配置文件](#%E4%BF%AE%E6%94%B9spring%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6)
  - [SpringMVC](#springmvc)
    - [SpringMVC简介](#springmvc%E7%AE%80%E4%BB%8B)
      - [什么是MVC](#%E4%BB%80%E4%B9%88%E6%98%AFmvc)
      - [什么是SpringMVC](#%E4%BB%80%E4%B9%88%E6%98%AFspringmvc)
      - [SpringMVC的特点](#springmvc%E7%9A%84%E7%89%B9%E7%82%B9)
    - [入门案例](#%E5%85%A5%E9%97%A8%E6%A1%88%E4%BE%8B)
      - [开发环境](#%E5%BC%80%E5%8F%91%E7%8E%AF%E5%A2%83)
      - [创建Maven工程](#%E5%88%9B%E5%BB%BAmaven%E5%B7%A5%E7%A8%8B)
        - [配置web.xml](#%E9%85%8D%E7%BD%AEwebxml)
        - [创建请求控制器](#%E5%88%9B%E5%BB%BA%E8%AF%B7%E6%B1%82%E6%8E%A7%E5%88%B6%E5%99%A8)
        - [创建SpringMVC的配置文件](#%E5%88%9B%E5%BB%BAspringmvc%E7%9A%84%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6)
        - [测试helloworld](#%E6%B5%8B%E8%AF%95helloworld)
        - [总结](#%E6%80%BB%E7%BB%93)
    - [@RequestMapping注解](#requestmapping%E6%B3%A8%E8%A7%A3)
      - [RequestMapping注解的功能](#requestmapping%E6%B3%A8%E8%A7%A3%E7%9A%84%E5%8A%9F%E8%83%BD)
      - [@RequestMapping注解的位置](#requestmapping%E6%B3%A8%E8%A7%A3%E7%9A%84%E4%BD%8D%E7%BD%AE)
      - [@RequestMapping注解的value属性](#requestmapping%E6%B3%A8%E8%A7%A3%E7%9A%84value%E5%B1%9E%E6%80%A7)
      - [@RequestMapping注解的method属性](#requestmapping%E6%B3%A8%E8%A7%A3%E7%9A%84method%E5%B1%9E%E6%80%A7)
      - [@RequestMapping注解的params属性（了解）](#requestmapping%E6%B3%A8%E8%A7%A3%E7%9A%84params%E5%B1%9E%E6%80%A7%E4%BA%86%E8%A7%A3)
      - [@RequestMapping注解的headers属性（了解）](#requestmapping%E6%B3%A8%E8%A7%A3%E7%9A%84headers%E5%B1%9E%E6%80%A7%E4%BA%86%E8%A7%A3)
      - [SpringMVC支持ant风格的路径](#springmvc%E6%94%AF%E6%8C%81ant%E9%A3%8E%E6%A0%BC%E7%9A%84%E8%B7%AF%E5%BE%84)
      - [SpringMVC支持路径中的占位符（重点）](#springmvc%E6%94%AF%E6%8C%81%E8%B7%AF%E5%BE%84%E4%B8%AD%E7%9A%84%E5%8D%A0%E4%BD%8D%E7%AC%A6%E9%87%8D%E7%82%B9)
    - [SpringMVC获取请求参数](#springmvc%E8%8E%B7%E5%8F%96%E8%AF%B7%E6%B1%82%E5%8F%82%E6%95%B0)
      - [通过ServletAPI获取](#%E9%80%9A%E8%BF%87servletapi%E8%8E%B7%E5%8F%96)
      - [通过控制器方法的形参获取请求参数](#%E9%80%9A%E8%BF%87%E6%8E%A7%E5%88%B6%E5%99%A8%E6%96%B9%E6%B3%95%E7%9A%84%E5%BD%A2%E5%8F%82%E8%8E%B7%E5%8F%96%E8%AF%B7%E6%B1%82%E5%8F%82%E6%95%B0)
      - [@RequestParam注解](#requestparam%E6%B3%A8%E8%A7%A3)
      - [@RequestHeader注解](#requestheader%E6%B3%A8%E8%A7%A3)
      - [@CookieValue注解](#cookievalue%E6%B3%A8%E8%A7%A3)
      - [通过POJO获取请求参数](#%E9%80%9A%E8%BF%87pojo%E8%8E%B7%E5%8F%96%E8%AF%B7%E6%B1%82%E5%8F%82%E6%95%B0)
      - [解决获取请求的乱码问题（method为POST）](#%E8%A7%A3%E5%86%B3%E8%8E%B7%E5%8F%96%E8%AF%B7%E6%B1%82%E7%9A%84%E4%B9%B1%E7%A0%81%E9%97%AE%E9%A2%98method%E4%B8%BApost)
    - [域对象共享数据](#%E5%9F%9F%E5%AF%B9%E8%B1%A1%E5%85%B1%E4%BA%AB%E6%95%B0%E6%8D%AE)
      - [使用ServletAPI向request域对象共享数据](#%E4%BD%BF%E7%94%A8servletapi%E5%90%91request%E5%9F%9F%E5%AF%B9%E8%B1%A1%E5%85%B1%E4%BA%AB%E6%95%B0%E6%8D%AE)
      - [使用ModelAndView向request域对象共享数据](#%E4%BD%BF%E7%94%A8modelandview%E5%90%91request%E5%9F%9F%E5%AF%B9%E8%B1%A1%E5%85%B1%E4%BA%AB%E6%95%B0%E6%8D%AE)
      - [使用Model向request域对象共享数据](#%E4%BD%BF%E7%94%A8model%E5%90%91request%E5%9F%9F%E5%AF%B9%E8%B1%A1%E5%85%B1%E4%BA%AB%E6%95%B0%E6%8D%AE)
      - [使用map向request域对象共享数据](#%E4%BD%BF%E7%94%A8map%E5%90%91request%E5%9F%9F%E5%AF%B9%E8%B1%A1%E5%85%B1%E4%BA%AB%E6%95%B0%E6%8D%AE)
      - [使用ModelMap向request域对象共享数据](#%E4%BD%BF%E7%94%A8modelmap%E5%90%91request%E5%9F%9F%E5%AF%B9%E8%B1%A1%E5%85%B1%E4%BA%AB%E6%95%B0%E6%8D%AE)
      - [Model、ModelMap、Map的关系](#modelmodelmapmap%E7%9A%84%E5%85%B3%E7%B3%BB)
      - [向session域共享数据](#%E5%90%91session%E5%9F%9F%E5%85%B1%E4%BA%AB%E6%95%B0%E6%8D%AE)
      - [向application域共享数据](#%E5%90%91application%E5%9F%9F%E5%85%B1%E4%BA%AB%E6%95%B0%E6%8D%AE)
    - [SpringMVC的视图](#springmvc%E7%9A%84%E8%A7%86%E5%9B%BE)
      - [ThymeleafView](#thymeleafview)
      - [转发视图](#%E8%BD%AC%E5%8F%91%E8%A7%86%E5%9B%BE)
      - [重定向视图](#%E9%87%8D%E5%AE%9A%E5%90%91%E8%A7%86%E5%9B%BE)
      - [视图控制器：view-controller](#%E8%A7%86%E5%9B%BE%E6%8E%A7%E5%88%B6%E5%99%A8view-controller)
    - [RESTful](#restful)
      - [RESTful简介](#restful%E7%AE%80%E4%BB%8B)
        - [资源](#%E8%B5%84%E6%BA%90)
        - [资源的表述](#%E8%B5%84%E6%BA%90%E7%9A%84%E8%A1%A8%E8%BF%B0)
        - [状态转移](#%E7%8A%B6%E6%80%81%E8%BD%AC%E7%A7%BB)
      - [RESTful的实现](#restful%E7%9A%84%E5%AE%9E%E7%8E%B0)
      - [HiddenHttpMethodFilter](#hiddenhttpmethodfilter)
    - [RESTful案例](#restful%E6%A1%88%E4%BE%8B)
      - [准备工作](#%E5%87%86%E5%A4%87%E5%B7%A5%E4%BD%9C)
      - [功能清单](#%E5%8A%9F%E8%83%BD%E6%B8%85%E5%8D%95)
      - [具体功能：访问首页](#%E5%85%B7%E4%BD%93%E5%8A%9F%E8%83%BD%E8%AE%BF%E9%97%AE%E9%A6%96%E9%A1%B5)
        - [配置view-controller](#%E9%85%8D%E7%BD%AEview-controller)
        - [创建页面](#%E5%88%9B%E5%BB%BA%E9%A1%B5%E9%9D%A2)
      - [具体功能：查询所有员工信息](#%E5%85%B7%E4%BD%93%E5%8A%9F%E8%83%BD%E6%9F%A5%E8%AF%A2%E6%89%80%E6%9C%89%E5%91%98%E5%B7%A5%E4%BF%A1%E6%81%AF)
        - [控制器方法](#%E6%8E%A7%E5%88%B6%E5%99%A8%E6%96%B9%E6%B3%95)
        - [创建employee_list.html](#%E5%88%9B%E5%BB%BAemployee_listhtml)
      - [具体功能：添加员工信息](#%E5%85%B7%E4%BD%93%E5%8A%9F%E8%83%BD%E6%B7%BB%E5%8A%A0%E5%91%98%E5%B7%A5%E4%BF%A1%E6%81%AF)
        - [控制器方法](#%E6%8E%A7%E5%88%B6%E5%99%A8%E6%96%B9%E6%B3%95)
        - [创建employee_add.html](#%E5%88%9B%E5%BB%BAemployee_addhtml)
        - [具体功能：修改员工信息和根据ID查询员工信息](#%E5%85%B7%E4%BD%93%E5%8A%9F%E8%83%BD%E4%BF%AE%E6%94%B9%E5%91%98%E5%B7%A5%E4%BF%A1%E6%81%AF%E5%92%8C%E6%A0%B9%E6%8D%AEid%E6%9F%A5%E8%AF%A2%E5%91%98%E5%B7%A5%E4%BF%A1%E6%81%AF)
        - [控制器方法](#%E6%8E%A7%E5%88%B6%E5%99%A8%E6%96%B9%E6%B3%95)
      - [创建employee_update.html](#%E5%88%9B%E5%BB%BAemployee_updatehtml)
      - [具体功能：删除员工信息](#%E5%85%B7%E4%BD%93%E5%8A%9F%E8%83%BD%E5%88%A0%E9%99%A4%E5%91%98%E5%B7%A5%E4%BF%A1%E6%81%AF)
        - [控制器方法](#%E6%8E%A7%E5%88%B6%E5%99%A8%E6%96%B9%E6%B3%95)
    - [SpringMVC处理Ajax请求](#springmvc%E5%A4%84%E7%90%86ajax%E8%AF%B7%E6%B1%82)
      - [@RequestBody](#requestbody)
      - [@RequestBody获取json格式的请求参数](#requestbody%E8%8E%B7%E5%8F%96json%E6%A0%BC%E5%BC%8F%E7%9A%84%E8%AF%B7%E6%B1%82%E5%8F%82%E6%95%B0)
      - [@ResponseBody](#responsebody)
      - [@ResponseBody响应浏览器json数据](#responsebody%E5%93%8D%E5%BA%94%E6%B5%8F%E8%A7%88%E5%99%A8json%E6%95%B0%E6%8D%AE)
      - [@RestController注解](#restcontroller%E6%B3%A8%E8%A7%A3)
    - [文件上传和下载](#%E6%96%87%E4%BB%B6%E4%B8%8A%E4%BC%A0%E5%92%8C%E4%B8%8B%E8%BD%BD)
      - [文件下载](#%E6%96%87%E4%BB%B6%E4%B8%8B%E8%BD%BD)
      - [文件上传](#%E6%96%87%E4%BB%B6%E4%B8%8A%E4%BC%A0)
        - [添加依赖](#%E6%B7%BB%E5%8A%A0%E4%BE%9D%E8%B5%96)
        - [在SpringMVC的配置文件添加配置](#%E5%9C%A8springmvc%E7%9A%84%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6%E6%B7%BB%E5%8A%A0%E9%85%8D%E7%BD%AE)
        - [控制器方法](#%E6%8E%A7%E5%88%B6%E5%99%A8%E6%96%B9%E6%B3%95)
        - [附：避免上传的文件被覆盖](#%E9%99%84%E9%81%BF%E5%85%8D%E4%B8%8A%E4%BC%A0%E7%9A%84%E6%96%87%E4%BB%B6%E8%A2%AB%E8%A6%86%E7%9B%96)
    - [拦截器](#%E6%8B%A6%E6%88%AA%E5%99%A8)
      - [拦截器的配置](#%E6%8B%A6%E6%88%AA%E5%99%A8%E7%9A%84%E9%85%8D%E7%BD%AE)
      - [拦截器的三个抽象方法](#%E6%8B%A6%E6%88%AA%E5%99%A8%E7%9A%84%E4%B8%89%E4%B8%AA%E6%8A%BD%E8%B1%A1%E6%96%B9%E6%B3%95)
      - [多个拦截器的执行顺序](#%E5%A4%9A%E4%B8%AA%E6%8B%A6%E6%88%AA%E5%99%A8%E7%9A%84%E6%89%A7%E8%A1%8C%E9%A1%BA%E5%BA%8F)
    - [异常处理器](#%E5%BC%82%E5%B8%B8%E5%A4%84%E7%90%86%E5%99%A8)
      - [基于配置的异常处理](#%E5%9F%BA%E4%BA%8E%E9%85%8D%E7%BD%AE%E7%9A%84%E5%BC%82%E5%B8%B8%E5%A4%84%E7%90%86)
      - [基于注解的异常处理](#%E5%9F%BA%E4%BA%8E%E6%B3%A8%E8%A7%A3%E7%9A%84%E5%BC%82%E5%B8%B8%E5%A4%84%E7%90%86)
    - [注解配置SpringMVC](#%E6%B3%A8%E8%A7%A3%E9%85%8D%E7%BD%AEspringmvc)
      - [创建初始化类，代替web.xml](#%E5%88%9B%E5%BB%BA%E5%88%9D%E5%A7%8B%E5%8C%96%E7%B1%BB%E4%BB%A3%E6%9B%BFwebxml)
      - [创建SpringConfig配置类，代替spring的配置文件](#%E5%88%9B%E5%BB%BAspringconfig%E9%85%8D%E7%BD%AE%E7%B1%BB%E4%BB%A3%E6%9B%BFspring%E7%9A%84%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6)
      - [创建WebConfig配置类，代替SpringMVC的配置文件](#%E5%88%9B%E5%BB%BAwebconfig%E9%85%8D%E7%BD%AE%E7%B1%BB%E4%BB%A3%E6%9B%BFspringmvc%E7%9A%84%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6)
      - [测试功能](#%E6%B5%8B%E8%AF%95%E5%8A%9F%E8%83%BD)
    - [SpringMVC执行流程](#springmvc%E6%89%A7%E8%A1%8C%E6%B5%81%E7%A8%8B)
      - [SpringMVC常用组件](#springmvc%E5%B8%B8%E7%94%A8%E7%BB%84%E4%BB%B6)
      - [DispatcherServlet初始化过程](#dispatcherservlet%E5%88%9D%E5%A7%8B%E5%8C%96%E8%BF%87%E7%A8%8B)
        - [初始化WebApplicationContext](#%E5%88%9D%E5%A7%8B%E5%8C%96webapplicationcontext)
        - [创建WebApplicationContext](#%E5%88%9B%E5%BB%BAwebapplicationcontext)
        - [DispatcherServlet初始化策略](#dispatcherservlet%E5%88%9D%E5%A7%8B%E5%8C%96%E7%AD%96%E7%95%A5)
      - [DispatcherServlet调用组件处理请求](#dispatcherservlet%E8%B0%83%E7%94%A8%E7%BB%84%E4%BB%B6%E5%A4%84%E7%90%86%E8%AF%B7%E6%B1%82)
        - [processRequest](#processrequest)
        - [doService](#doservice)
        - [doDispatch](#dodispatch)
        - [processDispatchResult](#processdispatchresult)
      - [SpringMVC的执行流程](#springmvc%E7%9A%84%E6%89%A7%E8%A1%8C%E6%B5%81%E7%A8%8B)
  - [SSM整合](#ssm%E6%95%B4%E5%90%88)
    - [ContextLoaderListener](#contextloaderlistener)
    - [准备工作](#%E5%87%86%E5%A4%87%E5%B7%A5%E4%BD%9C)
      - [创建Maven 模块](#%E5%88%9B%E5%BB%BAmaven-%E6%A8%A1%E5%9D%97)
      - [导入依赖](#%E5%AF%BC%E5%85%A5%E4%BE%9D%E8%B5%96)
      - [创建表](#%E5%88%9B%E5%BB%BA%E8%A1%A8)
    - [配置web.xml](#%E9%85%8D%E7%BD%AEwebxml)
    - [创建SpringMVC的配置文件](#%E5%88%9B%E5%BB%BAspringmvc%E7%9A%84%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6)
    - [搭建MyBatis环境](#%E6%90%AD%E5%BB%BAmybatis%E7%8E%AF%E5%A2%83)
      - [创建jdbc.properties文件](#%E5%88%9B%E5%BB%BAjdbcproperties%E6%96%87%E4%BB%B6)
      - [配置mybatis-config文件](#%E9%85%8D%E7%BD%AEmybatis-config%E6%96%87%E4%BB%B6)
      - [创建Mapper接口和映射文件](#%E5%88%9B%E5%BB%BAmapper%E6%8E%A5%E5%8F%A3%E5%92%8C%E6%98%A0%E5%B0%84%E6%96%87%E4%BB%B6)
      - [创建日志文件log4j.xml](#%E5%88%9B%E5%BB%BA%E6%97%A5%E5%BF%97%E6%96%87%E4%BB%B6log4jxml)
    - [创建Spring的配置文件并配置](#%E5%88%9B%E5%BB%BAspring%E7%9A%84%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6%E5%B9%B6%E9%85%8D%E7%BD%AE)
    - [测试功能](#%E6%B5%8B%E8%AF%95%E5%8A%9F%E8%83%BD)
      - [创建组件](#%E5%88%9B%E5%BB%BA%E7%BB%84%E4%BB%B6)
      - [创建页面](#%E5%88%9B%E5%BB%BA%E9%A1%B5%E9%9D%A2)
      - [最终结果](#%E6%9C%80%E7%BB%88%E7%BB%93%E6%9E%9C)

<!-- /TOC -->

# SSM一套通关

> （本笔记使用IDEA作为开发工具）

## Mybatis

### Mybatis简介

#### Mybatis历史

- MyBatis最初是Apache的一个开源项目iBatis, 2010年6月这个项目由Apache Software Foundation迁移到了Google Code。随着开发团队转投Google Code旗下，iBatis3.x正式更名为MyBatis。代码于2013年11月迁移到Github。
- iBatis一词来源于“internet”和“abatis”的组合，是一个基于Java的持久层框架。iBatis提供的持久层框架包括SQL Maps和Data Access Objects（DAO）

#### Mybaits特性

1. MyBatis 是支持定制化 SQL、存储过程以及高级映射的优秀的持久层框架
2. MyBatis 避免了几乎所有的 JDBC 代码和手动设置参数以及获取结果集
3. MyBatis可以使用简单的XML或注解用于配置和原始映射，将接口和Java的POJO（Plain Old Java Objects，普通的Java对象）映射成数据库中的记录
4. MyBatis 是一个半自动的ORM（Object Relation Mapping）框架

#### Mybatis下载

1. Mybatis中文网：<https://mybatis.net.cn/getting-started.html>
2. GitHub仓库：<https://github.com/mybatis/mybatis-3>
3. 原版网站：<https://mybatis.org/mybatis-3/>

### mybatis_helloworld

#### 创建工程

1. 安装：IDEA、Maven、MySQL、（任意数据库可视化工具）、Mybatis
2. 创建Maven工程
- 创建项目命名为SSM；
- 创建模块名为：MyBatis_HelloWorld
3. 打包方式设置为jar(这个操作须在创建完项目后进入pom.xml文件中进行设置，代码如下：`<packaging>jar</packaging>`)
4. 引入依赖（将这里的内容拷贝到pom.xml文件下；具体的功能见其中的注释）

```xml
<dependencies>
 <dependency>
     <!-- Mybatis核心 -->
  <groupId>org.mybatis</groupId>
  <artifactId>mybatis</artifactId>
  <version>3.5.7</version>
 </dependency>
 <!-- junit测试 -->
 <dependency>
  <groupId>junit</groupId>
  <artifactId>junit</artifactId>
  <version>4.12</version>
  <scope>test</scope>
 </dependency>
 <!-- MySQL驱动 -->
 <dependency>
  <groupId>mysql</groupId>
  <artifactId>mysql-connector-java</artifactId>
  <version>8.0.16</version>
        <!--这个版本对应数据库的版本，并最终影响数据库的连接驱动-->
  </dependency>
</dependencies>
```

#### 创建数据库

打开数据库可视化工具，创建数据库“SSM”、创建表“t_user”。并打开编辑器，粘贴如下的内容：

```sql
CREATE TABLE `t_user` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `username` varchar(20) DEFAULT NULL,
  `password` varchar(20) DEFAULT NULL,
  `age` int(11) DEFAULT NULL,
  `gender` char(1) DEFAULT NULL,
  `emall` varchar(50) DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8
```

#### 创建实体类

1. 将实体类创建到模块路径、src/main/java下，起名为：`com.tl.mybatis.pojo.User`（这样起名可同时将包名一并建出）
2. 创建实体类属性并提供构造器、Getter与Setter、toString方法

```java
private Integer id;
private String username;
private String password;
private Integer age;
private String gender;
private String email;

 public User() {
 }

 public User(Integer id, String username, String password, Integer age, String gender, String email) {
        this.id = id;
        this.username = username;
        this.password = password;
        this.age = age;
        this.gender = gender;
        this.email = email;
 }

 public Integer getId() {
        return id;
 }

 public void setId(Integer id) {
        this.id = id;
 }

 public String getUsername() {
        return username;
 }

 public void setUsername(String username) {
        this.username = username;
 }

 public String getPassword() {
        return password;
 }

 public void setPassword(String password) {
        this.password = password;
 }

 public Integer getAge() {
        return age;
 }

 public void setAge(Integer age) {
        this.age = age;
 }

 public String getGender() {
        return gender;
 }

 public void setGender(String gender) {
        this.gender = gender;
 }

 public String getEmail() {
        return email;
 }

 public void setEmail(String email) {
        this.email = email;
 }
```

#### Mybatis的核心配置文件

- 取名可以任意但通常习惯命名为[mybatis-config.xml]；当整合spring后这个配置文件可以省略，所以在当前章节可以直接复制，粘贴。
- 核心配置文件主要作用是配置连接数据库的环境以及MyBatis的全局配置信息
- 核心配置文件存放的位置是src\main\resources目录下
- 核心配置文件中的标签必须按照固定的顺序(**有的标签可以不写，但顺序一定不能乱**)：`properties`、`settings`、`typeAliases`、`typeHandlers`、`objectFactory`、`objectWrapperFactory`、`reflectorFactory`、`plugins`、`environments`、`databaseIdProvider`、`mappers`
1. 右键src/main/resources文件夹，选择“new→file”，在弹出的菜单中输入`mybatis-config.xml`，按回车
2. 粘贴如下的内容

```xml
    <?xml version="1.0" encoding="UTF-8" ?>
    <!DOCTYPE configuration
            PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
            "http://mybatis.org/dtd/mybatis-3-config.dtd">
    <configuration>
        <properties resource="jdbc.properties" />
            <setting name="mapUnderscoreToCamelCase" value="true"/>
        <typeAliases>
     <!-- 这里写的是对应于某实体bean -->
            <package name="xx.xxx.xxx.pojo"/>
        </typeAliases>
        <environments default="development">
            <environment id="development">
                <transactionManager type="JDBC"/>
                <dataSource type="POOLED">
                    <property name="driver" value="${jdbc.driver}"/>
                    <property name="url" value="${jdbc.url}"/>
                    <property name="username" value="${jdbc.username}"/>
                    <property name="password" value="${jdbc.password}"/>
                </dataSource>
            </environment>
        </environments>
        <mappers>
     <!-- 这里对应的是某mapper映射文件 -->
            <package name="xx.xxx.xxx.mapper"/>
        </mappers>
    </configuration>
```

核心配置文件详解

1. `<environments>`：设置多个连接数据库的环境
   属性：`default`（设置默认使用的环境的id）

2. `<typeAliases>`标签
   `typeAlias`：设置某个具体类型的别名
   属性：`type|alias`
   
   - `type`：需要设置别名的类型的全类名
   - `alias`：设置此类型的别名，且该别名不区分大小写。若不设置该属性，则该类型拥有默认的别名，即类名。
     `<typeAlias type="com.tl.mybatis.bean.User"></typeAlias>`：不设置alias属性
     `<typeAlias type="com.seven.mybatis.bean.User" alias="user">`：设置alias属性

3. `<environment>`标签：设置具体的连接数据库的环境信息
   属性：`id`
   
   - id：设置环境的唯一标识，可通过environments标签中的default设置某一个环境的id，表示默认使用的环境

4. `<transactionManager>`标签：设置事务管理方式
   属性：`type = "JDBC|MANAGED"`
   
   - `JDBC`：设置当前环境的事务管理都必须手动处理
   - `MANAGED`：设置事务被处理。例如Spring中的AOP

5. `<properties>`标签：引用配置文件
   
   - 引用：`<properties resource="jdbc.properties"></properties>`
   - 新建jdbc.properties文件
   
   ```properties
    jdbc.driver=com.mysql.cj.jdbc.Driver
    jdbc.url=jdbc:mysql://localhost:3306/ssm?serverTimeZone=UTC
    jdbc.username=root
    jdbc.password=root
   ```

6. `<dataSource>`标签：设置数据源
   属性：`type = "POOLED|UNPOOLED|JNDI"`
   引用：`<dataSource type="POOLED">`
   
   - POOLED：使用数据库连接池，即会将创建的连接进行缓存，下次使用可以从缓存直接获取，不需要重新创建
   - UNPOOLED：不使用数据库连接池，即每次使用连接都需要重新创建
   - JNDI：调用上下文中的数据源
   - `<property>`标签：设置与数据库相关的参数
     - 属性：`name|value`
       name：连接字段；value：对应的参数
   
   ```xml
   <property name="driver" value="${jdbc.driver}"/>
    <property name="url" value="${jdbc.url}"/>
    <property name="username" value="${jdbc.username}"/>
    <property name="password" value="${jdbc.password}"/>
   ```

7. `<mappers>`：引入核心配置文件
   
   - 以具体的xml为单位：`<mapper resource="UserMapper.xml"/>`
   - 以包为单位：`<package name="com.tl.mybatis.mapper"/>`
     注意：此（指以包为单位的方式）方式必须保证①mapper接口和mapper映射文件必须在相同的包下；②mapper接口要和mapper映射文件的名字一致

8. 延迟加载
   
   ```xml
    <settings>
        <setting name="lazyLoadingEnabled" value="true"/>
        <setting name="aggressiveLazyLoading" value="false"/>
    </settings>
   ```
- LazyLoadingEnabled：延迟加载的全局开关。当开启后，所有的关联对象都会延迟加载
- aggressiveLazyLoading：按需加载。当开启时，任何方法的调用都会加载该对象的所有属性。通过`association`和`collection`中的`fetchType`属性设置当前的分步查询是否使用延迟加载
    `fetchType=lazy|eager`（lazy：延迟加载；eager：立即加载）

#### 创建mapper接口

 MyBatis中的mapper接口相当于以前的dao。但是区别在于，mapper仅仅是接口（interface），我们不需要提供实现类（即implements...）。
 在com.tl.mybatis目录下，新建包mapper，并新建UserMapper接口:

```java
public interface UserMapper {

   int insertUser();
}
```

#### 创建映射文件

在resource目录下新建包，名为com.tl.mybatis.mapper，并新建文件，命名为Usermapper.xml，编写如下的内容：

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
  <!-- namespace中是映射接口的全类名 -->
<mapper namespace="com.tl.mybatis.mapper.UserMapper">

<!-- 推荐在写增删改查的操作前，将接口中的方法复制一份到本映射文件 -->
<!-- id为接口中的方法 -->
<!--     int insertUser()-->
    <insert id="insertUser">
        insert into t_user values(null,'admin','123456',23,'男','123@example.com')
    </insert>
</mapper>
```

注意：
①mapper接口的全类名和映射接口的namespace一致；
②mapper接口中的方法的方法名要和映射文件中的sql的id保持一致

#### 编写测试类（插入用户信息）

```java
public class MybatisTest {

    @Test  //Junit注解
    public void testInsert() throws IOException {
        //获取核心配置文件的输入流
        InputStream is = Resources.getResourceAsStream("mybatis-config.xml");
        //获取SQLSessionFactoryBuilder对象
        SqlSessionFactoryBuilder sqlSessionFactoryBuilder = new SqlSessionFactoryBuilder();
        //获取SQLSessionFactory对象
        SqlSessionFactory sqlSessionFactory = sqlSessionFactoryBuilder.build(is);
        //获取sql的会话对象SQLSession，是Mybatis提供的操作数据库的对象
       SqlSession sqlSession = sqlSessionFactory.openSession();
        //获取UserMapper的代理实现类对象
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        //调用mapper接口中的方法，实现添加用户信息的功能
        int i = mapper.insertUser();
        System.out.println(i);
        //关闭session
        sqlSession.close();
    }
}
```

*代码测试通过但在数据库中未查询出新添加的数据：获取SQL的会话对象`SqlSession()`不会自动提交事务,是MyBatis提供的操作数据库的对象；将`SqlSession()`的参数设定为true即可完成自动提交事务。否则需要自己手动写`SqlSession.commit()`*

#### 添加log4j日志文件

> Log4j是Apache的一个开源项目，通过使用Log4j，我们可以控制日志信息输送的目的地是控制台、文件、GUI组件，甚至是套接口服务器、NT的事件记录器、UNIX Syslog守护进程等；我们也可以控制每一条日志的输出格式；通过定义每一条日志信息的级别，我们能够更加细致地控制日志的生成过程。最令人感兴趣的就是，这些可以通过一个配置文件来灵活地进行配置，而不需要修改应用的代码。

1. 添加Maven依赖

```xml
  <!-- log4j日志 -->
        <dependency>
            <groupId>log4j</groupId>
            <artifactId>log4j</artifactId>
            <version>1.2.17</version>
        </dependency>
    </dependencies>
```

2. 在resource目录下新建log4j.xml文件，并粘贴如下内容

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE log4j:configuration SYSTEM "log4j.dtd">
<log4j:configuration xmlns:log4j="http://jakarta.apache.org/log4j/">
    <appender name="STDOUT" class="org.apache.log4j.ConsoleAppender">
        <param name="Encoding" value="UTF-8" />
        <layout class="org.apache.log4j.PatternLayout">
            <param name="ConversionPattern" value="%-5p %d{MM-dd HH:mm:ss,SSS} %m (%F:%L) \n" />
        </layout>
    </appender>
    <logger name="java.sql">
        <level value="debug" />
    </logger>
    <logger name="org.apache.ibatis">
        <level value="info" />
    </logger>
    <root>
        <level value="debug" />
        <appender-ref ref="STDOUT" />
    </root>
</log4j:configuration>
```

#### 将有关SqlSession的内容提取为一个工具类（Util）

在com.tl.mybatis下新建包utils，并新建类SqlSessionUtil，编写如下的内容：

```java
package com.tl.mybatis.utils;

import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;

import java.io.IOException;
import java.io.InputStream;

public class SqlsessionUtil {
    public static SqlSession getSqlSession(){

        SqlSession sqlSession = null;

        try {
            //获取核心配置文件的输入流
            InputStream is = Resources.getResourceAsStream("mybatis-config.xml");
            //获取SqlSessionFactoryBuilder
            SqlSessionFactoryBuilder sqlSessionFactoryBuilder = new SqlSessionFactoryBuilder();
            //获取SqlSessionFactory
            SqlSessionFactory sqlSessionFactory = sqlSessionFactoryBuilder.build(is);
            //获取SqlSession对象
            sqlSession = sqlSessionFactory.openSession(true);
        } catch (IOException e) {
            throw new RuntimeException(e);
        }
        return sqlSession;
    }
}
```

#### 修改用户信息

1. 添加mapper接口
   
   ```java
    void updateUser();
   ```

2. 添加映射
   
   ```xml
   <!--    void updateUser()-->
    <update id="updateUser">
        update t_user set username='root',password='123' where id = 3
    </update>
   ```

3. 编写测试类
   
   ```java
   @Test
    public void testUpdate(){
        SqlSession sqlSession = SqlsessionUtil.getSqlSession();
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        mapper.updateUser();
        sqlSession.close();
    }
   ```

#### 删除用户信息

1. 添加mapper接口
   
   ```java
    void deleteUser();
   ```

2. 添加映射
   
   ```xml
   <!--    void deleteUser()-->
    <delete id="deleteUser">
        delete from t_user where id = 3
    </delete>
   ```

3. 编写测试类

```java
    @Test
    public void testDelete(){

            SqlSession sqlSession = SqlsessionUtil.getSqlSession();
            UserMapper mapper = sqlSession.getMapper(UserMapper.class);
            mapper.deleteUser();
            sqlSession.close();

    }
```

#### 查询一条员工信息（根据员工ID）

1. 添加mapper接口
   
   ```java
   User getUserById();
   ```

2. 添加映射
   
   ```xml
    <select id="getUserById" resultType="user">
        select * from t_user where id = 1
    </select>
   ```
   
   resultType：设置结果类型，即查询的数据要转换为的Java类型
   resultMap：自定义映射，处理多对一或一对多的映射关系

3. 编写测试类

```java
    @Test
    public void testGetUserById(){
        SqlSession sqlSession = SqlsessionUtil.getSqlSession();
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        User user = mapper.getUserById();
        System.out.println(user);
        sqlSession.close();
    }
```

#### 查询所有员工信息

1. 添加mapper接口
   
   ```java
   List<User> getAllUser();
   ```

2. 添加映射
   
   ```xml
   <!--   List<User> getAllUser()-->
    <select id="getAllUser" resultType="User">
        select * from t_user
   
   </select>
   ```

3. 编写测试类

```java
 @Test
    public void testGetAllUser(){
        SqlSession sqlSession = SqlsessionUtil.getSqlSession();
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        List<User> list = mapper.getAllUser();
        list.forEach(System.out::println);
        sqlSession.close();
    }
```

#### 利用IDEA的文件模板工具，快速生成框架

![文件和代码模板](2022-11-12-23-44-14.png)

### mybatis获取参数值的方式

- `#{}`获取：#{}的本质就是占位符赋值 （自动加单引号）
- `${}`获取：${}的本质就是字符串拼接（需要手动添加单引号）
1. 若mapper接口方法的参数为多个字面量类型时，此时mybatis会将参数放到map集合中，以两种方式进行存储：
   - arg1,arg2...为键，以参数为值
   - param1,param2...为键，以参数为值
     **故通过`#{}`、`${}`访问该map集合的键，就可以获得相对应的值**
2. 若mapper接口方法的参数为map集合类型的参数
   - 通过`#{}`、`${}`访问该map集合的键，就可以获得相对应的值
3. 若mapper接口方法的参数为实体类类型的参数
   - 通过`#{}`、`${}`访问实体类中的属性名，就可以获得相对应的属性值
4. 在mapper接口方法的参数上设置`@param`注解
   - 以`@param`注解的value属性值为键，以参数为值。
   - 以param1，param2...为键，以参数为值。

#### mybatis的查询功能

1. 根据ID获取User对象
   
   - 添加mapper接口
     
     ```java
     User getUserById(@Param("id") Integer id);
     ```
   
   - 添加映射
     
     ```xml
      <!--    User  getUserById(@Param("id") Integer id); -->
        <select id="getUserById" resultType="User">
            select * from t_user where id = #{id}
        </select>
     ```
   
   - 编写测试类
     
     ```java
     @Test
     public void testGetUserById(){
        SqlSession sqlSession = SqlsessionUtil.getSqlSession();
        SelectMapper mapper = sqlSession.getMapper(SelectMapper.class);
        User user = mapper.getUserById(1);
        System.out.println(user);
     }
     ```

2. 查询所有t_user表的数据
   
   - 添加mapper接口
     
     ```java
        User getAllUser();
     ```
     
     注意：
     <b>这么写是错误的：如果用实体类对象接收参数则会报错，信息为`org.apache.ibatis.exceptions.TooManyResultsException`:
     Expected one result (or null)to be returned by selectOne(), but found: 5
     （期望返回一个结果但返回了5条数据）</b>
     <font color="red">故此接口应该使用List集合接收</font>
   
   - 添加mapper接口
     
     ```java
        List<User> getAllUser();
     ```
   
   - 添加映射
     
     ```xml
        <!--    List<User> getAllUser();   -->
        <select id="getAllUser" resultType="User">
            select * from t_user
        </select>
     ```

3. 利用map集合获取数据
   以字段名为键，以字段的值为值。若某一字段值为null，则不会放入map
   
   - 添加mapper接口
     
     ```java
        Map<String,Object> getAllUserByMap(@Param("id") Integer id);
     ```
   
   - 添加映射
     
     ```xml
     <!--    List<User> getAllUser();   -->
     <select id="getAllUser" resultType="User">
        select * from t_user where id =#{id}
     </select>
     ```

4. 利用map集合获取全部数据
   若查询的数据有多条，且要将每条数据转换类map集合，有两种解决方案
- 将mapper接口方法的返回值设定为泛型是map的list集合
  `List<Map<String, Object>> list = mapper.getAllUserToMap();`

- 可将每条数据转换的map集合放在一个大map中，但是必须要通过`@MapKey`注解，将查询到的某个字段的值作为大的map的键
  
  ```java
  @MapKey("id")
  Map<String, Object> getAllUserToMap()
  ```
  
  - 添加mapper接口
    
    ```java
    @MapKey("id")
    Map<String, Object> getAllUserToMap()
    ```
  
  - 添加映射
    
    ```xml
    <!--   Map<String,Object> getAllUserToMap() -->
    <select id="getAllUserToMap" resultType="map">
        select * from t_user
    </select>
    ```

#### 特殊SQL的执行

1. 模糊查询
   
   - 利用字符串拼接模糊查询，相当于“`+`”
        `select * from t_user where username like '%${mohu}%'`
        注意：这种写法是错误的——`select * from t_user where username like '%#{mohu}%'`
        原因：`#{}`会自动在两边自动加上单引号，会导致`select * from t_user where username like '%?%'`（即无法解析模糊查询符"%"及通配符"?"）
     
     - 添加mapper接口
       
       ```java
           List<User> testMohu(@Param("mohu") String mohu);
       ```
     
     - 添加映射
       
       ```xml
       <select id="getUserByLike" resultType="User">
           select * from t_user where username like '%${mohu}%'
       </select>
       ```
   
   - 利用`concat`函数进行字符串拼接，比较繁琐，不推荐使用
     
     - 添加mapper接口
       
       ```java
           List<User> testMohu(@Param("mohu") String mohu);
       ```
     
     - 添加映射
       
       ```xml
       <select id="getUserByLike" resultType="User">
           select * from t_user where username like concat('%',#{mohu},'%')
       </select>
       ```
   
   - 推荐使用如下的方式
     
     - 添加mapper接口
       
       ```java
           List<User> testMohu(@Param("mohu") String mohu);
       ```
     
     - 添加映射
       
       ```xml
       <select id="getUserByLike" resultType="User">
          select * from t_user where username like "%"#{mohu}"%" <!--此处IDEA会爆红，但不影响最终查询-->
       </select>
       ```
       
       - 编写测试类
       
       ```java
           @Test
       public void testGetUserByLike(){
           SqlSession sqlSession = SqlsessionUtil.getSqlSession();
           SpecialSQLMapper mapper = sqlSession.getMapper(SpecialSQLMapper.class);
           List<User> list = mapper.getUserByLike("c"); //括号内写查询的模糊条件
           list.forEach(System.out::println);
           }
       ```

2. 批量删除
   
   - 添加mapper接口
     
     ```java
        int deleteMore(@Param("ids") String ids);
     ```
   
   - 添加映射
     
     ```xml
     <delete id="deleteMore">
        <!-- 只能使用${} 用#{}会报错 以后可用foreach 解决 -->
        delete from t_user where id in (${ids})
     </delete>
     ```

3. 动态设置表名
   
   - 添加mapper接口
     
     ```java
        List<User> getAllUser(@Param("tableName") String tableName);
     ```
   
   - 添加映射
     
     ```xml
        <!-- 依然是#{}和${}的问题 -->
        <select id="getAllUser" resultType="User">
            select * from ${tableName}
        </select>
     ```

4. 动态设置表名
   
   - 添加mapper接口
     
     ```java
        List<User> getAllUser(@Param("tableName") String tableName);
     ```
   
   - 添加映射
     
     ```xml
        <!-- 依然是#{}和${}的问题 -->
        <select id="getAllUser" resultType="User">
            select * from ${tableName}
        </select>
     ```

5. 获取自增主键（测试添加用户）
   
   - 添加mapper接口
     
     ```java
       int insertUser(User user);
     ```
   
   - 添加映射
     需要使用`useGeneratedKeys`、`keyProperty`属性
     `useGeneratedKeys`：设置使用自增的主键
     `keyProperty`：将添加的数据的自增主键为实体类类型的参数的属性赋值
     
     ```xml
         <insert id="insertUser" useGeneratedKeys="true" keyProperty="id">
            insert into t_user values (null,#{username},#{password},#{age},#{gender},#{email})
        </insert>
     ```

### 自定义映射：resultMap

*若字段名和实体类中的属性名不一致，则可以通过resultMap设置自定义映射*

1. 属性：id|type
   - id：表示自定义映射的唯一标识
   - type：查询的数据要映射的实体类的类型
2. 子标签
   - id：设置主键的映射关系
   - result：设置普通字段的映射关系
   - association：设置多对一的映射关系（处理实体类类型的属性）
   - collection：设置一对多的映射关系
3. 子标签中的属性
   - property：设置映射关系中实体类中的属性名
   - column：设置映射关系中表中的字段名

#### 字段名和实体类中的属性名不一致

1. 查询时可使用别名

2. 开启下划线（字段名的设置规则）转小驼峰（属性名的设置规则）的配置，在`mybatis-config.xml`添加如下的内容
   
   ```xml
    <settings>
    <!-- 下划线 自动映射 驼峰 -->
    <setting name="mapUnderscoreToCamelCase" value="true"/>
    </settings>
   ```

3. 使用`resultMap`。注意`resultMap`和`resultType`是二选一的
   
   ```xml
    <resultMap id="empResultMap" type="Emp">
        <id column="emp_id" property="empId"/>
        <result column="emp_name" property="empName"/>
        <result column="age" property="age"/>
        <result column="gender" property="gender"/>
    </resultMap>
    <!-- Emp getEmpByEmpId(@Param("empId") Integer empId); -->
    <select id="getEmpByEmpId" resultMap="empResultMap">
        select *
        from t_emp
        where emp_id = #{empId}
    </select>
   ```

#### 多对一关系

1. 使用级联，即一次性连接出所有字段
   
   ```java
    Emp getEmpAndDeptByEmpId(@Param("empId") Integer empId);
   ```
   
   ```xml
    <resultMap id="getEmpAndDeptByEmpId" type="Emp">
        <id column="emp_id" property="empId" />
        <result column="emp_name" property="empName" />
        <!-- 级联方式：多对一的映射关系 -->
        <result column="dept_id" property="dept.deptId" />
        <result column="dept_name" property="dept.deptName" />
    </resultMap>
    <select id="getEmpAndDeptByEmpId" resultMap="getEmpAndDeptByEmpId">
        SELECT *
        FROM t_emp
        LEFT JOIN t_dept ON t_emp.dept_id = t_dept.dept_id
        WHERE emp_id = #{empId};
    </select>
   ```

2. 使用`association`标签
   
   ```xml
    <resultMap id="getEmpAndDeptByEmpId" type="Emp">
        <id column="emp_id" property="empId" />
        <result column="emp_name" property="empName" />
            <association property="dept" javaType="Dept">
                <id column="dept_id" property="deptId" />
                <result column="dept_name" property="deptName" />
            </association>
    </resultMap>
    <select id="getEmpAndDeptByEmpId" resultMap="getEmpAndDeptByEmpId">
        SELECT *
        FROM t_emp
        LEFT JOIN t_dept ON t_emp.dept_id = t_dept.dept_id
        WHERE emp_id = #{empId};
    </select>
   ```

3. 使用分步查询，先查询出一张表的信息，再查询出另一张表的信息
   优点：可以延迟加载，但必须配置该机制
- 编写需要查询的接口：

```java
    // 分步查询第一步
    Emp getEmpAndDeptByStepOne(@Param("empId") Integer empId);
```

```java
    // 分步查询第二步
    Dept getEmpAndDeptByStepTwo(@Param("deptId") Integer deptId);
```

- 创建映射文件：EmpMapper.xml

```xml
    <resultMap id="empAndDeptByStepResultMap" type="Emp">
        <id column="emp_id" property="empId"/>
        <result column="emp_name" property="empName"/>
        <result column="age" property="age"/>
        <result column="gender" property="gender"/>
        <association property="dept" fetchType="eager"
                     select="com.tl.mybatis.mapper.DeptMapper.getEmpAndDeptByStepTwo"
                     column="dept_id"/>
        <!-- association属性：
            property：设置需要处理映射关系的属性的属性名
            fetchType：在开启了延迟加载的环境后，通过该属性设置当前的分步查询是否使用延迟加载
                eager(立即加载) | lazy(延迟加载)
            select：设置分步查询的sql的唯一标识
            column：将查询出的某个字段作为分步查询的sql的条件
        -->
    </resultMap>
    <!--    Emp getEmpAndDeptByStepOne(@Param("empId") Integer empId)-->
    <select id="getEmpAndDeptByStepOne" resultMap="empAndDeptByStepResultMap">
        select *
        from t_emp
        where emp_id = #{empId}
    </select>
```

- 创建映射文件：DeptMapper.xml

```xml
    <select id="getEmpAndDeptByStepTwo" resultType="Dept">
        select * from t_dept where dept_id = #{deptId}
    </select>
```

- 编写测试类

```java
        @Test
        public void testGetEmpAndDeptByStep(){
        SqlSession sqlSession = SqlsessionUtil.getSqlSession();
        EmpMapper mapper = sqlSession.getMapper(EmpMapper.class);
        Emp emp = mapper.getEmpAndDeptByStepOne(2);
        System.out.println(emp.getEmpName());
        }
```

#### 一对多关系

1. 使用级联 + collection
- 编写需要查询的接口

```java
    Dept getDeptAndEmpsByDeptId(@Param("deptId") Integer deptId);
```

- 添加映射文件

```xml
<resultMap id="getDeptAndEmpsByDeptIdResultMap" type="dept">
    <id column="dept_id" property="deptId"></id>
    <result column="dept_name" property="deptName"></result>
    <!--
        property: 关联的属性.
        ofType: 集合内部元素的类型.
     -->
    <collection property="emps" ofType="emp">
        <id column="emp_id" property="empId"></id>
        <result column="emp_name" property="empName"></result>
    </collection>
</resultMap>
```

```xml
<!-- Dept getDeptAndEmpsByDeptId(@Param("deptId") Integer deptId); -->
<select id="getDeptAndEmpsByDeptId" resultMap="getDeptAndEmpsByDeptIdResultMap">
    SELECT *
    FROM t_dept
    LEFT JOIN t_emp
    ON t_dept.dept_id = t_emp.dept_id
    WHERE t_dept.dept_id = #{deptId};
</select>
```

2. 使用分步查询：先查询部门，再根据部门的id查询该部门下的员工信息
- 编写要查询的接口
  
  - DeptMapper.java
    
    ```java
    //分步查询第一步：查询部门信息
    Dept getDeptAndEmpdsStepOne(@Param("deptId") Integer deptId);
    ```
  
  - EmpMapper.java
    
    ```java
    //分步查询第二步：查询该部门下的员工
    Emp getDeptAndEmpdsStepOne(@Param("deptId") Integer empId);
    ```
  
  - 添加映射文件
    
    - DeptMapper.xml
    
    ```xml
    <resultMap id="deptAndEmpResultMap" type="Dept">
        <id column="dept_id" property="deptId"/>
        <result column="dept_name" property="deptName"/>
        <collection property="emps" ofType="Emp">
        <!-- ofType：设置集合类型的属性中存储的数据的类型-->
        <id column="emp_id" property="empId"/>
        <result column="emp_name" property="empName"/>
        <result column="age" property="age"/>
        <result column="gender" property="gender"/>
        </collection>
    </resultMap>
    
    <select id="getDeptAndEmpByStepOne" resultMap="deptAndEmpResultMapByStep">
        select * from t_dept where dept_id = #{deptId}
    </select>
    ```
    
    - EmpMapper.xml
    
    ```xml
    <select id="getDeptAndEmpdsStepTwo" resultType="emp">
        SELECT *
        FROM t_emp
        WHERE emp_id = #{empId};
    </select>
    ```

### 动态SQL

> 根据传入的参数动态的决定最后执行的SQL语句

1. `if`标签：可通过属性`test`进行表达式的判断。若表达式结果为true，则执行标签中的内容，否则不执行
   
   ```xml
   <!--List<Emp> getEmpListByCondition(Emp emp);-->
    <select id="getEmpListByMoreTJ" resultType="Emp">
        <!-- 1=1是因为如果下方条件都不满足的情况下where会报错-->
        select * from t_emp where 1=1
        <if test="ename != '' and ename != null"> and ename = #{ename} </if>
        <if test="age != '' and age != null">  and age = #{age} </if>
        <if test="sex != '' and sex != null"> and sex = #{sex}  </if>
    </select>
   ```

2. `where`标签：
   
   - 若`where`标签中的if条件都不满足，则`where`标签没有任何功能，即不会在查询语句中添加`where`关键字
   
   - 若`where`标签中的if条件满足，则`where`标签会自动添加`where`关键字，并将条件中最前方多余的“and”去掉
     **注意：`where`标签不能去掉条件最后多余的and**
     
     ```xml
     <select id="getEmpByConditionTwo" resultType="Emp">
        select * from t_emp
        <where>
            <if test="empName != null and empName != ''">
                emp_name = #{empName}
            </if>
            <if test="age != null and age != ''">
                <!--即使上面的条件不成立前面的and也会自动消除-->
                and age = #{age}
            </if>
            <if test="gender != null and gender != ''">
                and gender = #{gender}
            </if>
        </where>
     </select>
     ```

3. `trim`标签
   
   - `prefix`、`suffix`属性：在标签中内容前面或后面添加指定内容
   
   - `prefixOverrides`、`suffixOverrides`：在标签中内容前面或后面去掉指定内容
     
     ```xmlTT
     <select id="getEmpByCondition" resultType="Emp">
        select * from t_emp
        <!-- prefix：在内容的前面添加 where 。  suffixOverrides：在内容的后面去掉 and -->
        <trim prefix="where" suffixOverrides="and">
            <if test="empName != null and empName != ''">
                emp_name = #{empName} and
            </if>
            <if test="age != null and age != ''">
                age = #{age} and
            </if>
            <if test="gender != null and gender != ''">
                gender = #{gender}
            </if>
        </trim>
     </select>
     ```

4. `choose`、`when`、`otherwise` 标签：相当于java中的`if...else if...else`语句块；<font color="red">`when`至少设置一个，`otherwise`最多设置一个</font>
   
   ```xml
   <select id="getEmpByChoose" resultType="Emp">
        select * from t_emp
        <where>
            <choose>
                <when test="empName != null and empName != ''">
                    emp_name = #{empName}
                </when>
                <when test="age != null and age != ''">
                    age = #{age}
                </when>
                <when test="gender != null and gender != ''">
                    gender = #{gender}
                </when>
            </choose>
        </where>
    </select>
   ```

5. `foreach`
   
   - 属性
     `collection`：设置要循环的数组或集合
     `item`：用一个字符串表示数组或集合中的每一个数据
     `separator`：设置每次循环的数据之间的分隔符
     `open`：循环的所有内容以什么开始
     `close`：循环的所有内容以什么结束
     
     - 循环添加
     
     ```xml
     <insert id="insertMoreEmp">
        insert into t_emp values
        <foreach collection="emps" item="emp" separator=",">
            (null,#{emp.empName},#{emp.age},#{emp.gender},null)
        </foreach>
     </insert>
     ```
     
     - 循环删除
       两种删除方式：利用mysql的in函数进行批量删除；利用`where`和`or`进行批量删除
     
     ```xml
        <delete id="deleteMoreEmp">
            <!--
        delete from t_emp where emp_id in
        <foreach collection="empIds" item="empId" separator="," open="(" close=")">
            #{empId}
        </foreach>
        -->
            delete from t_emp where
        <foreach collection="empIds" item="empId" separator="or">
            emp_id = #{empId}
        </foreach>
     </delete>
     ```

6. SQL标签：可以记录一段sql，在需要用的地方使用include标签进行引用
   
   ```xml
        <sql id="empColumns">
            emp_id,emp_name,age,gender,dept_id
        </sql>
   
        <!--   用来引用sql 标签中的字段     -->
        <include refid="empColumns"></include>
   
        <select id="getEmpByCondition" resultType="Emp">
        select <include refid="empColumns"></include> from t_emp
        <trim prefix="where" suffixOverrides="and">
            <if test="empName != null and empName != ''">
                emp_name = #{empName} and
            </if>
            <if test="age != null and age != ''">
                age = #{age} and
            </if>
            <if test="gender != null and gender != ''">
                gender = #{gender}
            </if>
        </trim>
    </select>
   ```

### Mybatis的缓存

#### Mybatis的一级缓存

一级缓存是SQLSession级别的，通过同一个SQLSession查询的数据会被缓存，下次查询相同的数据，就会从缓存中直接获取，不会从数据库重新访问。
使一级缓存失效的四种情况：

- 不同的SqlSession对应不同的一级缓存
- 同一个SqlSession但是查询条件不同
- 同一个SqlSession两次查询期间执行了任何一次增删改操作
- 同一个SqlSession两次查询期间手动清空了缓存

#### MyBatis的二级缓存

二级缓存是SqlSessionFactory级别，通过同一个SqlSessionFactory创建的SqlSession查询的结果会被缓存；此后若再次执行相同的查询语句，结果就会从缓存中获取
二级缓存开启的条件：

- 在核心配置文件中，设置全局配置属性`cacheEnabled="true"`，默认为`true`，不需要设置
- 在映射文件中设置标签`<cache/>`
- 二级缓存必须在SqlSession关闭或提交之后有效
- 查询的数据所转换的实体类类型必须实现序列化的接口
  使二级缓存失效的情况：两次查询之间执行了任意的增删改，会使一级和二级缓存同时失效
  二级缓存的配置（了解）
  在 mapper 配置文件中添加的 cache 标签可以设置一些属性：
1. eviction属性：缓存回收策略，默认的是 LRU。
   LRU（Least Recently） - 最近最少使用的：移除最长时间不被使用的对象。
   FIFO（First in First out） - 先进先出：按对象进入缓存的顺序来移除它们。
   SOFT - 软引用：移除基于垃圾回收器状态和软引用规则的对象。
   WEAK - 弱引用：更积极地移除基于垃圾收集器状态和弱引用规则的对象。
2. flushInterval属性：刷新间隔，单位毫秒
   默认情况是不设置，也就是没有刷新间隔，缓存仅仅调用语句时刷新
3. size属性：引用数目，正整数。
   代表缓存最多可以存储多少个对象，太大容易导致内存溢出
4. readOnly属性：只读，true/false
   true：只读缓存，会给所有调用者返回缓存对象的相同实例。因此这些对象不能被修改。者提供了很重要的性能优势
   false（默认）：读写缓存；会返回缓存对象的拷贝（通过序列化）。这会慢一些，但是安全

#### Mybatis缓存查询的顺序

先查询二级缓存，因为二级缓存中可能会有其他程序已经查出来的数据，可以拿来直接使用。如果二级缓存没有命中，再查询一级缓存。如果一级缓存也没有命中，则查询数据库。SqlSession 关闭之后，一级缓存中的数据会写入二级缓存。

#### 整合第三方缓存EHCache

1. 添加依赖
   
   ```xml
   <!-- Mybatis EHCache整合包 -->
    <dependency>
    <groupId>org.mybatis.caches</groupId>
    <artifactId>mybatis-ehcache</artifactId>
    <version>1.2.1</version> </dependency>
    <!-- slf4j日志门面的一个具体实现 -->
    <dependency>
    <groupId>ch.qos.logback</groupId>
    <artifactId>logback-classic</artifactId>
    <version>1.2.3</version>
    </dependency>
   ```

2. 各个jar包的功能
   
   | jar包名称          | 作用                  |
   | --------------- | ------------------- |
   | mybatis-echache | Mybatis和EHCache的整合包 |
   | ehcache         | EHCache核心包          |
   | slf4j-api       | SLF4J日志门面包          |
   | logback-classic | 支持SLF4j门面接口的一个具体实现  |

3. 创建EHCache的配置文件`ehcache.xml`
   
   ```xml
   <?xml version="1.0" encoding="utf-8" ?>
    <ehcache xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="../config/ehcache.xsd">
    <!-- 磁盘保存路径 -->
    <diskStore path="D:\atguigu\ehcache"/>
        <defaultCache maxElementsInMemory="1000" maxElementsOnDisk="10000000"  eternal="false" overflowToDisk="true" timeToIdleSeconds="120"     timeToLiveSeconds="120" diskExpiryThreadIntervalSeconds="120"   memoryStoreEvictionPolicy="LRU">
        </defaultCache>
    </ehcache>
   ```

4. 设置二级缓存的类型
   `<cache type="org.mybatis.caches.ehcache.EhcacheCache"/>`

5. 加入logback日志
   
   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
    <configuration debug="true">
    <!--指定日志输出的位置-->
    <appender name = "STDOUT" class="ch.qos.logback.core.ConsoleAppender">
        <encoder>
            <!--日志输出的格式-->
            <!--按照顺序：时间、日志级别、线程名称、打印日志的类、日志主体内容、换行-->
            <pattern>[%d{HH:mm:ss.SSS}] [%-Slevel] [%thread] [%logger] [%msg]%n</pattern>
        </encoder>
    </appender>
    <!--设置全局日志级别。日志级别按照顺序分别是：DEBUG、INFO、WARN、ERROR-->
    <!--指定任何一个日志级别都只打印当前级别和后面级别的日志-->
    <root level = "DEBUG">
        <!--指定打印日志的appender。这里通过“STDOUT”引用了前面配置的appender-->
        <appender-ref ref="STDOUT" />
    </root>
    <!--根据特殊需求指定局部日志级别-->
    <looger name="com.tl.mybatis.mapper" lever="DEBUG"/>
   </configuration>
   ```

6. EHCache配置文件说明
   
   | 属性名                             | 是否必填 | 作用                                                                                           |
   |:------------------------------- | ---- | -------------------------------------------------------------------------------------------- |
   | maxElementsInMemory             | 是    | 在内存中缓存的element的最大数目                                                                          |
   | maxElementsOnDisk               | 是    | 在磁盘上缓存的element的最大数目，若是0表示无穷大                                                                 |
   | eternal                         | 是    | 设定缓存的elements是否永远不过期。如果为true，则缓存的数据始终有效；如果为false，那么还要根据timeToIdIeSeconds、timeToLiveSeconds判断 |
   | overflowToDisk                  | 是    | 设定当内存缓存溢出的时候是否将过期的element缓存到磁盘上                                                              |
   | timeToIdIeSeconds               | 否    | 当缓存在EhCache中的数据前后两次访问的时间超过timeToIdIeSeconds的属性取值时，这些数据便会删除，默认值是0，也就是可闲置时间无穷大                 |
   | timeToLiveSeconds               | 否    | 缓存element的有效生命期，默认是0，也就是element存活时间无限大                                                       |
   | diskSpoolBufferSizeMB           | 否    | DiskStore（磁盘缓存）的缓存区大小。默认是30MB。每个Cache都应该有自己的一个缓冲区                                            |
   | diskPersistent                  | 否    | 在VM重启的时候是否启用磁盘保存EHCache中的数据，默认是false                                                         |
   | diskExpiryThreadIntervalSeconds | 否    | 磁盘缓存的清理线程运行间隔，默认是120秒。每个120s，相应的线程会进行一次EhCache中数据的清理工作                                       |
   | memoryStoreEvictionPolicy       | 否    | 当内存缓存达到最大，有新的element加入的时候，移除缓存中element的策略。默认是LRU（最近最少使用），可选的有LFU（最不常使用）和FIFO（先进先出）           |

### Mybatis的逆向工程

正向工程：先创建 Java 实体类，由框架负责根据实体类生成数据库表。 Hibernate 是支持正向工程的
逆向工程：先创建数据库表，由框架负责根据数据库表，反向生成如下资源：Java实体类、Mapper接口、Mapper映射文件

#### 创建逆向工程的步骤

1. 添加依赖和插件
   
   ```xml
    <!-- 依赖MyBatis核心包 -->
    <dependencies>
        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis</artifactId>
            <version>3.5.7</version>
        </dependency>
        <!-- junit测试 -->
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
            <scope>test</scope>
        </dependency>
   
        <!-- log4j日志 -->
        <dependency>
            <groupId>log4j</groupId>
            <artifactId>log4j</artifactId>
            <version>1.2.17</version>
        </dependency>
   
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>8.0.16</version>
        </dependency>
        <dependency>
            <groupId>com.github.pagehelper</groupId>
            <artifactId>pagehelper</artifactId>
            <version>5.2.0</version>
        </dependency>
    </dependencies>
   
    <!-- 控制Maven在构建过程中相关配置 -->
    <build>
        <!-- 构建过程中用到的插件 -->
        <plugins>
            <!-- 具体插件，逆向工程的操作是以构建过程中插件形式出现的 -->
            <plugin>
                <groupId>org.mybatis.generator</groupId>
                <artifactId>mybatis-generator-maven-plugin</artifactId>
                <version>1.3.0</version>
                <!-- 插件的依赖 -->
                <dependencies>
                    <!-- 逆向工程的核心依赖 -->
                    <dependency>
                        <groupId>org.mybatis.generator</groupId>
                        <artifactId>mybatis-generator-core</artifactId>
                        <version>1.3.2</version>
                    </dependency>
                    <!-- MySQL驱动 -->
                    <dependency>
                        <groupId>mysql</groupId>
                        <artifactId>mysql-connector-java</artifactId>
                        <version>8.0.16</version>
                    </dependency>
                </dependencies>
            </plugin>
        </plugins>
    </build>
   ```

2. 创建Mybatis的核心配置文件
   
   ```xml
   <?xml version="1.0" encoding="UTF-8" ?>
    <!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
    <configuration>
    <properties resource="jdbc.properties"/>
    <settings>
        <!--      将下划线映射为驼峰  -->
        <setting name="mapUnderscoreToCamelCase" value="true"/>
    </settings>
   
    <typeAliases>
        <package name="com.tl.mybatis.pojo"/>
    </typeAliases>
    <environments default="development">
        <environment id="development">
            <transactionManager type="JDBC"/>
   
            <dataSource type="POOLED">
                <property name="driver" value="${jdbc.driver}"/>
                <property name="url" value="${jdbc.url}"/>
                <property name="username" value="${jdbc.username}"/>
                <property name="password" value="${jdbc.password}"/>
            </dataSource>
        </environment>
    </environments>
   
    <mappers>
   
        <package name="com.tl.mybatis.mapper"/>
    </mappers>
    </configuration>
   ```

3. 创建逆向工程的配置文件，文件名必须是<font color="red">generatorConfig.xml</font>
   
   ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <!DOCTYPE generatorConfiguration
        PUBLIC "-//mybatis.org//DTD MyBatis Generator Configuration 1.0//EN"
        "http://mybatis.org/dtd/mybatis-generator-config_1_0.dtd">
    <generatorConfiguration>
    <!--
            targetRuntime: 执行生成的逆向工程的版本
                    MyBatis3Simple: 生成基本的CRUD（清新简洁版）
                    MyBatis3: 生成带条件的CRUD（奢华尊享版）
     -->
    <context id="DB2Tables" targetRuntime="MyBatis3">
        <!-- 数据库的连接信息 -->
        <jdbcConnection driverClass="com.mysql.cj.jdbc.Driver"
                        connectionURL="jdbc:mysql://localhost:3306/ssm?serverTimezone=UTC"
                        userId="root"
                        password="root">
        </jdbcConnection>
        <!-- javaBean的生成策略-->
        <javaModelGenerator targetPackage="com.tl.mybatis.pojo" targetProject=".\src\main\java">
            <property name="enableSubPackages" value="true" />
            <property name="trimStrings" value="true" />
        </javaModelGenerator>
        <!-- SQL映射文件的生成策略 -->
        <sqlMapGenerator targetPackage="com.tl.mybatis.mapper"  targetProject=".\src\main\resources">
            <property name="enableSubPackages" value="true" />
        </sqlMapGenerator>
        <!-- Mapper接口的生成策略 -->
        <javaClientGenerator type="XMLMAPPER" targetPackage="com.tl.mybatis.mapper"  targetProject=".\src\main\java">
            <property name="enableSubPackages" value="true" />
        </javaClientGenerator>
        <!-- 逆向分析的表 -->
        <!-- tableName设置为*号，可以对应所有表，此时不写domainObjectName -->
        <!-- domainObjectName属性指定生成出来的实体类的类名 -->
        <table tableName="t_emp" domainObjectName="Emp"/>
        <table tableName="t_dept" domainObjectName="Dept"/>
    </context>
    </generatorConfiguration>
   ```

4. 执行（单击右侧[Maven]按钮，显示如图所示的界面。随后按照图上所表示的位置，右键"运行Maven"[mybatis-generator:generate]）
   ![逆向工程](2022-11-16-22-36-45.png)

### 分页功能

#### 分页功能分析

   底层原理

- 在SQL语句中使用limit关键字

- 几个必要的参数
    index：当前页的起始索引；pageSize：每页显示的条数；pageNum：当前页的页码
    count：总记录数；totalPage：总页数
  公式：`totalPage = count / pageSize;`→`if(count % pageSize!= 0){totalPage += 1;}`
  
  例：`pageSize=4, pageNum=1, index=0 limit(0,4)`
    `pageSize=4, pageNum=3, index=8 limit(8,4)`
    `pageSize=4, pageNum=6, index=20 limit(20,4)`
  公式：`index = (pageNum - 1) * pageSize`

#### 分页插件

1. 添加依赖
   
   ```xml
   <dependency>
            <groupId>com.github.pagehelper</groupId>
            <artifactId>pagehelper</artifactId>
            <version>5.2.0</version>
    </dependency>
   ```

2. 将插件配置到mybatis核心配置文件中
   
   ```xml
   <plugins>
        <!--配置分页插件-->
        <plugin interceptor="com.github.pagehelper.PageInterceptor"/>
    </plugins>
   ```

3. 编写测试类
   
   - 查询功能前开启分页功能：`PageHelper.startPage(int pageNum, int pageSize);`
     pageNum：当前页的页码；pageSize：每页显示的条数
   - 获取到list集合后，可以获取到与分页有关的数据。数据字段含义如下：
     pageNum：当前页的页码
     pageSize：每页显示的条数
     size：当前页显示的真实条数
     total：总记录数
     pages：总页数
     prePage：上一页的页码
     nextPage：下一页的页码
     isFirstPage/isLastPage：是否为第一页 / 最后一页
     hasPreviousPage/hasNextPage：是否存在上一页 / 下一页
     navigatePages：导航分页的页码数
     navigatepageNums：导航分页的页码， [1,2,3,4,5]
   - 分页字段原始数据：
     PageInfo{pageNum=1, pageSize=13, size=13, startRow=1, endRow=13, total=31, pages=3, list=Page{count=true, pageNum=1, pageSize=13, startRow=0, endRow=13, total=31, pages=3, reasonable=false, pageSizeZero=false
     }
   
   ```java
    public class PageTest {
     @Test
        public void testPage(){
            SqlSession sqlSession = SqlsessionUtil.getSqlSession();
            EmpMapper mapper = sqlSession.getMapper(EmpMapper.class);
            Page<Object> page = PageHelper.startPage(1, 4);
            List<Emp> list = mapper.selectByExample(null);
            PageInfo<Emp> pageInfo = new PageInfo<>(list,5);
            list.forEach(System.out::println);
            System.out.println(pageInfo);
        }
    }
   ```

## Spring

### Spring简介

#### Spring概述

官网地址：<https://spring.io/>

- Spring 是最受欢迎的企业级 Java 应用程序开发框架，数以百万的来自世界各地的开发人员使用Spring 框架来创建性能好、易于测试、可重用的代码。
- Spring 框架是一个开源的 Java 平台，它最初是由 Rod Johnson 编写的，并且于 2003 年 6 月首次在 Apache 2.0 许可下发布。     Spring 是轻量级的框架，其基础版本只有 2 MB 左右的大小。
- Spring 框架的核心特性是可以用于开发任何 Java 应用程序，但是在 Java EE 平台上构建 web 应用程序是需要扩展的。 Spring 框架的目标是使 J2EE 开发变得更容易使用，通过启用基于 POJO编程模型来促进良好的编程实践。

#### Spring家族

项目列表：<https://spring.io/projects>

#### Spring Framework

Spring 基础框架，可以视为 Spring 基础设施，基本上任何其他 Spring 项目都是以 Spring Framework为基础的。

##### Spring Framework特性

- 非侵入式：使用 Spring Framework 开发应用程序时，Spring 对应用程序本身的结构影响非常小。对领域模型可以做到零污染；对功能性组件也只需要使用几个简单的注解进行标记，完全不会破坏原有结构，反而能将组件结构进一步简化。这就使得基于 Spring Framework 开发应用程序时结构清晰、简洁优雅。
- **控制反转：IOC——Inversion of Control，翻转资源获取方向。把自己创建资源、向环境索取资源变成环境将资源准备好，我们享受资源注入。**
- **面向切面编程：AOP——Aspect Oriented Programming，在不修改源代码的基础上增强代码功能。**
- 容器：Spring IOC 是一个容器，因为它包含并且管理组件对象的生命周期。组件享受到了容器化的管理，替程序员屏蔽了组件创建过程中的大量细节，极大的降低了使用门槛，大幅度提高了开发效率。
- 组件化：Spring 实现了使用简单的组件配置组合成一个复杂的应用。在 Spring 中可以使用 XML和 Java 注解组合这些对象。这使得我们可以基于一个个功能明确、边界清晰的组件有条不紊的搭建超大型复杂应用系统。
- 声明式：很多以前需要编写代码才能实现的功能，现在只需要声明需求即可由框架代为实现。
- 一站式：在 IOC 和 AOP 的基础上可以整合各种企业应用的开源框架和优秀的第三方类库。而且 Spring 旗下的项目已经覆盖了广泛领域，很多方面的功能性需求可以在 Spring Framework 的基础上全部使用 Spring 来实现

##### Spring Framework 五大功能模块

| 功能模块                    | 功能介绍                            |
| ----------------------- | ------------------------------- |
| Core Container          | 核心容器，在Spring环境下使用任何功能都必须基于IOC容器 |
| AOP&Aspects             | 面向切面编程                          |
| Testing                 | 提供了对Junit或TestNG测试框架的整合         |
| Data Access/Integration | 提供了对数据访问/集成的功能                  |
| SpringMVC               | 提供了面向Web应用程序的集成功能               |

### IOC

#### IOC容器

##### IOC思想

IOC：Inversion of Control，翻译过来是**反转控制**

1. 获取资源的传统方式
   自己做饭：买菜、洗菜、择菜、改刀、炒菜，全过程参与，费时费力，必须清楚了解资源创建整个过程中的全部细节且熟练掌握。
   在应用程序中的组件需要获取资源时，传统的方式是组件 主动 的从容器中获取所需要的资源，在这样的模式下开发人员往往需要知道在具体容器中特定资源的获取方式，增加了学习成本，同时降低了开发效率。
2. 反转控制方式获取资源
   点外卖：下单、等、吃，省时省力，不必关心资源创建过程的所有细节。
   反转控制的思想完全颠覆了应用程序组件获取资源的传统方式：反转了资源的获取方向 —— 改由容器主动的将资源推送给需要的组件，开发人员不需要知道容器是如何创建资源对象的，只需要提供接收资源的方式即可，极大的降低了学习成本，提高了开发的效率。这种行为也称为查找的被动 形式。
3. DI
   DI ：Dependency Injection ，翻译过来是**依赖注入**。
   DI 是 IOC 的另一种表述方式：即组件以一些预先定义好的方式（例如： setter 方法）接受来自于容器 的资源注入。相对于IOC 而言，这种表述更直接。
   所以结论是： IOC 就是一种反转控制的思想，而 DI 是对 IOC 的一种具体实现。

##### IOC容器在Spring中的实现

 Spring 的 IOC 容器就是 IOC 思想的一个落地的产品实现。 IOC 容器中管理的组件也叫做 bean 。在创建bean 之前，首先需要创建 IOC 容器。 Spring 提供了 IOC 容器的两种实现方式：

1. BeanFactory
   这是 IOC 容器的基本实现，是 Spring 内部使用的接口。面向 Spring 本身，不提供给开发人员使用。

2. ApplicationContext
   BeanFactory 的子接口，提供了更多高级特性。面向 Spring 的使用者，几乎所有场合都使用

3. ApplicationContext 而不是底层的 BeanFactory。
   ApplicationContext的主要实现类
   ![Spring的层次结构](2022-11-19-21-00-21.png)
   
   | 类型名                             | 简介                                                                                          |
   | ------------------------------- | ------------------------------------------------------------------------------------------- |
   | ClassPathXmlApplicationContext  | 通过读取类路径下的 XML 格式的配置文件创建 IOC 容器对象                                                            |
   | FileSystemXmlApplicationContext | 通过文件系统路径读取 XML 格式的配置文件创建 IOC 容器对象                                                           |
   | ConfigurableApplicationContext  | ApplicationContext 的子接口，包含一些扩展方法refresh() 和 close() ，让 ApplicationContext 具有启动、关闭和刷新上下文的能力。 |
   | WebApplicationContext           | 专门为 Web 应用准备，基于 Web 环境创建 IOC 容器对象，并将对象引入存入 ServletContext 域中。                               |

#### 基于XML管理bean

##### 实验一：入门案例

1. 创建Maven Module

2. 引入依赖

```xml
        <dependencies>
        <!--基于Maven依赖传递性，导入spring-context依赖即可导入当前所需所有jar包-->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context</artifactId>
            <version>5.3.1</version>
        </dependency>
        <!--junit测试-->
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
            <scope>test</scope>
        </dependency>
    </dependencies>
```

![Spring依赖项](2022-11-19-21-48-20.png)

3. 创建类
   
   ```java
   public class HelloWorld {
    public void sayHello(){
        System.out.println("hello,spring");
        }
    }
   ```

4. 创建Spring的配置文件

在Resource包下新建（右键该文件夹→新建>XML配置文件>Spring配置）（若不存在该菜单则需要检查依赖是否已被正确引入），（建议）起名为“applicationContext”

5. 在该配置文件中编写如下的代码
   bean标签：配置一个bean对象，将该对象交给IOC管理
    属性：`id`：bean的唯一标识，不能重复
   
          `class`：设置bean对象所对应的类型
          `scope`：设置bean的作用域`prototype/singleton`
            `prototype`：单例。表示获取该bean所对应的对象都是同一个
            `singleton`：多例。表示获取该bean所对应的对象都不是同一个

```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="helloworld" class="com.tl.spring.pojo.HelloWorld"/>
</beans>
```

6. 创建测试类进行测试

```java
@Test
    public void test(){
        //获取IOC容器
        ApplicationContext ioc = new ClassPathXmlApplicationContext("applicationContext.xml");
        //获取IOC容器中的bean
        HelloWorld helloworld = (HelloWorld) ioc.getBean("helloworld");
        helloworld.sayHello();
    }
```

7. 注意：实体类中必须有无参构造函数，即`public xxx(){};`，否则会报错：
   `java.lang.NoSuchMethodException`

##### 实验二：获取bean

1. 方式一：根据id获取（注意类型转换）

`Student studentOne = (Student)ioc.getBean("studentOne");`

2. 方式二：根据类型获取

注意：根据类型获取bean时，要求IOC容器有且仅有一个类型匹配的bean，否则抛出异常：`NoUniqueBeanDefinitionException`；若没有任何一个类型匹配bean，也会抛出异常：`NoSuchBeanDefinitionException`

`Student student = ioc.getBean(Student.class);`

3. 方式三：根据id和类型获取

`Student student = ioc.getBean("studentOne", Student.class);`

4. 扩展

Q①：如果组件类实现了接口，根据接口类型可以获取 bean 吗？
A：可以，前提是 bean 唯一
例：Student类实现了Person接口，此时获取bean可以写为：`Person person = ioc.getBean(Person.class);`
Q②：如果一个接口有多个实现类，这些实现类都配置了 bean ，根据接口类型可以获取 bean 吗？
A：不行，因为 bean 不唯一

5. 结论
   根据类型来获取 bean 时，在满足 bean 唯一性的前提下，其实只是看：『对象instanceof 指定的类型』的返回结果，只要返回的是true 就可以认定为和类型匹配，能够获取到。**即通过bean的类型、bean所继承的类的类型、bean所实现的接口的类型都可以获取bean**。

##### 实验三：依赖注入——setter注入

1. 创建pojo

```java
public class Student {
    private String name;
    private int age;
    private Dept dept;

    public Student(String name, int age, Dept dept) {
        this.name = name;
        this.age = age;
        this.dept = dept;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public Dept getDept() {
        return dept;
    }

    public void setDept(Dept dept) {
        this.dept = dept;
    }

    @Override
    public String toString() {
        return "Student{" +
                "name='" + name + '\'' +
                ", age=" + age +
                ", dept=" + dept +
                '}';
    }

    public Student() {
    }

    public Student(String name, int age) {
        this.name = name;
        this.age = age;
    }
```

2. 配置bean时为其属性赋值
   `property`：通过成员变量的set方法进行赋值
    `name`：设置需要赋值的属性名（和set方法有关）
    `value`：设置属性值
   
   ```xml
    <bean id="studentTwo" class="com.tl.spring.pojo.Student">
        <property name="sid" value="1001"></property>
        <property name="sname" value="张三"></property>
        <property name="age" value="23"></property>
        <property name="gender" value="男"></property>
    </bean>
   ```

3. 测试

```java
    @Test
    public void testDI(){
        //获取IOC容器
        ApplicationContext ioc = new ClassPathXmlApplicationContext("spring-ioc.xml");
        //获取Bean
        Student student = ioc.getBean("studentTwo", Student.class);
        System.out.println(student);
    }
```

##### 实验四：依赖注入——构造器注入

1. 在Student类中添加有参构造

```java
    public Student(Integer id,String name,Integer age,String sex){  
      this.id=id;
      this.name=name;
      this.age=age;
      this.sex=sex;
    }
```

2. 配置bean

`constructor-arg`标签还有两个属性可以进一步描述构造器参数：
    `index`属性：指定参数所在位置的索引（从0开始）
    `name`属性：指定参数名

```xml
    <bean id="studentTwo"class="com.atguigu.spring.bean.Student">
      <constructor-arg value="1002"></constructor-arg>
      <constructor-arg value="李四"></constructor-arg>
      <constructor-arg value="33"></constructor-arg>
      <constructor-arg value="女"></constructor-arg>
</bean>
```

3. 测试

```java
    @Test
    public void testDIBySet(){
      ApplicationContext ac = new ClassPathXmlApplicationContext("spring-di.xml");
     StudentstudentOne = ac.getBean("studentTwo",Student.class);
      System.out.println(studentOne);
}
```

##### 实验五：特殊值处理

1. 字面量赋值

> 什么是字面量？
> `int a = 10;`
> 声明一个变量 a ，初始化为 10 ，此时 a 就不代表字母 a 了，而是作为一个变量的名字。当我们引用 a
> 的时候，我们实际上拿到的值是 10 。
> 而如果 a 是带引号的： 'a' ，那么它现在不是一个变量，它就是代表 a 这个字母本身，这就是字面
> 量。所以字面量没有引申含义，就是我们看到的这个数据本身。
> **使用values属性给bean的属性赋值时，spring会把value属性的值看作字面量**

`<property name="name" value="张三"/>`

2. 赋空值

```xml
    <property name="name">  
    <null/>
    </property>
```

注意：若写作`<property name="name" value="null"></property>`则name赋值为`"null"`。

3. xml实体
   常用特殊字符实体：`<：&lt;`、`>：&gt;`
   小于号在xml文档中用于定义标签的开始，不能随意使用
   解决方案：`<property name="expression" value="a &lt; b">`

4. CDATA节

该节中的内容会原样解析；CDATA节是xml中一个特殊的标签，因此不能写在属性中
错误写法：`<property name="name" value="<![CDATA[<王五>]]>"/>`
正确写法：

```xml
    <property name="name">  
        <value><![CDATA[<王五>]]></value>
    </property>
```

*快速生成CDATA（IDEA操作）：在需要插入CDATA节的地方，输入大写`CD`，按回车即可完成插入*

##### 实验六：为类类型变量赋值

1. 创建班级类Clazz

```java
    public class Clazz {
        private Integer cid;
        private String cname;

        public Integer getCid() {
            return cid;
        }

        public void setCid(Integer cid) {
            this.cid = cid;
        }

        public String getCname() {
            return cname;
        }

        public void setCname(String cname) {
            this.cname = cname;
        }

        public Clazz() {
        }

        public Clazz(Integer cid, String cname) {
            this.cid = cid;
            this.cname = cname;
        }

        @Override
        public String toString() {
            return "Clazz{" +
                    "cid=" + cid +
                    ", cname='" + cname + '\'' +
                    '}';
        }
}
```

2. 修改Student类，在Student类中添加如下代码

```java
    private Clazz clazz{};
    //构造方法、getter/setter、toString均省略
```

3. 方式一：引用外部的bean
   **`ref`：引用IOC容器中某个bean的id**
   
   ```xml
    <bean id="studentFive" class="com.tl.spring.pojo.Student">
        <property name="sid" value="1004"></property>
        <property name="sname" value="赵六"></property>
        <property name="age" value="26"></property>
        <property name="gender" value="男"></property>
        <property name="clazz" ref="clazzOne"></property>
    </bean>
    <bean>
        <bean id="clazzOne" class="com.tl.spring.pojo.Clazz">
        <property name="cid" value="1111"></property>
        <property name="cname" value="火箭班"></property>
    </bean>
   ```

**注意，不能写作`<property name="clazz" value="clazzOne">`。会抛出异常`java.lang.IllegalStateException`**
原因：若用value属性，则说明Spring将`Clazz`视为一个普通的字符串，并不能解析为一个bean的id

4. 方式二：级联方式赋值（不推荐此方式）
   **要保证提前为该属性赋值或者实例化**

```xml
    <property name="clazz" ref="clazzOne"></property>
    <property name="clazz.clazzId" value="3333"></property>
    <property name="clazz.clazzName" value="最强王者班"></property>
```

5. 方式三：内部bean
   **只能在当前bean的内部使用，不能直接通过IOC容器获取**

```xml
        <property name="clazz">
        <bean id="clazzInner" class="com.tl.spring.pojo.Clazz">
            <property name="cid" value="2222"></property>
            <property name="cname" value="北大青鸟班"></property>
        </bean>
    </property>
```

##### 实验七：为数组、集合类型赋值

1. 修改Student类，在Student类中添加如下代码

```java
    private String[] hobby{};
    //构造方法、getter/setter、toString均省略
```

2. 编写映射文件

数组内存放的是字面量类型时，用`value`标签；数组内存放的是类类型，使用`ref`标签

```xml
<property name="hobby">
    <array>
        <value>抽烟</value>
        <value>喝酒</value>
        <value>烫头</value>
    </array>
</property>
```

3. 为集合类型赋值
- List集合
  
  - 方式一：通过内部的List集合赋值
    
    ```xml
    <property name="students">
        <list>
            <ref bean="studentOne"></ref>
            <ref bean="studentTwo"></ref>
            <ref bean="studentThree"></ref>
        </list>
    </property>
    ```
  
  - 方式二：引用list集合的bean
    *需要使用util的约束（IDEA会自动导入）*：`<util:list id=""></util:list>`
    
    ```xml
    <util:list id="studentList">
        <ref bean="studentOne"></ref>
        <ref bean="studentTwo"></ref>
        <ref bean="studentThree"></ref>
    </util:list>
    ```

- Map集合
  
  - 方式一：通过内部的Map集合赋值
    
    - 创建Java文件
      
      ```java
      public class Teacher{};
      //构造方法、getter/setter、toString均省略
      ```
    
    - 在Student类中添加教师信息的Map：`private Map<String,Teacher> teacherMap;`
    
    - 设置bean的信息
      
      ```xml
      <bean id="teacherOne" class="com.tl.spring.pojo.Teacher">
          <property name="tid" value="10086"></property>
          <property name="tname" value="大宝"></property>
      </bean>
      
      <bean id="teacherTwo" class="com.tl.spring.pojo.Teacher">
          <property name="tid" value="10010"></property>
          <property name="tname" value="小宝"></property>
      </bean>
      ```
    
    - 将教师的id为键，教师的对象为值
      说明：一个`<entry>`所标记的内容为一个键值对；`<key>`表示设置的键，`<value>`表示设置 的值；`<xx-ref>`表示某个类类型
      
      ```xml
      <property name="teacherMap">
          <map>
              <entry key="10086" value-ref="teacherOne"></entry>
              <entry key="10010" value-ref="teacherTwo"></entry>
          </map>
      </property>
      ```
  
  - 方式二：引用Map集合的bean
    
    ```xml
    <util:map id = "teacherMap">
        <entry key="10086" value-ref="teacherOne"></entry>
        <entry key="10010" value-ref="teacherTwo"></entry>
    </util:map>
    ```

##### 实验八：p命名空间为成员变量赋值

1. 导入p命名空间的约束（实际上只需要输入`p:`就可以完成导入）

```xml
<?xml version="1.0" encoding="UTF-8"?>
  <beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:p="http://www.springframework.org/schema/p"
    xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

</beans>
```

2. 配置get、set方法

3. 在spring中配置bean对象

```xml
 <bean id="studentSix" class="com.tl.spring.pojo.Student" p:sid="1005" p:sname="小明" p:teacherMap-ref="teacherMap"/>
```

##### 实验九：引入外部属性文件

1. 加入依赖

```xml
<!-- Mysql驱动 -->
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>8.0.30</version>
</dependency>
<!-- 数据源 -->
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>druid</artifactId>
    <version>1.1.23</version>
</dependency>
```

2. 创建配置文件：spring-datasource.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
    <bean id="datasource" class="com.alibaba.druid.pool.DruidDataSource">
        <property name="driverClassName" value="com.mysql.cj.jdbc.Driver"/>
        <property name="url" value="jdbc:mysql://localhost:3306/ssm?serverTimezone=UTC"/>
        <property name="username" value="root"/>
        <property name="password" value="root"/>

    </bean>
</beans>
```

3. 数据源的配置

```xml
    <bean id="datasource" class="com.alibaba.druid.pool.DruidDataSource">
        <property name="driverClassName" value="com.mysql.cj.jdbc.Driver"></property>
        <property name="url" value="jdbc:mysql://localhost:3306/ssm?serverTimezone=UTC"></property>
        <property name="username" value="root"></property>
        <property name="password" value="root"></property>
    </bean>
```

其他与数据源有关的配置（了解即可，它们均有默认值）

- `initalSize`：设置当前数据库连接池初始化设置的连接个数
- `maxActive`：最大能存在的连接数量，默认为8
- `maxWait`：设置等待德鲁伊连接池分配的最大等待时间

注：可以引入jdbc.properties文件来实现配置
jdbc.properties新建方式：右键resource文件夹，新建→资源包
jdbc.properties文件的内容：

```properties
    jdbc.driver=com.mysql.cj.jdbc.Driver
    jdbc.url=jdbc:mysql://localhost:3306/ssm?serverTimezone=UTC
    jdbc.username=root
    jdbc.password=root
```

上述配置便可改写为：

```xml
<!--    引入jdbc.properties.之后可以通过${key}的方式访问value-->
    <context:property-placeholder location="jdbc.properties"></context:property-placeholder>

    <bean id="datasource" class="com.alibaba.druid.pool.DruidDataSource">
        <property name="driverClassName" value="${jdbc.driver}"/>
        <property name="url" value="${jdbc.url}"/>
        <property name="username" value="${jdbc.username}"/>
        <property name="password" value="${jdbc.password}"/>

    </bean>
```

4. 编写测试类

```java
    @Test
    public void testDataSource() throws SQLException {
        ApplicationContext ioc = new ClassPathXmlApplicationContext("spring-datasource.xml");
        DruidDataSource dataSource = ioc.getBean(DruidDataSource.class);
        System.out.println(dataSource.getConnection());
    }
```

##### 实验十：bean的作用域

1. 概念
   在Spring中可以通过配置bean标签的scope属性来指定bean的作用域范围，各取值含义如下表：
   
   | 取值            | 含义                      | 创建对象的时机   |
   | ------------- | ----------------------- | --------- |
   | singleton(默认) | 在IOC容器中，这个bean的对象始终为单实例 | IOC容器初始化时 |
   | prototype     | 这个bean在IOC容器中有多个实例      | 获取bean时   |
   
   如果是在WebApplicationContext环境下还会有另外两个作用域（但不常用）
   
   | 取值      | 含义         |
   | ------- | ---------- |
   | request | 在一个请求范围内有效 |
   | session | 在一个会话范围内有效 |

2. 创建类Student

```java
public class Student {
    private Integer sid;
    private String sname;


    @Override
    public String toString() {
        return "Student{" +
                ", sid=" + sid +
                ", sname='" + sname + '\'' +
                '}';
    }

    public Student(Integer sid, String sname) {
        this.sid = sid;
        this.sname = sname;
    }


    public Integer getSid() {
        return sid;
    }

    public void setSid(Integer sid) {
        this.sid = sid;
    }

    public String getSname() {
        return sname;
    }

    public void setSname(String sname) {
        this.sname = sname;
    }
}
```

3. 配置bean

```xml
    <bean id="student" class="com.tl.spring.pojo.Student" scope="prototype">
        <property name="sid" value="1001"></property>
        <property name="sname" value="张三"></property>
    </bean>
```

`scope`：设置bean的作用域
    `scope="singleton | prototype"`
    `singleton`（单例）：表示获取该bean所对应的对象都是同一个
    `prototype`（多例）：表示获取该bean所对应的对象都不是同一个

4. 编写测试类

```java
public class ScopeTest {
    @Test
    public void testScope(){
        ApplicationContext ioc = new ClassPathXmlApplicationContext("spring-scope.xml");
        Student student1 = ioc.getBean(Student.class);
        Student student2 = ioc.getBean(Student.class);
        System.out.println(student1==student2);
        // 注：若作用域为singleton，返回True；否则返回False
    }
}
```

##### 实验十一：bean的生命周期

1. 生命周期过程
- bean对象创建（调用无参构造器）

- 给bean对象设置属性

- bean对象初始化之前操作（由bean的后置处理器负责）

- bean对象初始化（需在配置bean时指定初始化方法）

- bean对象初始化之后操作（由bean的后置处理器负责）

- bean对象就绪可以使用

- bean对象销毁（需在配置bean时指定销毁方法）

- IOC容器关闭
2. 创建类

```java
package com.tl.spring.pojo;

public class User {
    private Integer id;
    private String username;
    private String password;
    private Integer age;

    public User() {
    }

    public User(Integer id, String username, String password, Integer age) {
        this.id = id;
        this.username = username;
        this.password = password;
        this.age = age;
    }


    public Integer getId() {
        return id;
    }

    public void setId(Integer id) {
        this.id = id;
    }

    public String getUsername() {
        return username;
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public String getPassword() {
        return password;
    }

    public void setPassword(String password) {
        this.password = password;
    }

    public Integer getAge() {
        return age;
    }

    public void setAge(Integer age) {
        this.age = age;
    }

    @Override
    public String toString() {
        return "User{" +
                "id=" + id +
                ", username='" + username + '\'' +
                ", password='" + password + '\'' +
                ", age=" + age +
                '}';
    }
}
```

3. 创建配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="user" class="com.tl.spring.pojo.User" init-method="initMethod" destroy-method="destroyMethod">
        <property name="id" value="1"></property>
        <property name="username" value="admin"></property>
        <property name="password" value="123456"></property>
        <property name="age" value="23"></property>
    </bean>
</beans>
```

4. 改写User类
- 无参构造方法：实例化

```java
    public User() {
        System.out.println("生命周期1：实例化");

    }
```

- 依赖注入

```java
    public void setId(Integer id) {
        System.out.println("生命周期2：依赖注入");
        this.id = id;
    }
```

- 初始化。需要通过bean的`init-method`属性指定初始化的方法

```java
public void initMethod(){
        System.out.println("生命周期3：初始化");
    }
```

- IOC容器关闭时销毁。需要通过bean的`destroy-method`属性指定销毁的方法

```java
    public void destroyMethod(){
        System.out.println("生命周期4：销毁");
    }
```

5. 创建测试类

`ConfigurableApplicationContext`是`ApplicationContext`的子接口，其中扩展了刷新和关闭容器的的方法

```java
public class LifeCycleTest {
    @Test
    public void test(){

        ConfigurableApplicationContext ioc = new ClassPathXmlApplicationContext("spring-lifecycle.xml");
        User user = ioc.getBean(User.class);
        System.out.println(user);
        ioc.close();
    }
```

注意：若bean的作用域为单例时，生命周期的前三个步骤会在获取IOC容器时执行；若bean的作用域为多例时，生命周期的前三个步骤会在获取bean时执行

6. bean的后置处理器

bean的后置处理器会在生命周期的初始化前后添加额外的操作，需要实现`BeanPostProcessor`接口，且配置到IOC容器中，需要注意的是，bean的后置处理器不是单独针对某一个bean生效，而是针对IOC容器中所有bean都会执行

创建bean的后置处理器

```java
public class MyBeanPostProcessor implements BeanPostProcessor {

    @Override
    public Object postProcessBeforeInitialization(Object bean, String beanName) throws BeansException {
        //此方法在bean的生命周期初始化之前执行
        System.out.println("MyBeanPostProcessor-->后置处理器postProcessBeforeInitialization");
        return BeanPostProcessor.super.postProcessBeforeInitialization(bean, beanName);
    }

    @Override
    public Object postProcessAfterInitialization(Object bean, String beanName) throws BeansException {
        //此方法在bean的生命周期初始化之后执行
        System.out.println("MyBeanPostProcessor-->postProcessAfterInitialization");
        return BeanPostProcessor.super.postProcessAfterInitialization(bean, beanName);
    }
}
```

7. 为后置处理器添加bean

`<bean id="myBeanPostProcessor" class="com.tl.spring.process.MyBeanPostProcessor"></bean>`

##### 实验十三：FactoryBean

1. 简介

FactoryBean是Spring提供的一种整合第三方框架的常用机制。和普通的bean不同，配置一个FactoryBean类型的bean，在获取bean的时候得到的并不是class属性中配置的这个类的对象，而是getObject()方法的返回值。通过这种机制，Spring可以帮我们把复杂组件创建的详细过程过程和繁琐细节都屏蔽起来，只把最简洁的使用界面展示给我们。
将来整合Mybatis时，Spring就是通过FactoryBean机制来帮我们创建SQLSessionFactory对象的
FactoryBean是一个接口，需要创建一个类实现该接口。其中有三个方法：

- `getObject()`：通过一个对象交给IOC容器管理

- `getObjectType()`：设置所提供对象的类型

- `isSingleton()`：所提供的对象是否单例
  当把FactoryBean的实现类配置为bean时，会把当前类中`getObject()`所返回的对象交给IOC容器管理
2. 创建FactoryBean

```java
public class UserFactoryBean implements FactoryBean<User> {
    @Override
    public User getObject() throws Exception {
        return new User();
    }

    @Override
    public Class<?> getObjectType() {
        return User.class;
    }
}
```

3. 配置bean

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean class="com.tl.spring.factory.UserFactoryBean"></bean>
</beans>
```

4. 测试

```java
public class UserFactoryBean implements FactoryBean<User> {
    @Override
    public User getObject() throws Exception {
        return new User();
    }

    @Override                                                                                            getObjectType() {
        return User.class;
    }
}
```

##### 实验十四：基于XML的自动装配

> 自动装配：根据指定的策略，在IOC容器中匹配某一个bean，自动为指定的bean中所依赖的类类型或接口类型属性赋值

1. 场景模拟
- 创建类UserController

```java
public class UserController {

    private UserService userService;

    public UserService getUserService() {
        return userService;
    }

    public void setUserService(UserService userService) {
        this.userService = userService;
    }
    public void saveUser(){
        userService.saveUser();
    }
}
```

- 创建接口

```java
public interface UserService {
    void saveUser();
}
```

- 创建Service层实现类

```java
public class UserServiceImpl implements UserService {
    private UserDao userDao;

    public UserDao getUserDao() {
        return userDao;
    }

    public void setUserDao(UserDao userDao) {
        this.userDao = userDao;
    }

    @Override
    public void saveUser() {
        userDao.saveUser();
    }
}
```

- 创建dao层

```java
public interface UserDao {

    void saveUser();
}
```

- 创建dao层实现类

```java
public class UserDaoImpl implements UserDao {
    @Override
    public void saveUser() {
        System.out.println("保存成功");

    }
}
```

2. 配置bean（这里并没有使用自动装配）

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="userController" class="com.tl.spring.controller.UserController">
        <property name="userService" ref="userService"></property>
    </bean>
    <bean id="userService" class="com.tl.spring.service.impl.UserServiceImpl">
        <property name="userDao" ref="userDao"></property>
    </bean>
    <bean id="userDao" class="com.tl.spring.dao.impl.UserDaoImpl"></bean>
</beans>
```

（使用了自动装配）

```xml
    <bean id="userController" class="com.tl.spring.controller.UserController" autowire="byType">
    </bean>
    <bean id="userService" class="com.tl.spring.service.impl.UserServiceImpl" autowire="byType">
    </bean>
    <bean id="userDao" class="com.tl.spring.dao.impl.UserDaoImpl"></bean>
</beans>
```

自动装配的策略：

- no、default：表示不装配，即bean中的属性不会自动匹配某个bean为属性赋值，此时属性使用默认值

- byType：根据要赋值的属性的类型，在IOC容器中匹配某个bean，为属性赋值

- 注意：若通过类型没有找到任何一个类型匹配的bean，此时不装配，属性使用默认值；若通过类型找到了多个类型匹配的bean，此时会抛出异常`noUniqueBeanDefinitionException`。当使用byType实现自动装配时，IOC容器中有且只有一个类型匹配的bean能够为属性赋值。

- byName：将要赋值的属性的属性名作为bean的id在IOC容器中匹配某个bean，为属性赋值。当类型匹配的bean有多个时，此时可以实现byName实现自动装配
3. 测试

```java
public class AutowireByXMLTest {
    @Test
    public void testAutowire(){
        ApplicationContext ioc = new ClassPathXmlApplicationContext("spring-autowire-xml.xml");
        UserController userController = ioc.getBean(UserController.class);
        userController.saveUser();
    }
}
```

#### 基于注解管理bean

##### 实验一：标记与扫描

1. 导入Maven模块

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.tl.spring</groupId>
    <artifactId>spring_ioc_annotation</artifactId>
    <version>1.0-SNAPSHOT</version>

    <properties>
        <maven.compiler.source>11</maven.compiler.source>
        <maven.compiler.target>11</maven.compiler.target>
    </properties>

    <dependencies>
        <!--基于Maven依赖传递性，导入spring-context依赖即可导入当前所需所有jar包-->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context</artifactId>
            <version>5.3.1</version>
        </dependency>
        <!--junit测试-->
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
            <scope>test</scope>
        </dependency>

        <!--        Mysql驱动-->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>8.0.30</version>
        </dependency>
        <dependency>
            <groupId>org.testng</groupId>
            <artifactId>testng</artifactId>
            <version>RELEASE</version>
            <scope>compile</scope>
        </dependency>
        <dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter</artifactId>
            <version>RELEASE</version>
            <scope>compile</scope>
        </dependency>
    </dependencies>
</project>
```

2. 创建Spring配置文件

3. 标识组件的常用注解（这四个注解功能一模一样，只是给开发人员看（代码可读性），让开发人员区分组件的功能）
- `@Component`：将类标识为普通组件
- `@Controller`：将类标识为控制层组件
- `@Service`：将类标识为业务层组件
- `@Repository`：将类标识为持久层组件

四个注解间的关系：均由`@Component`扩展而来
![bean的注解](2022-12-25-19-05-20.png)

4. 创建组件

```java
    @Controller
    public class UserController {
    }
```

```java
    public interface UserService {
    }
```

```java
    @Service
    public class UserServiceImpl implements UserService {
    }
```

```java
    public interface UserDao {
    }
```

```java
    @Repository
    public class UserDaoImpl implements UserDao {
    }
```

5. 扫描组件
- 情况一：最基本的扫描方式
  
  ```xml
  <context:component-scan base-package="com.tl.spring"/>
  <!-- 写的越详细，扫描的时间越短；否则越长 -->
  ```

- 情况二：指定要排除的组件

`<context:exclude-filter></<context:exclude-filter>`：排除扫描
type：设置排除扫描的方式
`type="annotation"`：根据注解的类型进行排除，`expression`需要设置排除的注解的全类名
`type="assignable"`：根据类的类型进行排除，`expression`需要设置排除的类的全类名
`<context:include-filter></context:include-filter>`：包含扫描
注意：需要在`<<context:component-scan></<context:component-scan>`标签中设置`use-default-filters="false"`
`use-default-filters="true"`（默认）：所设置的包下所有的类都需要扫描，此时可以使用排除扫描
`use-default-filters="false"`：所设置的包下所有的类都不需要扫描，此时可以使用包含扫描

```xml
    <context:component-scan base-package="com.tl.spring">
    <!-- 排除扫描 -->
        <context:exclude-filter type="annotation" expression="org.springframework.stereotype.Controller"/>
        <context:exclude-filter type="assignable" expression="com.tl.spring.controller.UserController"/>
    </context:component-scan>
```

```xml
    <context:component-scan base-package="com.tl.spring" use-default-filters="false">
    <!-- 包含扫描 -->
        <context:include-filter type="annotation" expression="org.springframework.stereotype.Controller"/>
    </context:component-scan>
```

7. 组件所对应的bean的id
   通过注解+扫描所配置的bean的id，默认值为类的小驼峰，即类名的首字母为小写的结果

```java
    ioc.getBean("userController",UserController.class);
    ioc.getBean("userServiceImpl",UserService.class);
    ioc.getBean("userDaoImpl",UserDao.class);
```

可以通过标识组件的注解的value属性值设置bean的自定义id，如：`@Controller("controller")`

##### 实验二：基于注解的自动装配

1. 场景模拟（参考基于xml的自动装配）
   在UserController中声明UserService对象；在UserServiceImpl中声明UserDao对象

```java
    @Autowired
    private UserService userService;
```

```java
    @Autowired
    private UserDao userDao;
```

2. `@Autowired`注解：实现自动装配功能的注解

```java
@Controller
public class UserController {
    @Autowired
    private UserService userService;
    public void saveUser(){
        userService.saveUser();
    }
}
```

```java
public interface UserService {
    void saveUser();
}
@Service
public class UserServiceImpl implements UserService {
    @Autowired
    private UserDao userDao;
    @Override
    public void saveUser() {
        userDao.saveUser();
    }
}
```

```java
public interface UserDao {
    void saveUser();
}
```

```java
@Repository
public class UserDaoImpl implements UserDao {
    @Override
    public void saveUser() {
        System.out.println("保存成功");
    }
}
```

3. `@Autowired`能够标识的位置：
- 标识在成员变量上，此时不需要设置成员变量的setXxx()方法；

```java
    @Autowired
    private UserService userService;
```

- 标识在setXxx()方法；

```java
    @Autowired
    public void setUserService(UserService userService) {
        this.userService = userService;
    }
```

- 为当前成员变量赋值的有参构造上

```java
    @Autowired
    public UserController(UserService userService) {
        this.userService = userService;
    }
```

4. `@Autowired`的原理
- 默认通过byType的方式，在IOC容器中通过类型匹配某个bean为属性赋值
- 若有多个类型匹配的bean，此时会自动转换为byName的方式实现自动装配的结果，即——将要赋值的属性的属性名作为bean的id匹配某个bean为属性赋值
- 若byType和byName的方式都无法实现自动装配，即IOC容器中有多个类型匹配的bean，且这些bean的id和要赋值的属性的属性名都不一致，此时抛异常：NoUniqueBeanDefinitionException
- 此时可以再要赋值的属性上，添加一个注解`@Qualifier`，通过该注解的value属性值，指定某个bean的id，将这个bean为属性赋值
- 注意：若IOC容器中没有任何一个类型匹配的bean，此时会抛出异常：`NoSuchBeanDefinitionException`；在`@Autowired`注解中有个属性required，默认值为true，要求必须完成自动装配，可以将required设置为false，此时能装配则装配，无法装配则使用属性的默认值

### AOP

#### 场景模拟

##### 声明接口

- 声明计算器接口Calculator，包含加减乘除的抽象方法
  
  ```java
  public interface Calculator {
      int add(int i, int j);
      int sub(int i, int j);
      int mul(int i, int j);
      int div(int i, int j);
  }
  ```

##### 创建实现类

```java
    public class CalculatorImpl implements Calculator{
        @Override
        public int add(int i, int j) {
            int result = i + j;
            System.out.println("方法内部，result:" + result);
            return result;
        }

        @Override
        public int sub(int i, int j) {
            int result = i - j;
            System.out.println("方法内部，result:" + result);
            return result;
        }

        @Override
        public int mul(int i, int j) {
            int result = i * j;
            System.out.println("方法内部，result:" + result);
            return result;
        }

        @Override
        public int div(int i, int j) {
            int result = i / j;
            System.out.println("方法内部，result:" + result);
            return result;
        }
    }
```

##### 创建带日志功能的实现类

```java
    public class CalculatorImpl implements Calculator{
    @Override
    public int add(int i, int j) {
        System.out.println("日志，方法：add，参数：" + i+","+j);
        int result = i + j;
        System.out.println("方法内部，result:" + result);
        System.out.println("日志，方法：add，参数：" + result);
        return result;
    }

    @Override
    public int sub(int i, int j) {
        System.out.println("日志，方法：sub，参数：" + i+","+j);
        int result = i - j;
        System.out.println("方法内部，result:" + result);
        System.out.println("日志，方法：sub，参数：" + result);
        return result;
    }

    @Override
    public int mul(int i, int j) {
        System.out.println("日志，方法：mul，参数：" + i+","+j);
        int result = i * j;
        System.out.println("方法内部，result:" + result);
        System.out.println("日志，方法：mul，参数：" + result);
        return result;
    }

    @Override
    public int div(int i, int j) {
        System.out.println("日志，方法：div，参数：" + i+","+j);

        int result = i / j;
        System.out.println("方法内部，result:" + result);
        System.out.println("日志，方法：div，参数：" + result);
        return result;
        }
    }
```

##### 提出问题

1. 现有代码缺陷
   针对带日志功能的实现类，我们发现有如下缺陷：对核心业务功能有干扰，导致程序员在开发核心业务功能时分散了精力；附加功能分散在各个业务功能方法中，不利于统一维护
2. 解决思路
   解决这两个问题，核心就是：**解耦**。我们需要把附加功能从业务功能代码中抽取出来。
3. 困难
   解决问题的困难：要抽取的代码在方法内部，靠以前把子类中的重复代码抽取到父类的方式没法解决。所以需要引入新的技术。

#### 代理模式

##### 概念

1. 介绍
   二十三种设计模式中的一种，属于结构型模式。它的作用就是通过提供一个代理类，让我们在调用目标方法的时候，不再是直接对目标方法进行调用，而是通过代理类**间接**调用。让不属于目标方法核心逻辑的代码从目标方法中剥离出来——**解耦**。调用目标方法时先调用代理对象的方法，减少对目标方法的调用和打扰，同时让附加功能能够集中在一起也有利于统一维护。

2. 生活中的代理
   
   - 广告商找大明星拍广告需要经过经纪人
   - 合作伙伴找大老板谈合作要约见面时间需要经过秘书
   - 房产中介是买卖双方的代理

3. 相关术语
   
   - 代理：将非核心逻辑剥离出来以后，封装这些非核心逻辑的类、对象、方法。
   - 目标：被代理“套用”了非核心逻辑代码的类、对象、方法。

##### 静态代理

创建静态代理类：

```java
public class CalculatorStaticProxy implements Calculator{

    //将被代理的目标对象声明为成员变量
    private CalculatorImpl target;
    public CalculatorStaticProxy(CalculatorImpl target) {
        this.target = target;
    }

    @Override
    public int add(int i, int j) {
        //附加功能由代理类中的代理方法来实现
        System.out.println("日志，方法：add，参数" + i+","+"j");
        //通过目标对象来实现核心业务逻辑
        int result = target.add(i, j);
        System.out.println("日志，方法：add，结果" +result);
        return result;
    }

    @Override
    public int sub(int i, int j) {
        System.out.println("日志，方法：sub，参数" + i+","+"j");
        int result = target.add(i, j);
        System.out.println("日志，方法：sub，结果" +result);
        return result;
    }

    @Override
    public int mul(int i, int j) {
        System.out.println("日志，方法：mul，参数" + i+","+"j");
        int result = target.add(i, j);
        System.out.println("日志，方法：mul，结果" +result);
        return result;
    }

    @Override
    public int div(int i, int j) {
        System.out.println("日志，方法：div，参数" + i+","+"j");
        int result = target.add(i, j);
        System.out.println("日志，方法：div，结果" +result);
        return result;
    }
}
```

> 静态代理确实实现了解耦，但是由于代码都写死了，完全不具备任何的灵活性。就拿日志功能来说，将来其他地方也需要附加日志，那还得再声明更多个静态代理类，那就产生了大量重复的代码，日志功能还是分散的，没有统一管理。提出进一步的需求：将日志功能集中到一个代理类中，将来有任何日志需求，都通过这一个代理类来实现。这就需要使用动态代理技术了。

##### 动态代理

动态代理分为两种：

- JDK动态代理，要求必须必须有接口，最终生成的代理类和目标类实现相同的接口，在com.sun.proxy包下，类名为$proxy2

- cglib动态代理，最终生成的代理类会继承目标类，并且和目标类在相同的包下
1. 生产代理对象的工厂类：
    ClassLoader loader：指定加载动态生成的代理类的类加载器
    Class[] interfaces：获取目标对象实现的所有接口的class对象的数组
    InvocationHandler h：设置代理类中的抽象方法如何重写

```java
public class ProxyFactory {
    private Object target;
    public ProxyFactory(Object target) {
        this.target = target;
    }
    public Object getProxy(){

        ClassLoader classLoader = this.getClass().getClassLoader();
        Class<?>[] interfaces = target.getClass().getInterfaces();
        InvocationHandler h = new InvocationHandler() {
            @Override
            /*proxy：表示代理对象，
            method表示要执行的方法，
            args表示要执行的方法的参数列表
            */
            public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
                Object result = null;
                try {
                    System.out.println("日志，方法：" + method.getName()+",参数"+ Arrays.toString(args));
                    result = method.invoke(target, args);
                    System.out.println("日志，方法：" + method.getName()+",结果"+ Arrays.toString(args));
                } catch (Exception e) {
                    e.printStackTrace();
                    System.out.println("日志，方法：" + method.getName()+",异常"+ e);
                } finally {
                    System.out.println("日志，方法：" + method.getName()+",方法执行完毕");

                }
                return result;
            }
        };
        return Proxy.newProxyInstance(classLoader,interfaces,h);
    }
}
```

2. 测试

```java
public class ProxyTest {
    @Test
    public void testProxy(){
        ProxyFactory proxyFactory = new ProxyFactory(new CalculatorImpl());
        Calculator proxy = (Calculator) proxyFactory.getProxy();
        proxy.div(1,0);
    }
}
```

#### AOP概念及相关术语

##### 概述

AOP（Aspect Oriented Programming）是一种设计思想，是软件设计领域中的面向切面编程，它是面向对象编程的一种补充和完善，它以通过预编译方式和运行期动态代理方式实现在不修改源代码的情况下给程序动态统一添加额外功能的一种技术。

##### 相关术语

1. 横切关注点
   从每个方法中抽取出来的同一类非核心业务。在同一个项目中，我们可以使用多个横切关注点对相关方法进行多个不同方面的增强。
   这个概念不是语法层面天然存在的，而是根据附加功能的逻辑上的需要：有十个附加功能，就有十个横切关注点。
2. 通知
   每一个横切关注点上要做的事情都需要写一个方法来实现，这样的方法就叫通知方法。
   - 前置通知：在被代理的目标方法**前**执行
   - 返回通知：在被代理的目标方法**成功结束**后执行（寿终正寝）
   - 异常通知：在被代理的目标方法**异常结束**后执行（死于非命）
   - 后置通知：在被代理的目标方法**最终结束**后执行（盖棺定论）
   - 环绕通知：使用`try...catch...finally`结构围绕**整个**被代理的目标方法，包括上面四种通知对应的所有位置
3. 切面
   封装通知方法的类。
4. 目标
   被代理的目标对象。
5. 代理
   向目标对象应用通知之后创建的代理对象。
6. 连接点
   这也是一个纯逻辑概念，不是语法定义的。把方法排成一排，每一个横切位置看成x轴方向，把方法从上到下执行的顺序看成y轴，x轴和y轴的交叉点就是连接点。
7. 切入点
   定位连接点的方式。每个类的方法中都包含多个连接点，所以连接点是类中客观存在的事物（从逻辑上来说）。如果把连接点看作数据库中的记录，那么切入点就是查询记录的 SQL 语句。Spring 的 AOP 技术可以通过切入点定位到特定的连接点。切点通过`org.springframework.aop.Pointcut`接口进行描述，它使用类和方法作为连接点的查询条件。

##### 作用

- 简化代码：把方法中固定位置的重复的代码抽取出来，让被抽取的方法更专注于自己的核心功能，提高内聚性。
- 代码增强：把特定的功能封装到切面类中，看哪里有需要，就往上套，被套用了切面逻辑的方法就被切面给增强了。

#### 基于注解的AOP

##### 技术说明

1. 动态代理（InvocationHandler）：JDK原生的实现方式，需要被代理的目标类必须实现接口。因为这个技术要求代理对象和目标对象实现同样的接口（兄弟两个拜把子模式）。
2. cglib：通过继承被代理的目标类（认干爹模式）实现代理，所以不需要目标类实现接口。
3. AspectJ：本质上是静态代理，将代理逻辑“织入”被代理的目标类编译得到的字节码文件，所以最终效果是动态的。weaver就是织入器。Spring只是借用了AspectJ中的注解。

##### 准备工作

1. 添加依赖
   在IOC所需依赖基础上再加入下面依赖即可

```xml
    <!-- spring-aspects会帮我们传递过来aspectjweaver -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-aspects</artifactId>
        <version>5.3.1</version>
    </dependency>
```

2. 准备被代理的目标资源

接口：

```java
public interface Calculator {
    int add(int i, int j);
    int sub(int i, int j);
    int mul(int i, int j);
    int div(int i, int j);
}
```

实现类：

```java
public class CalculatorImpl implements Calculator{
    @Override
    public int add(int i, int j) {

        int result = i + j;
        System.out.println("方法内部，result:" + result);

        return result;
    }

    @Override
    public int sub(int i, int j) {

        int result = i - j;
        System.out.println("方法内部，result:" + result);

        return result;
    }

    @Override
    public int mul(int i, int j) {

        int result = i * j;
        System.out.println("方法内部，result:" + result);

        return result;
    }

    @Override
    public int div(int i, int j) {

        int result = i / j;
        System.out.println("方法内部，result:" + result);

        return result;
    }
}
```

3. 配置Spring的配置文件
   AOP的注意事项
   - 切面类和目标类都需要交给IOC容器管理
   - 切面类必须通过@Aspect注解标识为一个切面
   - 在Spring的配置文件中设置`<aop:aspectj-autoproxy/>`开启基于注解的AOP

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd
       http://www.springframework.org/schema/context
       https://www.springframework.org/schema/context/spring-context.xsd
       http://www.springframework.org/schema/aop
       https://www.springframework.org/schema/aop/spring-aop.xsd">
    <context:component-scan base-package="com.tl.spring.aop.annotation">
    </context:component-scan>
<!--    开启基于注解的AOP-->
    <aop:aspectj-autoproxy/>
</beans>
```

##### 创建切面类并配置

`@Aspect`表示这个类是一个切面类
`@Component`注解保证这个切面类能够被IOC容器所管理

```java
@Aspect
@Component
public class LogAspect {
    @Before("execution(public int com.atguigu.aop.annotation.CalculatorImpl.*(..))")
public void beforeMethod(JoinPoint joinPoint){
 String methodName = joinPoint.getSignature().getName();
 String args = Arrays.toString(joinPoint.getArgs());
 System.out.println("Logger-->前置通知，方法名："+methodName+"，参数："+args);
 }
    @After("execution(* com.atguigu.aop.annotation.CalculatorImpl.*(..))")
 public void afterMethod(JoinPoint joinPoint){
  String methodName = joinPoint.getSignature().getName();
  System.out.println("Logger-->后置通知，方法名："+methodName);
 }
    @AfterReturning(value = "execution(*com.atguigu.aop.annotation.CalculatorImpl.*(..))", returning = "result")
 public void afterReturningMethod(JoinPoint joinPoint, Object result){
  String methodName = joinPoint.getSignature().getName();
  System.out.println("Logger-->返回通知，方法名："+methodName+"，结果："+result);
 }
    @AfterThrowing(value = "execution(*com.atguigu.aop.annotation.CalculatorImpl.*(..))", throwing = "ex")
 public void afterThrowingMethod(JoinPoint joinPoint, Throwable ex){
  String methodName = joinPoint.getSignature().getName();
  System.out.println("Logger-->异常通知，方法名："+methodName+"，异常："+ex);
 }
    @Around("execution(* com.atguigu.aop.annotation.CalculatorImpl.*(..))")
 public Object aroundMethod(ProceedingJoinPoint joinPoint){
        String methodName = joinPoint.getSignature().getName();
  String args = Arrays.toString(joinPoint.getArgs());
  Object result = null;
        try {
            System.out.println("环绕通知-->目标对象方法执行之前");
            //目标对象（连接点）方法的执行
            result = joinPoint.proceed();
            System.out.println("环绕通知-->目标对象方法返回值之后");
  } catch (Throwable throwable) {
            throwable.printStackTrace();
            System.out.println("环绕通知-->目标对象方法出现异常时");
  } finally {
   System.out.println("环绕通知-->目标对象方法执行完毕");
  }
  return result;
 }
}
```

##### 各种通知

- 前置通知：使用`@Before`注解标识，在被代理的目标方法前执行
- 返回通知：使用`@AfterReturning`注解标识，在被代理的目标方法成功结束后执行（寿终正寝）
- 异常通知：使用`@AfterThrowing`注解标识，在被代理的目标方法异常结束后执行（死于非命）
- 后置通知：使用`@After`注解标识，在被代理的目标方法最终结束后执行（盖棺定论）
- 环绕通知：使用`@Around`注解标识，使用`try...catch...finally`结构围绕整个被代理的目标方法，包括上面四种通知对应的所有位置

各种通知的执行顺序：

- Spring版本5.3.x以前：□前置通知→□目标操作→□后置通知→□返回通知或异常通知
- Spring版本5.3.x以后：■前置通知→■目标操作→■返回通知或异常通知→■后置通知（本笔记所用的版本）

##### 切入点表达式语法

- 用`*`号代替“权限修饰符”和“返回值”部分，表示“权限修饰符”和“返回值”不限
- 在包名的部分，一个“`.`”号只能代表包的层次结构中的一层，表示这一层是任意的。
  例如：`.Hello`匹配`com.Hello`，不匹配`com.tl.Hello`
- 在包名的部分，使用“`..`”表示包名任意、包的层次深度任意
- 在类名的部分，类名部分整体用`*`号代替，表示类名任意
- 在类名的部分，可以使用`.`号代替类名的一部分
  例如：`*Service`匹配所有名称以`Service`结尾的类或接口
- 在方法名部分，可以使用`*`号表示方法名任意
- 在方法名部分，可以使用`*`号代替方法名的一部分
  例如：`*Operation`匹配所有方法名以`Operation`结尾的方法
- ​在方法参数列表部分，使用`(..)`表示参数列表任意
- 在方法参数列表部分，使用`(int,..)`表示参数列表以一个int类型的参数开头
- 在方法参数列表部分，基本数据类型和对应的包装类型是不一样的
  切入点表达式中使用 int 和实际方法中 Integer 是不匹配的
- 在方法返回值部分，如果想要明确指定一个返回值类型，那么必须同时写明权限修饰符
  例如：`execution(public int ..Service.(.., int))` <font color="green">正确</font>
  例如：`execution( int *..Service.(.., int))`      <font color="red">错误</font>

##### 重用切入点表达式

1. 声明
   
   ```java
   @Pointcut("execution(* com.tl.aop.annotation.*.*(..))")
    public void pointCut(){}
   ```

2. 在同一个切面中使用
   
   ```java
   @Before("pointCut()")
   public void beforeMethod(JoinPoint joinPoint){
   String methodName = joinPoint.getSignature().getName();
   String args = Arrays.toString(joinPoint.getArgs());
   System.out.println("Logger-->前置通知，方法名："+methodName+"，参数："+args);
   }
   ```

3. 在不同切面中使用
   
   ```java
   @Before("com.tl.aop.CommonPointCut.pointCut()")
   public void beforeMethod(JoinPoint joinPoint){
   String methodName = joinPoint.getSignature().getName();
   String args = Arrays.toString(joinPoint.getArgs());
   System.out.println("Logger-->前置通知，方法名："+methodName+"，参数："+args);
   }
   ```

##### 获取通知的相关信息

1. 获取连接点信息
   获取连接点信息可以在通知方法的参数位置设置`JoinPoint`类型的形参
   
   ```java
   @Before("pointCut()")
   public void beforeAdviceMethod(JoinPoint joinPoint){
        //获取连接点所对应方法的签名信息
        Signature signature = joinPoint.getSignature();
        //获取连接点所对应方法的参数
        Object[] args = joinPoint.getArgs();
        System.out.println("LoggerAspect，方法："+signature.getName()+","+ Arrays.toString(args));
    }
   ```

2. 获取目标方法的返回值
    在返回通知中若要获取目标对象方法的返回值，只需要通过`@AfterReturning`注解的`returning`属性，就可以将通知方法的某个参数指定为接收目标对象方法的返回值的参数
   
   ```java
    @AfterReturning(value = "pointCut()",returning = "result")
    public void afterReturningAdviceMethod(JoinPoint joinPoint,Object result){
        //获取连接点所对应方法的签名信息
        Signature signature = joinPoint.getSignature();
        System.out.println("LoggerAspect，方法："+signature.getName()+"，结果" + result);
   
    }
   ```

3. 获取目标方法的异常
    在返回通知中若要获取目标对象方法的异常，只需要通过`@AfterReturning`注解的`returning`属性，就可以将通知方法的某个参数指定为接收目标对象方法的异常的参数
   
   ```java
   @AfterThrowing(value = "execution(* com.tl.aop.annotation.CalculatorImpl.*(..))", throwing = "ex")
    public void afterThrowingMethod(JoinPoint joinPoint, Throwable ex){
    String methodName = joinPoint.getSignature().getName();
    System.out.println("Logger-->异常通知，方法名："+methodName+"，异常："+ ex);
    }
   ```

##### 环绕通知

```java
    @Around("pointCut()")
    //环绕通知的方法的返回值一定要和目标对象方法的返回值一致
    public Object aroundAdviceMethod(ProceedingJoinPoint joinPoint){
        Object result = null;
        try {
            System.out.println("环绕通知-->前置通知");
            //表示目标对象方法的执行
            result = joinPoint.proceed();
            System.out.println("环绕通知-->返回通知");

        } catch (Throwable throwable) {
            throwable.printStackTrace();
            System.out.println("环绕通知-->异常通知");

        }finally {
            System.out.println("环绕通知-->后置通知");

        }
        return result;
    }
```

##### 切面的优先级

- 相同目标方法上同时存在多个切面时，切面的优先级控制切面的**内外嵌套**顺序。优先级高的切面：外面；优先级低的切面：里面
- 使用`@Order`注解可以控制切面的优先级：`@Order(较小的数)`：优先级高；`@Order(较大的数)`：优先级低

#### 基于XML的AOP（了解）

##### 准备工作（参考基于注解的AOP环境）

##### 实现

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd http://www.springframework.org/schema/aop https://www.springframework.org/schema/aop/spring-aop.xsd">

<!--    扫描组件-->
    <context:component-scan base-package="com.tl.spring.aop.xml"/>

    <aop:config>
<!--        将IOC容器中某个bean设置为切面-->
        <aop:aspect ref="loggerAspect">
            <!--设置一个公共的切入点表达式-->
            <aop:pointcut id="pointCut" expression="execution(* com.tl.spring.aop.xml.CalculatorImpl.*(..))"/>
            <aop:before method="beforeAdviceMethod" pointcut-ref="pointCut"/>
            <aop:after method="afterAdviceMethod" pointcut-ref="pointCut"/>
            <aop:after-returning method="afterReturningAdviceMethod" returning="result" pointcut-ref="pointCut"/>
            <aop:after-throwing method="afterThrowingAdviceMethod" throwing="ex" pointcut-ref="pointCut"/>
            <aop:around method="aroundAdviceMethod" pointcut-ref="pointCut"/>
        </aop:aspect>
        <aop:aspect ref="validateAspect" order="1">
            <aop:before method="beforeMethod" pointcut-ref="pointCut"/>
        </aop:aspect>
    </aop:config>
</beans>
```

### 声明式事务

#### JDBCTemplate

##### 简介

Spring框架对JDBC进行封装，使用JDBCTemplate方便实现对数据库操作

##### 准备工作

1. 加入依赖

```xml
<dependencies>
    <!-- 基于Maven依赖传递性，导入spring-context依赖即可导入当前所需所有jar包 -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context</artifactId>
        <version>5.3.1</version>
    </dependency>
    <!-- Spring 持久化层支持jar包 -->
    <!-- Spring 在执行持久化层操作、与持久化层技术进行整合过程中，需要使用orm、jdbc、tx三个jar包 -->
    <!-- 导入 orm 包就可以通过 Maven 的依赖传递性把其他两个也导入 -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-orm</artifactId>
        <version>5.3.1</version>
    </dependency>
    <!-- Spring 测试相关 -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-test</artifactId>
        <version>5.3.1</version>
    </dependency>
    <!-- junit测试 -->
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.12</version>
        <scope>test</scope>
    </dependency>
    <!-- MySQL驱动 -->
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>8.0.16</version>
    </dependency>
    <!-- 数据源 -->
    <dependency>
        <groupId>com.alibaba</groupId>
        <artifactId>druid</artifactId>
        <version>1.0.31</version>
    </dependency>
</dependencies>
```

2. 创建java.properties

```properties
    jdbc.driver=com.mysql.cj.jdbc.Driver
    jdbc.url=jdbc:mysql://localhost:3306/ssm?serverTimezone=UTC
    jdbc.username=root
    jdbc.password=root
```

3. 配置Spring的配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd">

    <!--导入外部属性文件-->
    <context:property-placeholder location="classpath:jdbc.properties"></context:property-placeholder>

    <!--配置数据源-->
    <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">
        <property name="driverClassName" value="${jdbc.driver}"></property>
        <property name="url" value="${jdbc.url}"></property>
        <property name="username" value="${jdbc.username}"></property>
        <property name="password" value="${jdbc.password}"></property>
    </bean>
    <!--配置JDBCTemplate-->
    <bean class="org.springframework.jdbc.core.JdbcTemplate">
    <!-- 装配数据源 -->
        <property name="dataSource" ref="dataSource"></property>
    </bean>
</beans>
```

##### 测试

1. 添加一条数据（修改、删除只需要修改其中的SQL语句即可）

`@RunWith`注解：指定当前测试类在Spring的测试环境中执行，此时就可以通过注入的方式直接获取IOC容器中的bean
`@ContextConfiguration`注解：设置Spring测试环境的配置文件

```java
@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration("classpath:spring-jdbc.xml")
public class JdbcTemplateTest {
    @Autowired
    private JdbcTemplate jdbcTemplate;
    @Test
    public void testInsert(){
        String sql = "insert into t_user values(null,?,?,?,?,?)";
        //增、删、改均是update方法
        jdbcTemplate.update(sql,"root","123",23,"女","123@qq.com");
        }
    }
```

2. 查询

```java
    @Test
    // 查询一条数据（作为实体类对象）
    public void testGetUserById(){
        String sql = "select * from t_user where id = ?";
        User user = jdbcTemplate.queryForObject(sql, new BeanPropertyRowMapper<>(User.class), 1);
        System.out.println(user);
    }

    @Test
    // 查询多条数据（作为list集合）
    public void testGetAllUser(){
        String sql = "select * from t_user";
        List<User> list = jdbcTemplate.query(sql, new BeanPropertyRowMapper<>(User.class));
        list.forEach(System.out::println);
    }

    @Test
    // 查询所有记录的条数
    public void testGetCount(){
        String sql = "select count(*) from t_user";
        Integer count = jdbcTemplate.queryForObject(sql, Integer.class);
        System.out.println(count);
    }
```

#### 声明式事务概念

##### 编程式事务

事务功能的相关操作全部通过自己编写代码来实现：

```java
    Connection conn = ...;
        try {
            // 开启事务：关闭事务的自动提交
            conn.setAutoCommit(false);
            // 核心操作
            // 提交事务
            conn.commit();
        }catch(Exception e){
            // 回滚事务
            conn.rollBack();
        }finally{
            // 释放数据库连接
            conn.close();
        }
```

编程式的实现方式存在缺陷：

- 细节没有被屏蔽：具体操作过程中，所有细节都需要程序员自己来完成，比较繁琐。
- 代码复用性不高：如果没有有效抽取出来，每次实现功能都需要自己编写代码，代码就没有得到复用。

##### 声明式事务

既然事务控制的代码有规律可循，代码的结构基本是确定的，所以框架就可以将固定模式的代码抽取出来，进行相关的封装。封装起来后，我们只需要在配置文件中进行简单的配置即可完成操作。

- 好处1：提高开发效率
- 好处2：消除了冗余的代码
- 好处3：框架会综合考虑相关领域中在实际开发环境下有可能遇到的各种问题，进行了健壮性、性能等各个方面的优化
  所以，我们可以总结下面两个概念：
- **编程式**：**自己写代码**实现功能
- **声明式**：通过**配置**让**框架**实现功能

#### 基于注解的声明式事务

##### 准备工作

1. 加入依赖

```xml
<dependencies>
    <!-- 基于Maven依赖传递性，导入spring-context依赖即可导入当前所需所有jar包 -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context</artifactId>
        <version>5.3.1</version>
    </dependency>
    <!-- Spring 持久化层支持jar包 -->
    <!-- Spring 在执行持久化层操作、与持久化层技术进行整合过程中，需要使用orm、jdbc、tx三个jar包 -->
    <!-- 导入 orm 包就可以通过 Maven 的依赖传递性把其他两个也导入 -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-orm</artifactId>
        <version>5.3.1</version>
    </dependency>
    <!-- Spring 测试相关 -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-test</artifactId>
        <version>5.3.1</version>
    </dependency>
    <!-- junit测试 -->
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.12</version>
        <scope>test</scope>
    </dependency>
    <!-- MySQL驱动 -->
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>8.0.16</version>
    </dependency>
    <!-- 数据源 -->
    <dependency>
        <groupId>com.alibaba</groupId>
        <artifactId>druid</artifactId>
        <version>1.0.31</version>
    </dependency>
</dependencies>
```

2. 创建java.properties

```properties
    jdbc.driver=com.mysql.cj.jdbc.Driver
    jdbc.url=jdbc:mysql://localhost:3306/ssm?serverTimezone=UTC
    jdbc.username=root
    jdbc.password=root
```

3. 配置Spring的配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd">

    <!--导入外部属性文件-->
    <context:property-placeholder location="classpath:jdbc.properties"></context:property-placeholder>

    <!--配置数据源-->
    <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">
        <property name="driverClassName" value="${jdbc.driver}"></property>
        <property name="url" value="${jdbc.url}"></property>
        <property name="username" value="${jdbc.username}"></property>
        <property name="password" value="${jdbc.password}"></property>
    </bean>
    <!--配置JDBCTemplate-->
    <bean class="org.springframework.jdbc.core.JdbcTemplate">
    <!-- 装配数据源 -->
        <property name="dataSource" ref="dataSource"></property>
    </bean>
</beans>
```

4. 创建表

```sql
    CREATE TABLE `t_book` (
        `book_id` int(11) NOT NULL AUTO_INCREMENT COMMENT '主键',
        `book_name` varchar(20) DEFAULT NULL COMMENT '图书名称',
        `price` int(11) DEFAULT NULL COMMENT '价格',
        `stock` int(10) unsigned DEFAULT NULL COMMENT '库存（无符号）',
        PRIMARY KEY (`book_id`)
    ) ENGINE=InnoDB AUTO_INCREMENT=3 DEFAULT CHARSET=utf8;
    insert into `t_book`(`book_id`,`book_name`,`price`,`stock`) values (1,'斗破苍穹',80,100),(2,'斗罗大陆',50,100);
    CREATE TABLE `t_user` (
        `user_id` int(11) NOT NULL AUTO_INCREMENT COMMENT '主键',
        `username` varchar(20) DEFAULT NULL COMMENT '用户名',
        `balance` int(10) unsigned DEFAULT NULL COMMENT '余额（无符号）',
        PRIMARY KEY (`user_id`)
    ) ENGINE=InnoDB AUTO_INCREMENT=2 DEFAULT CHARSET=utf8;
    insert into `t_user`(`user_id`,`username`,`balance`) values (1,'admin',50);
```

5. 创建组件

创建BookController：

```java
@Controller
public class BookController {
    @Autowired
    private BookService bookService;
    public void buyBook(Integer bookId, Integer userId){
        bookService.buyBook(bookId, userId);
    }
}
```

创建接口BookService：

```java
public interface BookService {
    /**
     * 买书
     * @param userId
     * @param bookId
     */
    void buyBook(Integer userId, Integer bookId);
}
```

创建实现类BookServiceImpl：

```java
@Service
public class BookServiceImpl implements BookService {
    @Autowired
    private BookDao bookDao;
    @Override
    public void buyBook(Integer userId, Integer bookId) {

        //查询图书的价格
        Integer price = bookDao.getPriceByBookId(bookId);
        //更新图书的库存
        bookDao.updateStock(bookId);
        //更新用户的余额
        bookDao.updateBalance(userId,price);
    }
}
```

创建接口BookDao：

```java
public interface BookDao {
    /**
     * 根据图书的ID查询图书的价格
     * @param bookId
     * @return
     */
    Integer getPriceByBookId(Integer bookId);

    /**
     * 更新图书的库存
     * @param bookId
     */
    void updateStock(Integer bookId);

    /**
     * 更新用户的余额
     * @param userId
     * @param price
     */

    void updateBalance(Integer userId, Integer price);
}
```

创建实现类BookDaoImpl：

```java
@Repository
public class BookDaoImpl implements BookDao {

    @Autowired
    private JdbcTemplate jdbcTemplate;
    @Override
    public Integer getPriceByBookId(Integer bookId) {
        String sql = "select price from t_book where book_id = ?";
        return jdbcTemplate.queryForObject(sql,Integer.class,bookId);
    }

    @Override
    public void updateStock(Integer bookId) {
        String sql = "update t_book set stock = stock - 1 where book_id= ?";
        jdbcTemplate.update(sql,bookId);

    }

    @Override
    public void updateBalance(Integer userId, Integer price) {

        String sql = "update t_user set balance = balance - ? where user_id =?";
        jdbcTemplate.update((sql,price,userId);

    }
}
```

##### 测试无事务情况

1. 创建测试类

```java
@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration("classpath:tx-annotation.xml")
public class TxByAnnotation {

    @Autowired
    private BookController bookController;

    @Test
    public void testBuyBook(){
        bookController.buyBook(1,1);
    }

}
```

2. 模拟场景

用户购买图书，先查询图书的价格，再更新图书的库存和用户的余额。假设用户id为1的用户，购买id为1的图书，用户余额为50，而图书价格为80，购买图书之后，用户的余额为-30，数据库中余额字段设置了无符号，因此无法将-30插入到余额字段。此时执行sql语句会抛SQLException

3. 观察结果

因为没有添加事务，图书的库存更新了，但是用户的余额没有更新。显然这样的结果是错误的，购买图书是一个完整的功能，更新库存和更新余额要么都成功要么都失败

![t_user表](2022-12-28-15-20-31.png)**用户的余额没有成功减少**
![t_bbok表](2022-12-28-15-19-52.png)**书的库存成功减少，但违反了事务的一致性**

##### 加入事务

1. 配置事务管理器

```xml
    <bean id = "transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
        <property name="dataSource" ref="dataSource"></property>
    </bean>
```

2. 开启事务的注解驱动
   将使用`@Transactional`注解所标识的方法或类中所有的方法使用事务进行管理`transaction-manager`属性设置事务管理器的id，若事务管理器的bean的id默认为`transactionManager`，则该属性可以不写

```xml
    <tx:annotation-driven transaction-manager="transactionManager"/>
```

**注意，选择tx为结尾的**
![事务的注解驱动](2022-12-28-15-45-58.png)

3. 添加注解
   因为service层表示业务逻辑层，一个方法表示一个完成的功能，因此处理事务一般在service层处理。在`BookServiceImpl`的`buybook()`方法上添加注解`@Transactional`

```java
@Service
public class BookServiceImpl implements BookService {
    @Autowired
    private BookDao bookDao;
    @Transactional
    @Override
    public void buyBook(Integer userId, Integer bookId) {

        //查询图书的价格
        Integer price = bookDao.getPriceByBookId(bookId);
        //更新图书的库存
        bookDao.updateStock(bookId);
        //更新用户的余额
        bookDao.updateBalance(userId,price);
    }
}
```

##### @Transactional注解标识的位置

- @Transactional标识在方法上，则只会影响该方法
- @Transactional标识的类上，则会影响类中所有的方法

##### 事务属性：只读

1. 介绍
   对一个查询操作来说，如果我们把它设置成只读，就能够明确告诉数据库，这个操作不涉及写操作。这样数据库就能够针对查询操作来进行优化。

```java
@Transactional(readOnly = true)
public void buyBook(Integer bookId, Integer userId) {
    //查询图书的价格
    Integer price = bookDao.getPriceByBookId(bookId);
    //更新图书的库存
    bookDao.updateStock(bookId);
    //更新用户的余额
    bookDao.updateBalance(userId, price);
    //System.out.println(1/0);
}
```

2. 注意：对增删改操作设置只读会抛出下面异常：`java.sql.SQLException`

##### 事务属性：超时

1. 介绍

事务在执行过程中，有可能因为遇到某些问题，导致程序卡住，从而长时间占用数据库资源。而长时间占用资源，大概率是因为程序运行出现了问题（可能是Java程序或MySQL数据库或网络连接等等）。此时这个很可能出问题的程序应该被回滚，撤销它已做的操作，事务结束，把资源让出来，让其他正常程序可以执行。*概括来说就是一句话：超时回滚，释放资源。*

2. 使用方式

```java
@Transactional(timeout = 3)
public void buyBook(Integer bookId, Integer userId) {
    try {
        TimeUnit.SECONDS.sleep(5);
    } catch (InterruptedException e) {
        e.printStackTrace();
    }
    //查询图书的价格
    Integer price = bookDao.getPriceByBookId(bookId);
    //更新图书的库存
    bookDao.updateStock(bookId);
    //更新用户的余额
    bookDao.updateBalance(userId, price);
    //System.out.println(1/0);
}
```

3. 观察结果

执行过程中抛出异常：`TransactionTimedOutException`

##### 事务属性：回滚策略

1. 介绍

声明式事务默认只针对运行时异常回滚，编译时异常不回滚。可以通过`@Transactional`中相关属性设置回滚策略

- rollbackFor属性：需要设置一个Class类型的对象

- rollbackForClassName属性：需要设置一个字符串类型的全类名

- noRollbackFor属性：需要设置一个Class类型的对象

- rollbackFor属性：需要设置一个字符串类型的全类名
2. 使用

```java
@Transactional(noRollbackFor = ArithmeticException.class)
//@Transactional(noRollbackForClassName = "java.lang.ArithmeticException")
public void buyBook(Integer bookId, Integer userId) {
    //查询图书的价格
    Integer price = bookDao.getPriceByBookId(bookId);
    //更新图书的库存
    bookDao.updateStock(bookId);
    //更新用户的余额
    bookDao.updateBalance(userId, price);
    System.out.println(1/0);
}
```

3. 观察结果

虽然购买图书功能中出现了数学运算异常（ArithmeticException），但是我们设置的回滚策略是——当出现ArithmeticException不发生回滚。因此购买图书的操作正常执行

##### 事务属性：事务隔离级别

1. 介绍

数据库系统必须具有隔离并发运行各个事务的能力，使它们不会相互影响，避免各种并发问题。一个事务与其他事务隔离的程度称为隔离级别。SQL标准中规定了多种事务隔离级别，不同隔离级别对应不同的干扰程度，隔离级别越高，数据一致性就越好，但并发性越弱。

隔离级别一共有四种：

- 读未提交：READ UNCOMMITTED
  允许Transaction01读取Transaction02未提交的修改。
- 读已提交：READ COMMITTED、
  要求Transaction01只能读取Transaction02已提交的修改。
- 可重复读：REPEATABLE READ
  确保Transaction01可以多次从一个字段中读取到相同的值，即Transaction01执行期间禁止其它事务对这个字段进行更新。
- 串行化：SERIALIZABLE
  确保Transaction01可以多次从一个表中读取到相同的行，在Transaction01执行期间，禁止其它事务对这个表进行添加、更新、删除操作。可以避免任何并发问题，但性能十分低下。

各个隔离级别解决并发问题的能力见下表：

| 隔离级别             | 脏读  | 不可重复读 | 幻读  |
| ---------------- | --- | ----- | --- |
| READ UNCOMMITTED | 有   | 有     | 有   |
| READ COMMITTED   | 无   | 有     | 有   |
| REPEATABLE READ  | 无   | 有     | 有   |
| SERIALIZABLE     | 无   | 有     | 无   |

各种数据库产品对事务隔离级别的支持程度：

| 隔离级别             | Oracle | MySQL |
| ---------------- | ------ | ----- |
| READ UNCOMMITTED | ×      | √     |
| READ COMMITTED   | √（默认）  | √     |
| REPEATABLE READ  | ×      | √（默认） |
| SERIALIZABLE     | √      | √     |

2. 使用方式

```java
    @Transactional(isolation = Isolation.DEFAULT) //使用数据库默认的隔离级别
    @Transactional(isolation = Isolation.READ_UNCOMMITTED) //读未提交
    @Transactional(isolation = Isolation.READ_COMMITTED) //读已提交
    @Transactional(isolation = Isolation.REPEATABLE_READ) //可重复读
    @Transactional(isolation = Isolation.SERIALIZABLE) //串行化
```

##### 事务属性：事务传播行为

1. 介绍
   当事务方法被另一个事务方法调用时，必须指定事务应该如何传播。例如：方法可能继续在现有事务中运行，也可能开启一个新事务，并在自己的事务中运行。

2. 测试
- 创建接口CheckoutService：

```java
public interface CheckoutService {
    void checkout(Integer[] bookIds, Integer userId);
}
```

- 创建实现类CheckoutServiceImpl：

```java
@Service
public class CheckoutServiceImpl implements CheckoutService {
    @Autowired
    private BookService bookService;
    @Override
    @Transactional
    //一次购买多本图书
    public void checkout(Integer[] bookIds, Integer userId) {
        for (Integer bookId : bookIds) {
            bookService.buyBook(bookId, userId);
        }
    }
}
```

- 在BookController中添加方法：

```java
@Autowired
private CheckoutService checkoutService;
public void checkout(Integer[] bookIds, Integer userId){
    checkoutService.checkout(bookIds, userId);
}
```

3. 观察结果

可以通过`@Transactional`中的`propagation`属性设置事务传播行为
修改BookServiceImpl中buyBook()上，注解`@Transactional`的`propagation`属性`@Transactional(propagation = Propagation.REQUIRED)`，默认情况，表示如果当前线程上有已经开启的事务可用，那么就在这个事务中运行。经过观察，购买图书的方法`buyBook()`在`checkout()`中被调用，`checkout()`上有事务注解，因此在此事务中执行。所购买的两本图书的价格为80和50，而用户的余额为100，因此在购买第二本图书时余额不足失败，导致整个`checkout()`回滚，即只要有一本书买不了，就都买不了；
`@Transactional(propagation = Propagation.REQUIRES_NEW)`，表示不管当前线程上是否有已经开启的事务，都要开启新事务。同样的场景，每次购买图书都是在`buyBook()`的事务中执行，因此第一本图书购买成功，事务结束，第二本图书购买失败，只在第二次的`buyBook()`中回滚，购买第一本图书不受影响，即能买几本就买几本。

#### 基于XML的声明式事务

##### 场景模拟（参考基于注解的声明式事务）

##### 修改Spring配置文件

将Spring配置文件中去掉tx:annotation-driven 标签，并添加配置：

```xml
<aop:config>
    <!-- 配置事务通知和切入点表达式 -->
    <aop:advisor advice-ref="txAdvice" pointcut="execution(*com.atguigu.spring.tx.xml.service.impl.*.*(..))"></aop:advisor>
</aop:config>
<!-- tx:advice标签：配置事务通知 -->
<!-- id属性：给事务通知标签设置唯一标识，便于引用 -->
<!-- transaction-manager属性：关联事务管理器 -->
<tx:advice id="txAdvice" transaction-manager="transactionManager">
    <tx:attributes>
        <!-- tx:method标签：配置具体的事务方法 -->
        <!-- name属性：指定方法名，可以使用星号代表多个字符 -->
        <tx:method name="get*" read-only="true"/>
        <tx:method name="query*" read-only="true"/>
        <tx:method name="find*" read-only="true"/>
        <!-- read-only属性：设置只读属性 -->
        <!-- rollback-for属性：设置回滚的异常 -->
        <!-- no-rollback-for属性：设置不回滚的异常 -->
        <!-- isolation属性：设置事务的隔离级别 -->
        <!-- timeout属性：设置事务的超时属性 -->
        <!-- propagation属性：设置事务的传播行为 -->
        <tx:method name="save*" read-only="false" rollback-for="java.lang.Exception" propagation="REQUIRES_NEW"/>
        <tx:method name="update*" read-only="false" rollback-for="java.lang.Exception" propagation="REQUIRES_NEW"/>
        <tx:method name="delete*" read-only="false" rollback-for="java.lang.Exception" propagation="REQUIRES_NEW"/>
    </tx:attributes>
</tx:advice>
```

**注意：基于xml实现的声明式事务，必须引入aspectj的依赖**

```xml
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-aspects</artifactId>
    <version>5.3.1</version>
</dependency>
```

## SpringMVC

### SpringMVC简介

#### 什么是MVC

MVC是一种软件架构的思想，将软件按照模型、视图、控制器来划分

- M：Model，模型层，指工程中的JavaBean，作用是处理数据
    JavaBean分为两类：
    一类称为实体类Bean：专门存储业务数据的，如 Student、User 等
    一类称为业务处理 Bean：指 Service 或 Dao 对象，专门用于处理业务逻辑和数据访问。

- V：View，视图层，指工程中的html或jsp等页面，作用是与用户进行交互，展示数据

- C：Controller，控制层，指工程中的servlet，作用是接收请求和响应浏览器

MVC的工作流程： 用户通过视图层发送请求到服务器，在服务器中请求被Controller接收，Controller调用相应的Model层处理请求，处理完毕将结果返回到Controller，Controller再根据请求处理的结果找到相应的View视图，渲染数据后最终响应给浏览器

#### 什么是SpringMVC

SpringMVC是Spring的一个后续产品，是Spring的一个子项目
SpringMVC 是 Spring 为表述层开发提供的一整套完备的解决方案。在表述层框架历经 Strust、WebWork、Strust2 等诸多产品的历代更迭之后，目前业界普遍选择了SpringMVC作为 Java EE 项目表述层开发的首选方案。
注：三层架构分为表述层（或表示层）、业务逻辑层、数据访问层，表述层表示前台页面和后台servlet

#### SpringMVC的特点

- Spring 家族原生产品，与 IOC 容器等基础设施无缝对接
- 基于原生的Servlet，通过了功能强大的前端控制器DispatcherServlet，对请求和响应进行统一处理
- 表述层各细分领域需要解决的问题全方位覆盖，提供全面解决方案代码清新简洁，大幅度提升开发效率
- 内部组件化程度高，可插拔式组件即插即用，想要什么功能配置相应组件即可
- 性能卓著，尤其适合现代大型、超大型互联网项目要求

### 入门案例

#### 开发环境

IDE：idea 2022.1
构建工具：Maven 3.8.6
服务器：Tomcat 9.0.52
Spring版本：5.3.1

#### 创建Maven工程

1. 添加Web模块

![项目结构](2022-12-28-21-35-52.png)
![部署描述符位置](2022-12-28-21-37-40.png)
**注意，图上显示的位置为默认位置，但这是不正确的，需要改为：\src\main\webapp（在WEB-INF前输入该内容）**
2. 将打包方式设置为war
   `<packaging>war</packaging>`
3. 引入依赖

```xml
<dependencies>
    <!-- SpringMVC -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-webmvc</artifactId>
        <version>5.3.1</version>
    </dependency>
    <!-- 日志 -->
    <dependency>
        <groupId>ch.qos.logback</groupId>
        <artifactId>logback-classic</artifactId>
        <version>1.2.3</version>
    </dependency>
    <!-- ServletAPI -->
    <dependency>
        <groupId>javax.servlet</groupId>
        <artifactId>javax.servlet-api</artifactId>
        <version>3.1.0</version>
        <scope>provided</scope>
    </dependency>
    <!-- Spring5和Thymeleaf整合包 -->
    <dependency>
        <groupId>org.thymeleaf</groupId>
        <artifactId>thymeleaf-spring5</artifactId>
        <version>3.0.12.RELEASE</version>
    </dependency>
</dependencies>
```

##### 配置web.xml

配置SpringMVC的前端控制器DispatcherServlet

1. 默认配置方式
   此配置作用下，SpringMVC的配置文件默认位于WEB-INF下，默认名称为servlet.xml，例如，以下配置所对应SpringMVC的配置文件位于WEB-INF下，文件名为springMVCservlet.xml
   `/`：匹配浏览器向服务器发送的所有请求(不包括.jsp)
   `/*`：匹配浏览器向服务器发送的所有请求(包括.jsp)

```xml
    <servlet>
        <servlet-name>SpringMVC</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>SpringMVC</servlet-name>
        <url-pattern>/</url-pattern>
    </servlet-mapping>
```

2. 扩展配置方式

```xml
<!-- 配置SpringMVC的前端控制器，对浏览器发送的请求统一进行处理 -->
<servlet>
    <servlet-name>springMVC</servlet-name>
    <servlet-class>org.springframework.web.servlet.DispatcherServlet</servletclass>
    <!-- 通过初始化参数指定SpringMVC配置文件的位置和名称 -->
    <init-param>
        <!-- contextConfigLocation为固定值 -->
        <param-name>contextConfigLocation</param-name>
        <!-- 使用classpath:表示从类路径查找配置文件，例如maven工程中的src/main/resources -->
        <param-value>classpath:springMVC.xml</param-value>
    </init-param>
    <!--
        作为框架的核心组件，在启动过程中有大量的初始化操作要做
        而这些操作放在第一次请求时才执行会严重影响访问速度
        因此需要通过此标签将启动控制DispatcherServlet的初始化时间提前到服务器启动时
    -->
    <load-on-startup>1</load-on-startup>
</servlet>
<servlet-mapping>
    <servlet-name>springMVC</servlet-name>
    <!--
        设置springMVC的核心控制器所能处理的请求的请求路径
        /所匹配的请求可以是/login或.html或.js或.css方式的请求路径
        但是/不能匹配.jsp请求路径的请求
    -->
    <url-pattern>/</url-pattern>
</servlet-mapping>
```

##### 创建请求控制器

由于前端控制器对浏览器发送的请求进行了统一的处理，但是具体的请求有不同的处理过程，因此需要创建处理具体请求的类，即请求控制器。请求控制器中每一个处理请求的方法成为控制器方法。因为SpringMVC的控制器由一个POJO（普通的Java类）担任，因此需要通过`@Controller`注解将其标识为一个控制层组件，交给Spring的IoC容器管理，此时SpringMVC才能够识别控制器的存在

```java
@Controller
public class HelloController {

}
```

##### 创建SpringMVC的配置文件

```xml
<!-- 自动扫描包 -->
<context:component-scan base-package="com.atguigu.mvc.controller"/>
<!-- 配置Thymeleaf视图解析器 -->
<bean id="viewResolver"class="org.thymeleaf.spring5.view.ThymeleafViewResolver">
    <property name="order" value="1"/>
    <property name="characterEncoding" value="UTF-8"/>
    <property name="templateEngine">
        <bean class="org.thymeleaf.spring5.SpringTemplateEngine">
            <property name="templateResolver">
                <bean
                      class="org.thymeleaf.spring5.templateresolver.SpringResourceTemplateResolver">
                    <!-- 视图前缀 -->
                    <property name="prefix" value="/WEB-INF/templates/"/>
                    <!-- 视图后缀 -->
                    <property name="suffix" value=".html"/>
                    <property name="templateMode" value="HTML5"/>
                    <property name="characterEncoding" value="UTF-8" />
                </bean>
            </property>
        </bean>
    </property>
</bean>
```

##### 测试helloworld

1. 实现对首页的访问

在请求控制器中创建处理请求的方法

```java
@RequestMapping("/")
public String index() {
    //设置逻辑视图名
    return "index";
}
```

`@RequestMapping`注解：处理请求和控制器方法之间的映射关系。`value`属性可以通过请求地址匹配请求，`/`表示的当前工程的上下文路径，它等效于`localhost:8080/springMVC/`

2. 通过超链接跳转到指定页面
- 在主页index.html中设置超链接
  
    `th:href`为Thymeleaf携带的标记，若想使用，必须加上`xmlns:th="http://www.thymeleaf.org"`
  
  ```html
  <!DOCTYPE html>
  <html lang="en" xmlns:th="http://www.thymeleaf.org">
      <head>
          <meta charset="UTF-8">
          <title>首页</title>
      </head>
      <body>
          <h1>首页</h1>
          <a th:href="@{/hello}">HelloWorld</a><br/>
      </body>
  </html>
  ```

- 在请求控制器中创建处理请求的方法
  
  ```java
  @RequestMapping("/hello")
  public String HelloWorld() {
      return "target";
  }
  ```

##### 总结

浏览器发送请求，若请求地址符合前端控制器的`url-pattern`，该请求就会被前端控制器`DispatcherServlet`处理。前端控制器会读取SpringMVC的核心配置文件，通过扫描组件找到控制器，将请求地址和控制器中`@RequestMapping`注解的`value`属性值进行匹配，若匹配成功，该注解所标识的控制器方法就是处理请求的方法。处理请求的方法需要返回一个字符串类型的视图名称，该视图名称会被视图解析器解析，加上前缀和后缀组成视图的路径，通过Thymeleaf对视图进行渲染，最终转发到视图所对应页面。

### @RequestMapping注解

#### RequestMapping注解的功能

从注解名称上我们可以看到，@RequestMapping注解的作用就是将请求和处理请求的控制器方法关联起来，建立映射关系。SpringMVC 接收到指定的请求，就会来找到在映射关系中对应的控制器方法来处理这个请求。

#### @RequestMapping注解的位置

- `@RequestMapping`标识一个类：设置映射请求的请求路径的初始信息
- `@RequestMapping`标识一个方法：设置映射请求请求路径的具体信息

```java
@Controller
@RequestMapping("/test")
public class RequestMappingController {
    //此时请求映射所映射的请求的请求路径为：/test/testRequestMapping
    @RequestMapping("/testRequestMapping")
    public String testRequestMapping(){
        return "success";
    }
}
```

#### @RequestMapping注解的value属性

- `@RequestMapping`注解的value属性通过请求的请求地址匹配请求映射
- `@RequestMapping`注解的value属性是一个字符串类型的数组，表示该请求映射能够匹配多个请求地址所对应的请求
- `@RequestMapping`注解的value属性必须设置，至少通过请求地址匹配请求映射

```html
<a th:href="@{/testRequestMapping}">测试@RequestMapping的value属性/testRequestMapping</a><br>
<a th:href="@{/test}">测试@RequestMapping的value属性/test</a><br>
```

```java
@RequestMapping(
    value = {"/testRequestMapping", "/test"}
)
public String testRequestMapping(){
    return "success";
}
```

#### @RequestMapping注解的method属性

`@RequestMapping`注解的`method`属性通过请求的请求方式（get或post）匹配请求映射
`@RequestMapping`注解的`method`属性是一个RequestMethod类型的数组，表示该请求映射能够匹配多种请求方式的请求。若当前请求的请求地址满足请求映射的value属性，但是请求方式不满足method属性，则页面报错 *405：Request method 'POST' not supported*

```html
<a th:href="@{/test}">测试@RequestMapping的value属性-->/test</a><br>
<form th:action="@{/test}" method="post">
    <input type="submit">
</form>
```

```java
@RequestMapping(
    value = {"/testRequestMapping", "/test"},
    method = {RequestMethod.GET, RequestMethod.POST}
)
public String testRequestMapping(){
    return "success";
}
```

注：

1. 对于处理指定请求方式的控制器方法，SpringMVC中提供了`@RequestMapping`的派生注解：
   - 处理get请求的映射-->`@GetMapping`
   - 处理post请求的映射-->`@PostMapping`
   - 处理put请求的映射-->`@PutMapping`
   - 处理delete请求的映射-->`@DeleteMapping`
2. 常用的请求方式有`get`，`post`，`put`，`delete`
   但是目前浏览器只支持`get`和`post`，若在form表单提交时，为method设置了其他请求方式的字符串（put或delete），则按照默认的请求方式get处理；若要发送put和delete请求，则需要通过spring提供的过滤器HiddenHttpMethodFilter，在RESTful部分会讲到

#### @RequestMapping注解的params属性（了解）

`@RequestMapping`注解的params属性通过请求的请求参数匹配请求映射。该属性是一个字符串类型的数组，可以通过四种表达式设置请求参数和请求映射的匹配关系：

- `param`：表示当前所匹配请求的请求参数必须携带param参数
- `!param`：表示当前所匹配请求的请求参数中一定不能携带param参数
- `param=value`：表示当前所匹配请求的请求参数中必须携带param参数且值必须为value
- `param!=value`：表示当前所匹配请求的请求参数中可以不携带param，若携带，一定不能是value
  若当前请求满足@RequestMapping注解的value和method属性，但是不满足params属性，此时页面会报错 *400：Parameter conditions "username, password!=123456" not met for actual request parameters: username={admin}, password={123456}*

```html
    <!-- 以下两种方式等效 -->
  <a th:href="@{/abc?username=admin}">测试@RequestMapping注解的param属性</a>
  <a th:href="@{/abc?(username='admin')}">测试@RequestMapping注解的param属性</a>
```

```java
    @RequestMapping(value = {"/hello","/abc"},
                    method = {RequestMethod.POST,RequestMethod.GET},
                    params = {"username","!password","age=20","gender!=男"},
    )
    public String hello(){
        return "success";
    }
```

#### @RequestMapping注解的headers属性（了解）

`@RequestMapping`注解的`headers`属性通过请求的请求头信息匹配请求映射。该属性是一个字符串类型的数组，可以通过四种表达式设置请求头信息和请求映射的匹配关系：

- `header`：要求请求映射所匹配的请求必须携带header请求头信息
- `!header`：要求请求映射所匹配的请求必须不能携带header请求头信息
- `header=value`：要求请求映射所匹配的请求必须携带header请求头信息且header=value
- `header!=value`：要求请求映射所匹配的请求必须携带header请求头信息且header!=value
  若当前请求满足`@RequestMapping`注解的`value`和`method`属性，但是不满足headers属性，此时页面显示404错误，即资源未找到

#### SpringMVC支持ant风格的路径

`？`：表示任意的单个字符（不包括问号本身）
`*`：表示任意的0个或多个字符（不包括`?`和`/`）
`**`：表示任意层数的任意目录
注意：在使用`**`时，只能使用`/**/xxx`的方式

#### SpringMVC支持路径中的占位符（重点）

原始方式：`/deleteUser?id=1`
rest方式：`/user/delete/1`

SpringMVC路径中的占位符常用于RESTful风格中，当请求路径中将某些数据通过路径的方式传输到服务器中，就可以在相应的@RequestMapping注解的value属性中通过占位符{xxx}表示传输的数据，再通过@PathVariable注解，将占位符所表示的数据赋值给控制器方法的形参

```html
<a th:href="@{/testRest/1/admin}">测试路径中的占位符-->/testRest</a>
```

```java
@RequestMapping("/testRest/{id}/{username}")
public String testRest(@PathVariable("id") String id, @PathVariable("username")
String username){
    System.out.println("id:"+id+",username:"+username);
    return "success";
}
//最终输出的内容为：id:1,username:admin
```

### SpringMVC获取请求参数

#### 通过ServletAPI获取

只需要在控制器方法的形参位置设置`HttpServletRequest`类型的形参，就可以在控制器方法中使用`request`对象获取请求参数

```html
<form th:action="@{/param/servletAPI}" method="post">
    用户名：<input type="text" name="username"><br>
    密码：<input type="password" name="password"><br>
    <input type="submit" value="登录" ><br>
</form>
```

```java
@RequestMapping("/testParam")
public String testParam(HttpServletRequest request){
    String username = request.getParameter("username");
    String password = request.getParameter("password");
    System.out.println("username:"+username+",password:"+password);
    return "success";
}
```

#### 通过控制器方法的形参获取请求参数

只需要在控制器方法的形参位置，设置一个形参，形参的名字和请求参数的名字一致即可

```html
    <a th:href="@{/testParam(username='admin',password=123456)}">测试获取请求参数--
>/testParam</a><br>
```

```java
@RequestMapping("/testParam")
public String testParam(String username, String password){
    System.out.println("username:"+username+",password:"+password);
    return "success";
}
```

注：

- 若请求所传输的请求参数中有多个同名的请求参数，此时可以在控制器方法的形参中设置字符串数组或者字符串类型的形参接收此请求参数
- 若使用字符串数组类型的形参，此参数的数组中包含了每一个数据
- 若使用字符串类型的形参，此参数的值为每个数据中间使用逗号拼接的结果

#### @RequestParam注解

`@RequestParam`：将请求参数和控制器方法的形参绑定
`@RequestParam`注解的三个属性：`value`、`required`、`defaultValue`

- `value`：设置和形参绑定的请求参数的名字
- `required`：设置是否必须传输value所对应的请求参数。默认值为true，表示value所对应的参数必须传输，否则页面会报错：*400 - Required String Parameter 'xxx' is not present*；若设置为false，则表示value所对应的请求参数必须传输，若未传输，则形参值为null
- `defaultValue`：设置当没有传输value所对应的请求参数时，为形参设置的默认值，此时和`required`属性值无关

```java
    @RequestMapping("/param")
    public String getParam(
            @RequestParam(value = "userName",required = false,
            defaultValue = "hello") String username,
            String password){
        System.out.println("username：" + username + ",password：" + password);
        return "success";
    }
```

```html
<form th:action="@{/param}" method="post">
    用户名：<input type="text" name="userName"><br>
    密码：<input type="password" name="password"><br>
    <input type="submit" value="登录" ><br>
</form>
```

#### @RequestHeader注解

`@RequestHeader`：将请求头信息和控制器方法的形参绑定
`@RequestHeader`注解一共有三个属性：`value`、`required`、`defaultValue`，用法同`@RequestParam`

#### @CookieValue注解

`@CookieValue`：将Cookie数据和控制器方法的形参进行绑定
`@CookieValue`注解一共有三个属性：`value`、`required`、`defaultValue`，用法同`@RequestParam`

#### 通过POJO获取请求参数

需要在控制器方法的形参位置设置实体类类型的形参，要保证实体类中的属性的属性名和请求参数有的名字一致。可以通过实体类类型的形参获取请求参数

实体类：

```java
public class User {

    private Integer id;

    private String username;

    private String password;

    public User() {
    }

    public User(Integer id, String username, String password) {
        this.id = id;
        this.username = username;
        this.password = password;
    }

    @Override
    public String toString() {
        return "User{" +
                "id=" + id +
                ", username='" + username + '\'' +
                ", password='" + password + '\'' +
                '}';
    }

    public Integer getId() {
        return id;
    }

    public void setId(Integer id) {
        this.id = id;
    }

    public String getUsername() {
        return username;
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public String getPassword() {
        return password;
    }

    public void setPassword(String password) {
        this.password = password;
    }
}
```

```html
<form th:action="@{/param/pojo}" method="post">
    用户名：<input type="text" name="username"><br>
    密码：<input type="password" name="password"><br>
    <input type="submit" value="登录" ><br>
</form>
```

控制器方法

```java
    @RequestMapping("/param/pojo")
    private String getParamByPojo(User user){
        System.out.println(user);
        return "success";

        //控制台信息：User{id=null, username='admin', password='123456'}
    }
```

#### 解决获取请求的乱码问题（method为POST）

在web.xml中配置Spring的编码过滤器CharacterEncodingFilter

```xml
<!--配置springMVC的编码过滤器-->
<filter>
    <filter-name>CharacterEncodingFilter</filter-name>
    <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
    <init-param>
        <param-name>encoding</param-name>
        <param-value>UTF-8</param-value>
    </init-param>
    <init-param>
        <param-name>forceEncoding</param-name>
        <param-value>true</param-value>
    </init-param>
</filter>
<filter-mapping>
    <filter-name>CharacterEncodingFilter</filter-name>
    <url-pattern>/*</url-pattern>
</filter-mapping>
```

注：
①SpringMVC中处理编码的过滤器一定要配置到其他过滤器之前，否则无效
②若乱码问题依旧存在，则需要单击编辑配置（Edit Configuration），在虚拟机选项（Tomcat VM option）中设置参数：`-Dfile.encoding=utf-8`
![菜单位置](2023-01-05-11-00-46.png)
![运行/调试位置](2023-01-05-11-10-42.png)

### 域对象共享数据

#### 使用ServletAPI向request域对象共享数据

```java
@RequestMapping("/testServletAPI")
public String testServletAPI(HttpServletRequest request){
    request.setAttribute("testScope", "hello,servletAPI");
    return "success";
}
```

#### 使用ModelAndView向request域对象共享数据

使用ModelAndView时，可以使用其Model功能向请求域共享数据，使用View功能设置逻辑视图，但是控制器方法一定要将ModelAndView作为方法的返回值

```java
    ModelAndView mav = new ModelAndView();
        //向请求域中共享数据
        mav.addObject("testRequestScope","hello,ModelAndView");
        //设置逻辑视图
        mav.setViewName("success");
        return mav;
    }
```

#### 使用Model向request域对象共享数据

```java
    @RequestMapping("/test/model")
    public String testModel(Model model){
        System.out.println(model.getClass().getName());
        model.addAttribute("testRequestScope","hello.Model");
        return "success";
    }
```

#### 使用map向request域对象共享数据

```java
    @RequestMapping("/test/map")
    public String testModelMap(Map<String, Object> map){
        System.out.println(map.getClass().getName());
        map.put("testRequestScope","hello,map");
        return "success";
    }
```

#### 使用ModelMap向request域对象共享数据

```java
    @RequestMapping("/test/modelMap")
    public String testModelMap(ModelMap modelMap){
        System.out.println(modelMap.getClass().getName());
        modelMap.addAttribute("testRequestScope","hello.ModelMap");
        return "success";
    }
```

#### Model、ModelMap、Map的关系

其实在底层中，这些类型的形参最终都是通过`BindingAwareModelMap`创建

关系：
`public class BindingAwareModelMap extends ExtendedModelMap {}`
`public class ExtendedModelMap extends ModelMap implements Model {}`
`public class ModelMap extends LinkedHashMap<String, Object> {}`
![BindingAwareModelMap的图](2023-01-05-13-08-43.png)

#### 向session域共享数据

```java
@RequestMapping("/testSession")
public String testSession(HttpSession session){
    session.setAttribute("testSessionScope", "hello,session");
    return "success";
}
```

#### 向application域共享数据

```java
@RequestMapping("/testApplication")
public String testApplication(HttpSession session){
    ServletContext application = session.getServletContext();
    application.setAttribute("testApplicationScope", "hello,application");
    return "success";
}
```

### SpringMVC的视图

SpringMVC中的视图是View接口，视图的作用渲染数据，将模型Model中的数据展示给用户。SpringMVC视图的种类很多，默认有转发视图和重定向视图。当工程引入jstl的依赖，转发视图会自动转换为JstlView；若使用的视图技术为Thymeleaf，在SpringMVC的配置文件中配置了Thymeleaf的视图解析器，由此视图解析器解析之后所得到的是ThymeleafView

#### ThymeleafView

当控制器方法中所设置的视图名称没有任何前缀时，此时的视图名称会被SpringMVC配置文件中所配置的视图解析器解析，视图名称拼接视图前缀和视图。后缀所得到的最终路径，会通过转发的方式实现跳转

```java
@RequestMapping("/testHello")
public String testHello(){
    return "hello";
}
```

#### 转发视图

SpringMVC中默认的转发视图是InternalResourceView
SpringMVC中创建转发视图的情况：当控制器方法中所设置的视图名称以"forward:"为前缀时，创建InternalResourceView视图，此时的视图名称不会被SpringMVC配置文件中所配置的视图解析器解析，而是会将前缀"forward:"去掉，剩余部分作为最终路径通过转发的方式实现跳转。例如`forward:/`，`forward:/employee`

```java
@RequestMapping("/testForward")
public String testForward(){
 return "forward:/testHello";
}
```

#### 重定向视图

SpringMVC中默认的重定向视图是RedirectView
当控制器方法中所设置的视图名称以"redirect:"为前缀时，创建RedirectView视图，此时的视图名称不会被SpringMVC配置文件中所配置的视图解析器解析，而是会将前缀"redirect:"去掉，剩余部分作为最终路径通过重定向的方式实现跳转

例如`redirect:/`，`redirect:/employee`

```java
@RequestMapping("/testRedirect")
public String testRedirect(){
 return "redirect:/testHello";
}
```

#### 视图控制器：view-controller

视图控制器：为当前的请求直接设置页面名称实现页面跳转

```xml
    <!--
        path：设置处理的请求地址
        view-name：设置请求地址所对应的视图名称
    -->
    <mvc:view-controller path="/" view-name="index"/>
```

若设置视图控制器，则只有视图控制器所设置的请求会被处理，其他的请求将全部404
此时必须再配置一个标签：`<mvc:annotation-driven />`

### RESTful

#### RESTful简介

REST：Representational State Transfer，表现层资源状态转移。

##### 资源

资源是一种看待服务器的方式，即，将服务器看作是由很多离散的资源组成。每个资源是服务器上一个可命名的抽象概念。因为资源是一个抽象的概念，所以它不仅仅能代表服务器文件系统中的一个文件、数据库中的一张表等等具体的东西，可以将资源设计的要多抽象有多抽象，只要想象力允许而且客户端应用开发者能够理解。与面向对象设计类似，资源是以名词为核心来组织的，首先关注的是名词。一个资源可以由一个或多个URI来标识。URI既是资源的名称，也是资源在Web上的地址。对某个资源感兴趣的客户端应用，可以通过资源的URI与其进行交互。

##### 资源的表述

资源的表述是一段对于资源在某个特定时刻的状态的描述。可以在客户端-服务器端之间转移（交换）。资源的表述可以有多种格式，例如HTML/XML/JSON/纯文本/图片/视频/音频等等。资源的表述格式可以通过协商机制来确定。请求-响应方向的表述通常使用不同的格式。

##### 状态转移

状态转移说的是：在客户端和服务器端之间转移（transfer）代表资源状态的表述。通过转移和操作资源的表述，来间接实现操作资源的目的。

#### RESTful的实现

具体说，就是 HTTP 协议里面，四个表示操作方式的动词：GET、POST、PUT、DELETE。
它们分别对应四种基本操作：GET 用来获取资源，POST 用来新建资源，PUT 用来更新资源，DELETE用来删除资源。REST 风格提倡 URL 地址使用统一的风格设计，从前到后各个单词使用斜杠分开，不使用问号键值对方式携带请求参数，而是将要发送给服务器的数据作为 URL 地址的一部分，以保证整体风格的一致性。

| 操作   | 传统方式             | REST风格              |
| ---- | ---------------- | ------------------- |
| 查询操作 | getUserById?id=1 | user/1-->get请求方式    |
| 保存操作 | saveUser         | user-->post请求方式     |
| 删除操作 | deleteUser?id=1  | user/1-->delete请求方式 |
| 更新操作 | updateUser       | user-->put请求方式      |

#### HiddenHttpMethodFilter

注意：浏览器目前只能发送get和post请求

若要发送put和delete请求，需要在web.xml中配置一个过滤器`HiddenHttpMethodFilter`

```xml
    <filter>
        <filter-name>HiddenHttpMethodFilter</filter-name>
        <filter-class>org.springframework.web.filter.HiddenHttpMethodFilter</filter-class>
    </filter>
    <filter-mapping>
        <filter-name>HiddenHttpMethodFilter</filter-name>
        <url-pattern>/*</url-pattern>
    </filter-mapping>
```

注：

目前为止，SpringMVC中提供了两个过滤器：`CharacterEncodingFilter`和`HiddenHttpMethodFilter`。在web.xml中注册时，必须先注册`CharacterEncodingFilter`，再注册`HiddenHttpMethodFilter`
原因：在 `CharacterEncodingFilter` 中通过 `request.setCharacterEncoding(encoding)` 方法设置字符集时，`request.setCharacterEncoding(encoding)`方法要求前面不能有任何获取请求参数的操作而`HiddenHttpMethodFilter`恰恰有一个获取请求方式的操作：`String paramValue = request.getParameter(this.methodParam);`

配置了过滤器之后，发送的请求要满足两个条件，才能将请求方式转换为put或delete

- 当前请求的请求方式必须为post

```html
<form th:action="@{/user}" method="post">
    <!-- 第一个<input>的作用是为了引出请求参数，而将其类型设置为hidden是因为这个字段只是为了将请求方式进行转换，对于用户来说并没有实际作用 -->
    <input type="hidden" name="_method" value="put">
    <input type="submit" value="修改用户信息">
</form>
<form th:action="@{/user/5}" method="post">
    <input type="hidden" name="_method" value="delete">
    <input type="submit" value="删除用户信息">
</form>
```

- 当前请求必须传输请求参数`_method`，`_method`的值才是最终请求的方式

### RESTful案例

#### 准备工作

1. 实体类Employee

```java
public class Employee {
    private Integer id;
    private String lastName;
    private String email;
    //1 male, 0 female
    private Integer gender;
    public Integer getId() {
        return id;
    }
    public void setId(Integer id) {
        this.id = id;
    }
    public String getLastName() {
        return lastName;
    }
    public void setLastName(String lastName) {
        this.lastName = lastName;
    }
    public String getEmail() {
        return email;
    }
    public void setEmail(String email) {
        this.email = email;
    }
    public Integer getGender() {
        return gender;
    }
    public void setGender(Integer gender) {
        this.gender = gender;
    }
    public Employee(Integer id, String lastName, String email, Integer gender) {
        super();
        this.id = id;
        this.lastName = lastName;
        this.email = email;
        this.gender = gender;
    }
    public Employee() {
    }
}
```

2. 准备dao模拟数据

```java
import java.util.Collection;
import java.util.HashMap;
import java.util.Map;

import com.tl.pojo.Employee;
import org.springframework.stereotype.Repository;
@Repository
public class EmployeeDao {
    private static Map<Integer, Employee> employees = null;
    static{
        employees = new HashMap<Integer, Employee>();
        employees.put(1001, new Employee(1001, "E-AA", "aa@163.com", 1));
        employees.put(1002, new Employee(1002, "E-BB", "bb@163.com", 1));
        employees.put(1003, new Employee(1003, "E-CC", "cc@163.com", 0));
        employees.put(1004, new Employee(1004, "E-DD", "dd@163.com", 0));
        employees.put(1005, new Employee(1005, "E-EE", "ee@163.com", 1));
    }
    private static Integer initId = 1006;
    public void save(Employee employee){
        if(employee.getId() == null){
            employee.setId(initId++);
        }
        employees.put(employee.getId(), employee);
    }
    public Collection<Employee> getAll(){
        return employees.values();
    }
    public Employee get(Integer id){
        return employees.get(id);
    }
    public void delete(Integer id){
        employees.remove(id);
    }
}
```

#### 功能清单

| 功能清单      | url地址       | 请求方式   |
| --------- | ----------- | ------ |
| 访问首页      | /           | GET    |
| 查询全部数据    | /employee   | GET    |
| 删除        | /employee/2 | DELETE |
| 跳转到添加数据页面 | /toadd      | GET    |
| 执行保存      | /employee   | POST   |
| 跳转到更新数据页面 | /employee/2 | GET    |
| 执行更新      | /employee   | PUT    |

#### 具体功能：访问首页

##### 配置view-controller

`<mvc:view-controller path="/" view-name="index"/>`

##### 创建页面

```html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
    <head>
        <meta charset="UTF-8" >
        <title>Title</title>
    </head>
    <body>
        <h1>首页</h1>
        <a th:href="@{/employee}">访问员工信息</a>
    </body>
</html>
```

#### 具体功能：查询所有员工信息

##### 控制器方法

```java
@Controller
public class EmployeeController {
    @Autowired
    private EmployeeDao employeeDao;

    @RequestMapping(value = "/employee",method = RequestMethod.GET)
    public String getAllEmployee(Model model){
        //获取所有的员工信息
        Collection<Employee> allEmployee = employeeDao.getAll();
        //将所有的员工信息在请求域中共享
        model.addAttribute("allEmployee",allEmployee);
        //跳转到列表页面
        return "employee_list";
    }
}
```

##### 创建employee_list.html

```html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>employee_list</title>
</head>
<body>

<table>
    <tr>
        <th colspan="5">employee list</th>
    </tr>
    <tr>
        <th>id</th>
        <th>lastName</th>
        <th>email</th>
        <th>gender</th>
        <th>options</th>
    </tr>
    <tr th:each="employee:${allEmployee}">
        <td th:text="${employee.id}"></td>
        <td th:text="${employee.lastName}"></td>
        <td th:text="${employee.email}"></td>
        <td th:text="${employee.gender}"></td>
        <td>
            <a href="">delete</a>
            <a href="">update</a>
        </td>
    </tr>
</table>

</body>
</html>
```

#### 具体功能：添加员工信息

##### 控制器方法

```java
    @RequestMapping(value = "/employee",method = RequestMethod.POST)
    public String addEmployee(Employee employee){
        //保存员工信息
        employeeDao.save(employee);
        //重定向到列表功能：/employee
        return "redirect:/employee";
    }
```

##### 创建employee_add.html

```html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>add employee</title>
    <link rel="stylesheet" th:href="@{/static/css/index_work.css}">
</head>
<body>
<form th:action="@{/employee}" method="post">
    <table>
        <tr>
            <th colspan="2">add employee</th>
        </tr>
        <tr>
            <td>lastName</td>
            <td>
                <input type="text" name="lastName">
            </td>
        </tr>
        <tr>
            <td>email</td>
            <td>
                <input type="text" name="email">
            </td>
        </tr>

        <tr>
            <td>gender</td>
            <td>
                <input type="radio" name="gender" value="1">male
                <input type="radio" name="gender" value="0">female
            </td>
        </tr>

        <tr>
            <td colspan="2">
                <input type="submit" value="add">
            </td>
        </tr>


    </table>
</form>

</body>
</html>
```

##### 具体功能：修改员工信息和根据ID查询员工信息

##### 控制器方法

```java
    @RequestMapping(value = "/employee/{id}",method = RequestMethod.GET)
    public String toUpdate(@PathVariable("id") Integer id,Model model){
        //根据id查询员工信息
        Employee employee = employeeDao.get(id);
        //将员工信息共享到请求域中
        model.addAttribute("employee",employee);
        //跳转到employee_update.html
        return "employee_update";
    }

    @RequestMapping(value = "/employee",method = RequestMethod.PUT)
    public String updateEmployee(Employee employee){
        //修改员工信息
        employeeDao.save(employee);

        //重定向到列表功能：/employee
        return "redirect:employee";
    }
```

#### 创建employee_update.html

（修改employee_list.html：`<a th:href="@{'/employee/' +  ${employee.id}}">update</a>`）

```html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>update employee</title>
    <link rel="stylesheet" th:href="@{/static/css/index_work.css}">
</head>
<body>
<form th:action="@{/employee}" method="post">
    <input type="hidden" name="_method" value="put">
    <input type="hidden" name="id" th:value="${employee.id}">
    <table>
        <tr>
            <th colspan="2">update employee</th>
        </tr>
        <tr>
            <td>lastName</td>
            <td>
                <input type="text" name="lastName" th:value="${employee.lastName}">
            </td>
        </tr>
        <tr>
            <td>email</td>
            <td>
                <input type="text" name="email" th:value="${employee.email}">
            </td>
        </tr>

        <tr>
            <td>gender</td>
            <td>
                <input type="radio" name="gender" value="1" th:field="${employee.gender}">male
                <input type="radio" name="gender" value="0" th:field="${employee.gender}">female
            </td>
        </tr>

        <tr>
            <td colspan="2">
                <input type="submit" value="update">
            </td>
        </tr>


    </table>
</form>

</body>
</html>
```

#### 具体功能：删除员工信息

##### 控制器方法

```java
    @RequestMapping(value = "/employee/{id}",method = RequestMethod.DELETE)
    private String deleteEmployee(@PathVariable("id") Integer id){
        //删除员工信息
        employeeDao.delete(id);
        //重定向到列表功能：/employee
        return "redirect:/employee";
    }
```

```html
<!--引入JS-->
<script type="text/javascript" th:src="@{/static/js/vue.js}"></script>
<!-- 添加具有删除功能的超链接-->
<a @click="deleteEmployee" th:href="@{'/employee/'+  ${employee.id}}">delete</a>
<!-- 通过vue处理点击事件 -->
    <script type="text/javascript">
    var vue = new Vue(
        {
        el:"#app",
        methods:{
            deleteEmployee(){
                //获取form表单
                var form = document.getElementsByTagName("form")[0];
                //将超链接的href属性值赋值给form表单的action属性
                //event.target表示当前触发事件的标签
                form.action = event.target.href;
                //表单提交
                form.submit();
                //阻止超链接的默认行为
                event.preventDefault();
            }
        }
        });
    </script>
```

### SpringMVC处理Ajax请求

#### @RequestBody

`@RequestBody`可以获取请求体信息，使用`@RequestBody`注解标识控制器方法的形参，当前请求的请求体就会为当前注解所标识的形参赋值

```html
<!--此时必须使用post请求方式，因为get请求没有请求体-->
<form th:action="@{/test/RequestBody}" method="post">
    用户名：<input type="text" name="username"><br>
    密码：<input type="password" name="password"><br>
    <input type="submit">
</form>
```

```java
@RequestMapping("/test/RequestBody")
public String testRequestBody(@RequestBody String requestBody){
    System.out.println("requestBody:"+requestBody);
    return "success";
    // 输出结果：requestBody:username=admin&password=123456
}
```

#### @RequestBody获取json格式的请求参数

> 在使用了axios发送ajax请求之后，浏览器发送到服务器的请求参数有两种格式：
> 
> 1. name=value&name=value...，此时的请求参数可以通过request.getParameter()获取，对应
>    SpringMVC中，可以直接通过控制器方法的形参获取此类请求参数
> 2. {key:value,key:value,...}，此时无法通过request.getParameter()获取，之前我们使用操作json的相关jar包gson或jackson处理此类请求参数，可以将其转换为指定的实体类对象或map集合。在SpringMVC中，直接使用@RequestBody注解标识控制器方法的形参即可将此类请求参数转换为java对象

使用`@RequestBody`获取json格式的请求参数的条件：

1. 导入jackson的依赖

```xml
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-databind</artifactId>
    <version>2.12.1</version>
</dependency>
```

2. SpringMVC的配置文件中设置开启mvc的注解驱动

```xml
    <mvc:annotation-driven />
```

3. 在控制器方法的形参位置，设置json格式的请求参数要转换成的java类型（实体类或map）的参数，并使用`@RequestBody`注解标识

```html
<input type="button" value="测试@RequestBody获取json格式的请求参数"@click="testRequestBody()"><br>
<script type="text/javascript" th:src="@{/js/vue.js}"></script>
<script type="text/javascript" th:src="@{/js/axios.min.js}"></script>
<script type="text/javascript">
    var vue = new Vue({
        el:"#app",
        methods:{
                testRequestBody(){
                    axios.post(
                        "/SpringMVC/test/RequestBody/json",
                        {sername:"admin",password:"123456",age:23,gender:"男"}
                    ).then(response=>{
                        console.log(response.data)
                    });
                }
        }
    });
</script>
```

（下面两段代码获取到的User信息是完全一样的）

```java
    @RequestMapping("/test/RequestBody/json")
    public void testRequestBody(@RequestBody Map<String,Object> map, HttpServletResponse response) throws IOException {
        System.out.println(map);
        response.getWriter().write("hello,RequestBody");
    }
    public void testRequestBody(@RequestBody User user, HttpServletResponse response) throws IOException {
        System.out.println(user);
        response.getWriter().write("hello,RequestBody");
    }
```

#### @ResponseBody

@ResponseBody用于标识一个控制器方法，可以将该方法的返回值直接作为响应报文的响应体响应到浏览器

```java
@RequestMapping("/testResponseBody")
    public String testResponseBody(){
        //此时会跳转到逻辑视图success所对应的页面
        return "success";
    }
@RequestMapping("/testResponseBody")
@ResponseBody
    public String testResponseBody(){
        //此时响应浏览器数据success
        return "success";
}
```

#### @ResponseBody响应浏览器json数据

> 服务器处理ajax请求之后，大多数情况都需要向浏览器响应一个java对象，此时必须将java对象转换为json字符串才可以响应到浏览器，之前我们使用操作json数据的jar包gson或jackson将java对象转换为json字符串。在SpringMVC中，我们可以直接使用@ResponseBody注解实现此功能

@ResponseBody响应浏览器json数据的条件：

1. 导入jackson的依赖

```xml
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-databind</artifactId>
    <version>2.12.1</version>
</dependency>
```

2. SpringMVC的配置文件中设置开启mvc的注解驱动

```xml
    <mvc:annotation-driven />
```

3. 使用@ResponseBody注解标识控制器方法

```html
<input type="button" value="测试@ResponseBody响应浏览器json格式的数据"@click="testResponseBody()"><br>
<script type="text/javascript" th:src="@{/js/vue.js}"></script>
<script type="text/javascript" th:src="@{/js/axios.min.js}"></script>
<script type="text/javascript">
    var vue = new Vue({
        el:"#app",
        methods:{
            testResponseBody(){
                axios.post("/SpringMVC/test/ResponseBody/json").then(response=>{
                    console.log(response.data);
                });
            }
        }
    });
</script>
```

```java
    @RequestMapping("/test/ResponseBody/json")
    @ResponseBody
    //响应浏览器实体类对象
    public User testResponseBodyJson(){
        User user = new User(1001,"admin","123456",20,"女");
        return user;
    }

    //响应浏览器map集合
    public List<User> testResponseBodyJson(){
        User user0 = new User(1001,"admin","123456",20,"女");
        User user1 = new User(1002,"admin","123456",20,"女");
        User user2 = new User(1003,"admin","123456",20,"女");
        Map<String,Object> map = new HashMap<>();
        map.put("1001",user0);
        map.put("1002",user1);
        map.put("1003",user2);
        return map;
    }

    public List<User> testResponseBodyJson(){
        //响应浏览器list集合
        User user0 = new User(1001,"admin","123456",20,"女");
        User user1 = new User(1002,"admin","123456",20,"女");
        User user2 = new User(1003,"admin","123456",20,"女");
        List<User> list = Arrays.asList(user0, user1, user2);
        return list;
    }
```

#### @RestController注解

`@RestController`注解是springMVC提供的一个复合注解，标识在控制器的类上，就相当于为类添加了`@Controller`注解，并且为其中的每个方法添加了`@ResponseBody`注解

### 文件上传和下载

#### 文件下载

ResponseEntity用于控制器方法的返回值类型，该控制器方法的返回值就是响应到浏览器的响应报文。

使用ResponseEntity实现下载文件的功能

```java
    @RequestMapping("/test/down")
    public ResponseEntity<byte[]> testResponseEntity(HttpSession session) throws IOException {
        //获取ServletContext对象
        ServletContext servletContext = session.getServletContext();
        //获取服务器中文件的真实路径
        String realPath = servletContext.getRealPath("img");
        realPath = realPath + File.separator + "01.png";
        //创建输入流
        InputStream is = new FileInputStream(realPath);
        //创建字节数组.is.available()获取输入六所对应文件的字节数
        byte[] bytes = new byte[is.available()];
        //将流读到字节数组中
        is.read(bytes);
        //创建HttpHeaders对象设置响应头信息
        MultiValueMap<String, String> headers = new HttpHeaders();
        //设置要下载方式以及下载文件的名字
        headers.add("Content-Disposition", "attachment;filename=1.png");
        //设置响应状态码
        HttpStatus statusCode = HttpStatus.OK;
        //创建ResponseEntity对象
        ResponseEntity<byte[]> responseEntity = new ResponseEntity<>(bytes, headers,statusCode);
        //关闭输入流
        is.close();
        return responseEntity;

    }
```

#### 文件上传

文件上传要求form表单的请求方式必须为post，并且添加属性`enctype="multipart/form-data"`。SpringMVC中将上传的文件封装到MultipartFile对象中，通过此对象可以获取文件相关信息

上传步骤：

##### 添加依赖

```xml
<!-- https://mvnrepository.com/artifact/commons-fileupload/commons-fileupload -->
<dependency>
    <groupId>commons-fileupload</groupId>
    <artifactId>commons-fileupload</artifactId>
    <version>1.3.1</version>
</dependency>
```

##### 在SpringMVC的配置文件添加配置

```xml
<!--必须通过文件解析器的解析才能将文件转换为MultipartFile对象-->
<bean id="multipartResolver" class="org.springframework.web.multipart.commons.CommonsMultipartResolver">
</bean>
```

##### 控制器方法

```java
    @RequestMapping("/test/up")
    public String testUp(MultipartFile photo, HttpSession session) throws IOException {
        //获取上传的文件的文件名
        String filename = photo.getOriginalFilename();
        System.out.println(filename);
        //获取ServletContext对象
        ServletContext servletContext = session.getServletContext();
        //获取当前工程下photo目录的真实路径
        String photoPath = servletContext.getRealPath("photo");
        //创建photoPath对应的File对象
        File file = new File(photoPath);
        //判断File所对应目录是否存在
        if(!file.exists()){
            file.mkdir();
        }
        String finalPath = photoPath + File.separator + filename;
        //上传文件
        photo.transferTo(new File(finalPath));
        return "success";
    }
```

##### 附：避免上传的文件被覆盖

```java
    //获取上传的文件的扩展名
        String houzhuiName = filename.substring(filename.lastIndexOf("."));
    //获取uuid
        String uuid = UUID.randomUUID().toString();
    // 拼接一个新的文件名
        filename = uuid + houzhuiName;
```

### 拦截器

#### 拦截器的配置

SpringMVC中的拦截器用于拦截控制器方法的执行；SpringMVC中的拦截器需要实现`HandlerInterceptor`；SpringMVC的拦截器必须在SpringMVC的配置文件中进行配置

```xml
<bean class="com.atguigu.interceptor.FirstInterceptor"></bean>
<ref bean="firstInterceptor"></ref>
<!-- 以上两种配置方式都是对DispatcherServlet所处理的所有的请求进行拦截 -->
<mvc:interceptor>
    <mvc:mapping path="/**"/>
    <mvc:exclude-mapping path="/testRequestEntity"/>
    <ref bean="firstInterceptor"></ref>
</mvc:interceptor>
<!--
    以上配置方式可以通过ref或bean标签设置拦截器，通过mvc:mapping设置需要拦截的请求，
    通过mvc:exclude-mapping设置需要排除的请求，即不需要拦截的请求
-->
```

#### 拦截器的三个抽象方法

- `preHandle`：在控制器方法执行之前执行`preHandle()`，其`boolean`类型的返回值表示是否拦截或放行，返回`true`为放行，即调用控制器方法；返回`false`表示拦截，即不调用控制器方法
- `postHandle`：控制器方法执行之后执行`postHandle()`
- `afterCompletion`：处理完视图和模型数据，且渲染视图完毕之后执行`afterCompletion()`

#### 多个拦截器的执行顺序

①若每个拦截器的`preHandle()`都返回`true`，此时多个拦截器的执行顺序和拦截器在SpringMVC的配置文件的配置顺序有关：`preHandle()`会按照配置的顺序执行，而`postHandle()`和`afterCompletion()`会按照配置的反序执行
②若某个拦截器的`preHandle()`返回了`false`，`preHandle()`返回`false`和它之前的拦截器的`preHandle()`都会执行，`postHandle()`都不执行，返回`false`的拦截器之前的拦截器的`afterCompletion()`会执行

### 异常处理器

#### 基于配置的异常处理

SpringMVC提供了一个处理控制器方法执行过程中所出现的异常的接口：`HandlerExceptionResolver`。该接口的实现类有：`DefaultHandlerExceptionResolver`和`SimpleMappingExceptionResolver`
自定义的异常处理器`SimpleMappingExceptionResolver`，使用方式：

```xml
<bean
      class="org.springframework.web.servlet.handler.SimpleMappingExceptionResolver">
    <property name="exceptionMappings">
        <props>
            <!--
                properties的键表示处理器方法执行过程中出现的异常
                properties的值表示若出现指定异常时，设置一个新的视图名称，跳转到指定页面
            -->
            <prop key="java.lang.ArithmeticException">error</prop>
        </props>
    </property>
    <!--
  exceptionAttribute属性设置一个属性名，将出现的异常信息在请求域中进行共享
 -->
    <property name="exceptionAttribute" value="ex"></property>
</bean>
```

#### 基于注解的异常处理

```java
//@ControllerAdvice将当前类标识为异常处理的组件
@ControllerAdvice
public class ExceptionController {
    //@ExceptionHandler用于设置要处理的异常信息
    @ExceptionHandler(ArithmeticException.class)
    //ex表示控制器方法所出现的异常
    public String handleArithmeticException(Exception ex, Model model){
        model.addAttribute("ex", ex);
        return "error";
    }
}
```

### 注解配置SpringMVC

使用配置类和注解代替web.xml和SpringMVC配置文件的功能

#### 创建初始化类，代替web.xml

在Servlet3.0环境中，容器会在类路径中查找实现`javax.servlet.ServletContainerInitializer`接口的类，如果找到的话就用它来配置Servlet容器。 Spring提供了这个接口的实现，名为`SpringServletContainerInitializer`，这个类反过来又会查找实现`WebApplicationInitializer`的类并将配置的任务交给它们来完成。Spring3.2引入了一个便利的WebApplicationInitializer基础实现，名为`AbstractAnnotationConfigDispatcherServletInitializer`，当我们的类扩展了`AbstractAnnotationConfigDispatcherServletInitializer`并将其部署到Servlet3.0容器的时候，容器会自动发现它，并用它来配置Servlet上下文。

```java
public class WebInit extends AbstractAnnotationConfigDispatcherServletInitializer {
    /**
     *
     * @return
     * 代替web.xml
     */
    @Override
    //设置一个配置类代替Spring的配置文件
    protected Class<?>[] getRootConfigClasses() {
        return new Class[]{SpringConfig.class};
    }

    @Override
    //设置一个配置类代替SpringMVC的配置文件
    protected Class<?>[] getServletConfigClasses() {
        return new Class[]{WebConfig.class};
    }

    @Override
    //设置SpringMVC的前端控制器DispatcherServlet的Uurl-pattern
    protected String[] getServletMappings() {
        return new String[]{"/"};
    }

    @Override
    //设置当前的过滤器
    protected Filter[] getServletFilters() {
        //创建编码过滤器
        CharacterEncodingFilter characterEncodingFilter = new CharacterEncodingFilter();
        characterEncodingFilter.setEncoding("UTF-8");
        characterEncodingFilter.setForceEncoding(true);
        //创建处理请求方式的过滤器
        HiddenHttpMethodFilter hiddenHttpMethodFilter = new HiddenHttpMethodFilter();
        return new Filter[]{characterEncodingFilter,hiddenHttpMethodFilter};
    }
```

#### 创建SpringConfig配置类，代替spring的配置文件

```java
@Configuration
    public class SpringConfig {
    //ssm整合之后，spring的配置信息写在此类中
    }
```

#### 创建WebConfig配置类，代替SpringMVC的配置文件

```java
@Configuration
//1. 扫描组件
@ComponentScan("com.tl.controller")
//开启MVC的注解驱动
@EnableWebMvc
public class WebConfig implements WebMvcConfigurer {

    @Override
    //默认的servlet处理静态资源
    public void configureDefaultServletHandling(DefaultServletHandlerConfigurer configurer) {
        configurer.enable();
    }

    @Override
    //配置视图控制器
    public void addViewControllers(ViewControllerRegistry registry) {
        registry.addViewController("/").setViewName("index");
    }

    @Bean
    // @Bean注解可将标识的方法的返回值作为bean进行管理，bean的id为方法名
    public CommonsMultipartResolver multipartResolver(){
        return new CommonsMultipartResolver();
    }

    @Override
    public void addInterceptors(InterceptorRegistry registry) {
        FirstInterceptor firstInterceptor = new FirstInterceptor();
        registry.addInterceptor(firstInterceptor).addPathPatterns("/**");
    }

    @Override
    //配置异常解析器
    public void configureHandlerExceptionResolvers(List<HandlerExceptionResolver> resolvers) {
        SimpleMappingExceptionResolver exceptionResolver = new SimpleMappingExceptionResolver();
        Properties prop = new Properties();
        prop.setProperty("java.lang.ArithmeticException","error");
        exceptionResolver.setExceptionMappings(prop);
        exceptionResolver.setExceptionAttribute("ex");
        resolvers.add(exceptionResolver);
    }
    // 以下三个方法直接复制就好
    //配置生成模板解析器
    @Bean
    public ITemplateResolver templateResolver() {
        WebApplicationContext webApplicationContext = ContextLoader.getCurrentWebApplicationContext();
        // ServletContextTemplateResolver需要一个ServletContext作为构造参数，可通过WebApplicationContext 的方法获得
        ServletContextTemplateResolver templateResolver = new
                ServletContextTemplateResolver(webApplicationContext.getServletContext());
        templateResolver.setPrefix("/WEB-INF/templates/");
        templateResolver.setSuffix(".html");
        templateResolver.setCharacterEncoding("UTF-8");
        templateResolver.setTemplateMode(TemplateMode.HTML);
        return templateResolver;
    }
    //生成模板引擎并为模板引擎注入模板解析器
    @Bean
    public SpringTemplateEngine templateEngine(ITemplateResolver templateResolver) {
        SpringTemplateEngine templateEngine = new SpringTemplateEngine();
        templateEngine.setTemplateResolver(templateResolver);
        return templateEngine;
    }
    //生成视图解析器并未解析器注入模板引擎
    @Bean
    public ViewResolver viewResolver(SpringTemplateEngine templateEngine) {
        ThymeleafViewResolver viewResolver = new ThymeleafViewResolver();
        viewResolver.setCharacterEncoding("UTF-8");
        viewResolver.setTemplateEngine(templateEngine);
        return viewResolver;
    }
}
```

#### 测试功能

```html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>首页</title>
</head>
<body>
    <h1>index.html</h1>
</body>
</html>
```

### SpringMVC执行流程

#### SpringMVC常用组件

1. DispatcherServlet：前端控制器，不需要工程师开发，由框架提供
   作用：统一处理请求和响应，整个流程控制的中心，由它调用其它组件处理用户的请求
2. HandlerMapping：处理器映射器，不需要工程师开发，由框架提供
   作用：根据请求的url、method等信息查找Handler，即控制器方法
3. Handler：处理器，需要工程师开发
   作用：在DispatcherServlet的控制下Handler对具体的用户请求进行处理
4. HandlerAdapter：处理器适配器，不需要工程师开发，由框架提供
   作用：通过HandlerAdapter对处理器（控制器方法）进行执行
5. ViewResolver：视图解析器，不需要工程师开发，由框架提供
   作用：进行视图解析，得到相应的视图，例如：ThymeleafView、InternalResourceView、RedirectView
6. View：视图
   作用：将模型数据通过页面展示给用户

#### DispatcherServlet初始化过程

DispatcherServlet 本质上是一个 Servlet，所以天然的遵循 Servlet 的生命周期。所以宏观上是 Servlet生命周期来进行调度。

##### 初始化WebApplicationContext

所在类：`org.springframework.web.servlet.FrameworkServlet`

```java
protected WebApplicationContext initWebApplicationContext() {
    WebApplicationContext rootContext = WebApplicationContextUtils.getWebApplicationContext(getServletContext());
    WebApplicationContext wac = null;
    if (this.webApplicationContext != null) {
        // A context instance was injected at construction time -> use it
        wac = this.webApplicationContext;
        if (wac instanceof ConfigurableWebApplicationContext) {
            ConfigurableWebApplicationContext cwac =(ConfigurableWebApplicationContext) wac;
            if (!cwac.isActive()) {
                // The context has not yet been refreshed -> provide services such as
                    // setting the parent context, setting the application context id, etc
                    if (cwac.getParent() == null) {
                        // The context instance was injected without an explicit parent -> set
                            // the root application context (if any; may be null) as the parent
                            cwac.setParent(rootContext);
                    }
                configureAndRefreshWebApplicationContext(cwac);
            }
        }
    }
    if (wac == null) {
        // No context instance was injected at construction time -> see if one
        // has been registered in the servlet context. If one exists, it is assumed
            // that the parent context (if any) has already been set and that the
            // user has performed any initialization such as setting the context id
            wac = findWebApplicationContext();
    }
    if (wac == null) {
        // No context instance is defined for this servlet -> create a local one
        // 创建WebApplicationContext
        wac = createWebApplicationContext(rootContext);
    }
    if (!this.refreshEventReceived) {
        // Either the context is not a ConfigurableApplicationContext with refresh
            // support or the context injected at construction time had already been
            // refreshed -> trigger initial onRefresh manually here.
            synchronized (this.onRefreshMonitor) {
            // 刷新WebApplicationContext
            onRefresh(wac);
        }
    }
    if (this.publishContext) {
        // Publish the context as a servlet context attribute.
        // 将IOC容器在应用域共享
        String attrName = getServletContextAttributeName();
        getServletContext().setAttribute(attrName, wac);
    }
    return wac;
}
```

##### 创建WebApplicationContext

所在类：`org.springframework.web.servlet.FrameworkServlet`

```java
protected WebApplicationContext createWebApplicationContext(@Nullable ApplicationContext parent) {
    Class<?> contextClass = getContextClass();
    if (!ConfigurableWebApplicationContext.class.isAssignableFrom(contextClass))
    {
        throw new ApplicationContextException("Fatal initialization error in servlet with name '" +getServletName() +
                                              "': custom WebApplicationContext class [" + contextClass.getName() +
                                              "] is not of type ConfigurableWebApplicationContext");
    }
    // 通过反射创建 IOC 容器对象
    ConfigurableWebApplicationContext wac = (ConfigurableWebApplicationContext)BeanUtils.instantiateClass(contextClass);
    wac.setEnvironment(getEnvironment());
    // 设置父容器
    wac.setParent(parent);
    String configLocation = getContextConfigLocation();
    if (configLocation != null) {
        wac.setConfigLocation(configLocation);
    }
    configureAndRefreshWebApplicationContext(wac);
    return wac;
}
```

##### DispatcherServlet初始化策略

FrameworkServlet创建WebApplicationContext后，刷新容器，调用onRefresh(wac)，此方法在DispatcherServlet中进行了重写，调用了initStrategies(context)方法，初始化策略，即初始化DispatcherServlet的各个组件
所在类：`org.springframework.web.servlet.DispatcherServlet`

```java
protected void initStrategies(ApplicationContext context) {
    initMultipartResolver(context);
    initLocaleResolver(context);
    initThemeResolver(context);
    initHandlerMappings(context);
    initHandlerAdapters(context);
    initHandlerExceptionResolvers(context);
    initRequestToViewNameTranslator(context);
    initViewResolvers(context);
    initFlashMapManager(context);
}
```

#### DispatcherServlet调用组件处理请求

##### processRequest()

FrameworkServlet重写HttpServlet中的`service()`和`doXxx()`，这些方法中调用了`processRequest(request, response)`

所在类：`org.springframework.web.servlet.FrameworkServlet`

```java
protected final void processRequest(HttpServletRequest request,HttpServletResponse response)throws ServletException, IOException
{
    long startTime = System.currentTimeMillis();
    Throwable failureCause = null;
    LocaleContext previousLocaleContext = LocaleContextHolder.getLocaleContext();
    LocaleContext localeContext = buildLocaleContext(request);
    RequestAttributes previousAttributes = RequestContextHolder.getRequestAttributes();
    ServletRequestAttributes requestAttributes = buildRequestAttributes(request,response, previousAttributes);
    WebAsyncManager asyncManager = WebAsyncUtils.getAsyncManager(request);
    asyncManager.registerCallableInterceptor(FrameworkServlet.class.getName(),new RequestBindingInterceptor());
    initContextHolders(request, localeContext, requestAttributes);
    try {
        // 执行服务，doService()是一个抽象方法，在DispatcherServlet中进行了重写
        doService(request, response);
    }
    catch (ServletException | IOException ex) {
        failureCause = ex;
        throw ex;
    }
    catch (Throwable ex) {
        failureCause = ex;
        throw new NestedServletException("Request processing failed", ex);
    }
    finally {
        resetContextHolders(request, previousLocaleContext, previousAttributes);
        if (requestAttributes != null) {
            requestAttributes.requestCompleted();
        }
        logResult(request, response, failureCause, asyncManager);
        publishRequestHandledEvent(request, response, startTime, failureCause);
    }
}
```

##### doService()

所在类：`org.springframework.web.servlet.DispatcherServlet`

```java
@Override
protected void doService(HttpServletRequest request, HttpServletResponse response) throws Exception {
 logRequest(request);
    // Keep a snapshot of the request attributes in case of an include,
    // to be able to restore the original attributes after the include.
    Map<String, Object> attributesSnapshot = null;
    if (WebUtils.isIncludeRequest(request)) {
        attributesSnapshot = new HashMap<>();
        Enumeration<?> attrNames = request.getAttributeNames();
        while (attrNames.hasMoreElements()) {
            String attrName = (String) attrNames.nextElement();
            if (this.cleanupAfterInclude || attrName.startsWith(DEFAULT_STRATEGIES_PREFIX)) {
                attributesSnapshot.put(attrName,request.getAttribute(attrName));
            }
        }
    }
    // Make framework objects available to handlers and view objects.
    request.setAttribute(WEB_APPLICATION_CONTEXT_ATTRIBUTE,getWebApplicationContext());
    request.setAttribute(LOCALE_RESOLVER_ATTRIBUTE, this.localeResolver);
    request.setAttribute(THEME_RESOLVER_ATTRIBUTE, this.themeResolver);
    request.setAttribute(THEME_SOURCE_ATTRIBUTE, getThemeSource());
    if (this.flashMapManager != null) {
        FlashMap inputFlashMap = this.flashMapManager.retrieveAndUpdate(request,response);
        if (inputFlashMap != null) {
            request.setAttribute(INPUT_FLASH_MAP_ATTRIBUTE,Collections.unmodifiableMap(inputFlashMap));
        }
        request.setAttribute(OUTPUT_FLASH_MAP_ATTRIBUTE, new FlashMap());
        request.setAttribute(FLASH_MAP_MANAGER_ATTRIBUTE, this.flashMapManager);
    }
    RequestPath requestPath = null;
    if (this.parseRequestPath && !ServletRequestPathUtils.hasParsedRequestPath(request)) {
        requestPath = ServletRequestPathUtils.parseAndCache(request);
    }
    try {
        // 处理请求和响应
        doDispatch(request, response);
    }
    finally {
        if
            (!WebAsyncUtils.getAsyncManager(request).isConcurrentHandlingStarted()) {
            // Restore the original attribute snapshot, in case of an include.
            if (attributesSnapshot != null) {
                restoreAttributesAfterInclude(request, attributesSnapshot);
            }
        }
        if (requestPath != null) {
            ServletRequestPathUtils.clearParsedRequestPath(request);
        }
    }
}
```

##### doDispatch()

所在类：`org.springframework.web.servlet.DispatcherServlet`

```java
protected void doDispatch(HttpServletRequest request, HttpServletResponse response) throws Exception {
    HttpServletRequest processedRequest = request;
    HandlerExecutionChain mappedHandler = null;
    boolean multipartRequestParsed = false;
    WebAsyncManager asyncManager = WebAsyncUtils.getAsyncManager(request);
    try {
        ModelAndView mv = null;
        Exception dispatchException = null;
        try {
            processedRequest = checkMultipart(request);
            multipartRequestParsed = (processedRequest != request);
            // Determine handler for the current request.
            /*
                mappedHandler：调用链
                包含handler、interceptorList、interceptorIndex
                handler：浏览器发送的请求所匹配的控制器方法
                interceptorList：处理控制器方法的所有拦截器集合
                interceptorIndex：拦截器索引，控制拦截器afterCompletion()的执行
             */
            mappedHandler = getHandler(processedRequest);
            if (mappedHandler == null) {
                noHandlerFound(processedRequest, response);
                return;
            }
            // Determine handler adapter for the current request.
            // 通过控制器方法创建相应的处理器适配器，调用所对应的控制器方法
            HandlerAdapter ha = getHandlerAdapter(mappedHandler.getHandler());
            // Process last-modified header, if supported by the handler.
            String method = request.getMethod();
            boolean isGet = "GET".equals(method);
            if (isGet || "HEAD".equals(method)) {
                long lastModified = ha.getLastModified(request,mappedHandler.getHandler());
                if (new ServletWebRequest(request,response).checkNotModified(lastModified) && isGet) {
                    return;
                }
            }
            // 调用拦截器的preHandle()
            if (!mappedHandler.applyPreHandle(processedRequest, response)) {
                return;
            }
            // Actually invoke the handler.
            // 由处理器适配器调用具体的控制器方法，最终获得ModelAndView对象
            mv = ha.handle(processedRequest, response,mappedHandler.getHandler());
            if (asyncManager.isConcurrentHandlingStarted()) {
                return;
            }
            applyDefaultViewName(processedRequest, mv);
            // 调用拦截器的postHandle()
            mappedHandler.applyPostHandle(processedRequest, response, mv);
        }
        catch (Exception ex) {
            dispatchException = ex;
        }
        catch (Throwable err) {
            // As of 4.3, we're processing Errors thrown from handler methods as well,
            // making them available for @ExceptionHandler methods and otherscenarios.
            dispatchException = new NestedServletException("Handler dispatchfailed", err);
         }
         // 后续处理：处理模型数据和渲染视图
         processDispatchResult(processedRequest, response, mappedHandler, mv,dispatchException);
    }
    catch (Exception ex) {
        triggerAfterCompletion(processedRequest, response, mappedHandler, ex);
    }
    catch (Throwable err) {
        triggerAfterCompletion(processedRequest, response, mappedHandler,new NestedServletException("Handler processingfailed",
                                                                                                    err));
    }
    finally {
        if (asyncManager.isConcurrentHandlingStarted()) {
            // Instead of postHandle and afterCompletion
            if (mappedHandler != null) {
                mappedHandler.applyAfterConcurrentHandlingStarted(processedRequest, response);
             }
         }
        else {
            // Clean up any resources used by a multipart request.
            if (multipartRequestParsed) {
                cleanupMultipart(processedRequest);
            }
        }
    }
}
```

##### processDispatchResult()

```java
private void processDispatchResult(HttpServletRequest request,HttpServletResponse response,@Nullable HandlerExecutionChain
                                   mappedHandler, @Nullable ModelAndView mv,@Nullable Exception exception) throws Exception {
    boolean errorView = false;
    if (exception != null) {
        if (exception instanceof ModelAndViewDefiningException) {
            logger.debug("ModelAndViewDefiningException encountered",exception);
            mv = ((ModelAndViewDefiningException) exception).getModelAndView();
        }
        else {
            Object handler = (mappedHandler != null ? mappedHandler.getHandler(): null);
            mv = processHandlerException(request, response, handler, exception);
            errorView = (mv != null);
        }
    }
    // Did the handler return a view to render?
    if (mv != null && !mv.wasCleared()) {
        // 处理模型数据和渲染视图
        render(mv, request, response);
        if (errorView) {
            WebUtils.clearErrorRequestAttributes(request);
        }
    }
    else {
        if (logger.isTraceEnabled()) {
            logger.trace("No view rendering, null ModelAndView returned.");
        }
    }
    if (WebAsyncUtils.getAsyncManager(request).isConcurrentHandlingStarted()) {
        // Concurrent handling started during a forward
        return;
    }
    if (mappedHandler != null) {
        // Exception (if any) is already handled..
        // 调用拦截器的afterCompletion()
        mappedHandler.triggerAfterCompletion(request, response, null);
    }
}
```

#### SpringMVC的执行流程

1. 用户向服务器发送请求，请求被SpringMVC 前端控制器 DispatcherServlet捕获。
2. DispatcherServlet对请求URL进行解析，得到请求资源标识符（URI），判断请求URI对应的映射：
   - 不存在
     - 再判断是否配置了mvc:default-servlet-handler
     - 如果没配置，则控制台报映射查找不到，客户端展示404错误
     - 如果有配置，则访问目标资源（一般为静态资源，如：JS,CSS,HTML），找不到客户端也会展示404错误
   - 存在则执行下面的流程
3. 根据该URI，调用HandlerMapping获得该Handler配置的所有相关的对象（包括Handler对象以及Handler对象对应的拦截器），最后以HandlerExecutionChain执行链对象的形式返回。
4. DispatcherServlet 根据获得的Handler，选择一个合适的HandlerAdapter。
5. 如果成功获得HandlerAdapter，此时将开始执行拦截器的preHandler(…)方法【正向】
6. 提取Request中的模型数据，填充Handler入参，开始执行Handler（Controller)方法，处理请求。在填充Handler的入参过程中，根据你的配置，Spring将帮你做一些额外的工作：
   - HttpMessageConveter： 将请求消息（如Json、xml等数据）转换成一个对象，将对象转换为指定的响应信息
   - 数据转换：对请求消息进行数据转换。如String转换成Integer、Double等
   - 数据格式化：对请求消息进行数据格式化。 如将字符串转换成格式化数字或格式化日期等
   - 数据验证： 验证数据的有效性（长度、格式等），验证结果存储到BindingResult或Error中
7. Handler执行完成后，向DispatcherServlet 返回一个ModelAndView对象。
8. 此时将开始执行拦截器的postHandle(...)方法【逆向】。
9. 根据返回的ModelAndView（此时会判断是否存在异常：如果存在异常，则执行HandlerExceptionResolver进行异常处理）选择一个适合的ViewResolver进行视图解析，根据Model和View，来渲染视图。
10. 渲染视图完毕执行拦截器的afterCompletion(…)方法【逆向】。
11. 将渲染结果返回给客户端。

## SSM整合

### ContextLoaderListener

Spring提供了监听器ContextLoaderListener，实现ServletContextListener接口，可监听ServletContext的状态，在web服务器的启动，读取Spring的配置文件，创建Spring的IOC容器。web应用中必须在web.xml中配置

```xml
<listener>
    <!--
        配置Spring的监听器，在服务器启动时加载Spring的配置文件
        Spring配置文件默认位置和名称：/WEB-INF/applicationContext.xml
        可通过上下文参数自定义Spring配置文件的位置和名称
    -->
    <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
</listener>
<!--自定义Spring配置文件的位置和名称-->
<context-param>
    <param-name>contextConfigLocation</param-name>
    <param-value>classpath:spring.xml</param-value>
</context-param>
```

### 准备工作

#### 创建Maven 模块

#### 导入依赖

```xml
<packaging>war</packaging>
<properties>
    <spring.version>5.3.1</spring.version>
</properties>
<dependencies>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context</artifactId>
        <version>${spring.version}</version>
    </dependency>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-beans</artifactId>
        <version>${spring.version}</version>
    </dependency>
    <!--springmvc-->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-web</artifactId>
        <version>${spring.version}</version>
    </dependency>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-webmvc</artifactId>
        <version>${spring.version}</version>
    </dependency>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-jdbc</artifactId>
        <version>${spring.version}</version>
    </dependency>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-aspects</artifactId>
        <version>${spring.version}</version>
    </dependency>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-test</artifactId>
        <version>${spring.version}</version>
    </dependency>
    <!-- Mybatis核心 -->
    <dependency>
        <groupId>org.mybatis</groupId>
        <artifactId>mybatis</artifactId>
        <version>3.5.7</version>
    </dependency>
    <!--mybatis和spring的整合包-->
    <dependency>
        <groupId>org.mybatis</groupId>
        <artifactId>mybatis-spring</artifactId>
        <version>2.0.6</version>
    </dependency>
    <!-- 连接池 -->
    <dependency>
        <groupId>com.alibaba</groupId>
        <artifactId>druid</artifactId>
        <version>1.0.9</version>
    </dependency>
    <!-- junit测试 -->
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.12</version>
        <scope>test</scope>
    </dependency>
    <!-- MySQL驱动 -->
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>8.0.16</version>
    </dependency>
    <!-- log4j日志 -->
    <dependency>
        <groupId>log4j</groupId>
        <artifactId>log4j</artifactId>
        <version>1.2.17</version>
    </dependency>
    <!-- https://mvnrepository.com/artifact/com.github.pagehelper/pagehelper -->
    <dependency>
    <groupId>com.github.pagehelper</groupId>
    <artifactId>pagehelper</artifactId>
    <version>5.2.0</version>
    </dependency>
    <!-- 日志 -->
    <dependency>
        <groupId>ch.qos.logback</groupId>
        <artifactId>logback-classic</artifactId>
        <version>1.2.3</version>
    </dependency>
    <!-- ServletAPI -->
    <dependency>
        <groupId>javax.servlet</groupId>
        <artifactId>javax.servlet-api</artifactId>
        <version>3.1.0</version>
        <scope>provided</scope>
    </dependency>
    <dependency>
        <groupId>com.fasterxml.jackson.core</groupId>
        <artifactId>jackson-databind</artifactId>
        <version>2.12.1</version>
    </dependency>
    <dependency>
        <groupId>commons-fileupload</groupId>
        <artifactId>commons-fileupload</artifactId>
        <version>1.3.1</version>
    </dependency>
    <!-- Spring5和Thymeleaf整合包 -->
    <dependency>
        <groupId>org.thymeleaf</groupId>
        <artifactId>thymeleaf-spring5</artifactId>
        <version>3.0.12.RELEASE</version>
    </dependency>
</dependencies>
```

#### 创建表

```sql
CREATE TABLE `t_emp` (
    `emp_id` int(11) NOT NULL AUTO_INCREMENT,
    `emp_name` varchar(20) DEFAULT NULL,
    `age` int(11) DEFAULT NULL,
    `sex` char(1) DEFAULT NULL,
    `email` varchar(50) DEFAULT NULL,
    PRIMARY KEY (`emp_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8
```

### 配置web.xml

```xml
<filter>
        <filter-name>CharacterEncodingFilter</filter-name>
        <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
        <init-param>
            <param-name>encoding</param-name>
            <param-value>UTF-8</param-value>
        </init-param>
        <init-param>
            <param-name>forceEncoding</param-name>
            <param-value>true</param-value>
        </init-param>
    </filter>
    <filter-mapping>
        <filter-name>CharacterEncodingFilter</filter-name>
        <url-pattern>/*</url-pattern>
    </filter-mapping>

    <!--配置处理请求方式的过滤器-->
    <filter>
        <filter-name>HiddenHttpMethodFilter</filter-name>
        <filter-class>org.springframework.web.filter.HiddenHttpMethodFilter</filter-class>
    </filter>
    <filter-mapping>
        <filter-name>HiddenHttpMethodFilter</filter-name>
        <url-pattern>/*</url-pattern>
    </filter-mapping>
    <!--配置SpringMVC的前端控制器DispatcherServlet-->
    <servlet>
        <servlet-name>SpringMVC</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <!--设置SpringMVC配置文件自定义的位置和名称-->
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>classpath:springmvc.xml</param-value>
        </init-param>
        <!--将DispatcherServlet的初始化时间提前到服务器启动时-->
        <load-on-startup>1</load-on-startup>
    </servlet>
    <servlet-mapping>
        <servlet-name>SpringMVC</servlet-name>
        <url-pattern>/</url-pattern>
    </servlet-mapping>
    <!--配置Spring的监听器，在服务器启动时加载Spring的配置文件-->
    <listener>
        <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
    </listener>
    <!--设置Spring配置文件自定义的位置和名称-->
    <context-param>
        <param-name>contextConfigLocation</param-name>
        <param-value>classpath:spring.xml</param-value>
    </context-param>
```

### 创建SpringMVC的配置文件

```xml
<!--扫描控制层组件-->
<context:component-scan base-package="com.tl.ssm.controller"></context:component-scan>

    <!--配置视图解析器-->
    <bean id="viewResolver"
          class="org.thymeleaf.spring5.view.ThymeleafViewResolver">
        <property name="order" value="1"/>
        <property name="characterEncoding" value="UTF-8"/>
        <property name="templateEngine">
            <bean class="org.thymeleaf.spring5.SpringTemplateEngine">
                <property name="templateResolver">
                    <bean
                            class="org.thymeleaf.spring5.templateresolver.SpringResourceTemplateResolver">
                        <!-- 视图前缀 -->
                        <property name="prefix" value="/WEB-INF/templates/"/>
                        <!-- 视图后缀 -->
                        <property name="suffix" value=".html"/>
                        <property name="templateMode" value="HTML5"/>
                        <property name="characterEncoding" value="UTF-8" />
                    </bean>
                </property>
            </bean>
        </property>
    </bean>

    <!--配置默认的servlet处理静态资源-->
    <mvc:default-servlet-handler/>
    <!--开启mvc的注解驱动-->
    <mvc:annotation-driven />

    <!--配置视图控制器-->
    <mvc:view-controller path="/" view-name="index" />

    <!--配置文件上传解析器-->
    <bean id="multipartResolver" class="org.springframework.web.multipart.commons.CommonsMultipartResolver"/>
```

### 搭建MyBatis环境

#### 创建jdbc.properties文件

```properties
    jdbc.driver=com.mysql.cj.jdbc.Driver
    jdbc.url=jdbc:mysql://localhost:3306/ssm?serverTimezone=UTC
    jdbc.username=root
    jdbc.password=root
```

#### 配置mybatis-config文件

```xml
    <!--由于其他的配置均已在spring.xml文件中配置完毕，故这里的内容很少-->
    <!--      将下划线映射为驼峰  -->
    <settings>
        <setting name="mapUnderscoreToCamelCase" value="true"/>
    </settings>

    <plugins>
        <!--配置分页插件-->
        <plugin interceptor="com.github.pagehelper.PageInterceptor"></plugin>
    </plugins>
```

#### 创建Mapper接口和映射文件

```java
public interface EmployeeMapper {
    List<Employee> getEmployeeList();
}
```

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
"http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.atguigu.ssm.mapper.EmployeeMapper">
    <select id="getEmployeeList" resultType="Employee">
        select * from t_emp
    </select>
</mapper>
```

#### 创建日志文件log4j.xml

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE log4j:configuration SYSTEM "log4j.dtd">
<log4j:configuration xmlns:log4j="http://jakarta.apache.org/log4j/">
    <appender name="STDOUT" class="org.apache.log4j.ConsoleAppender">
        <param name="Encoding" value="UTF-8" />
        <layout class="org.apache.log4j.PatternLayout">
            <param name="ConversionPattern" value="%-5p %d{MM-dd HH:mm:ss,SSS} %m (%F:%L) \n" />
        </layout>
    </appender>
    <logger name="java.sql">
        <level value="debug" />
    </logger>
    <logger name="org.apache.ibatis">
        <level value="info" />
    </logger>
    <root>
        <level value="debug" />
        <appender-ref ref="STDOUT" />
    </root>
</log4j:configuration>
```

### 创建Spring的配置文件并配置

> 这一部分的代码既可以配置在mybatis-config文件中，也可以配置在spring.xml文件中。本笔记将其配置在spring.xml文件中

```xml
    <!--扫描组件（除控制层）-->
    <context:component-scan base-package="com.tl.ssm">
        <context:exclude-filter type="annotation" expression="org.springframework.stereotype.Controller"/>
    </context:component-scan>

    <!--引入jdbc.properties-->
    <context:property-placeholder location="classpath:jdbc.properties"></context:property-placeholder>

    <!--配置数据源-->
    <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">
        <property name="driverClassName" value="${jdbc.driver}"></property>
        <property name="url" value="${jdbc.url}"></property>
        <property name="username" value="${jdbc.username}"></property>
        <property name="password" value="${jdbc.password}"></property>
    </bean>

        <!--配置事务管理器-->
    <bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
        <property name="dataSource" ref="dataSource"></property>
    </bean>

    <!--开启事务的注解驱动
        将使用注解@Transactional标识的方法或类中所有的方法进行事务管理
    -->
    <tx:annotation-driven transaction-manager="transactionManager"/>

    <!--配置SQLSessionFactoryBean，可以直接在Spring的IOC中获取SQLSessionFactory-->
    <bean class="org.mybatis.spring.SqlSessionFactoryBean">
        <!--设置Mybatis的核心配置文件的路径-->
        <property name="configLocation" value="classpath:mybatis-config.xml"></property>
        <!--设置数据源-->
        <property name="dataSource" ref="dataSource"></property>
        <!--设置类型别名对应的包-->
        <property name="typeAliasesPackage" value="com.tl.ssm.pojo"></property>
<!--
        设置映射文件的路径，只有映射文件的包和mapper接口的包不一致时需要设置
        <property name="mapperLocations" value="classpath:mappers/*.xml"></property>
-->
    </bean>

    <!--配置mapper接口的扫描，可以将指定包下所有的mapper接口，通过SqlSession创建代理实现类对象，并将这些对象交给IOC容器管理-->
    <bean class="org.mybatis.spring.mapper.MapperScannerConfigurer">
        <property name="basePackage" value="com.tl.ssm.mapper"></property>
    </bean>
```

### 测试功能

#### 创建组件

实体类Employee

```java
public class Employee {
    private Integer empId;
    private String empName;
    private Integer age;
    private String sex;
    private String email;
    public Employee() {
    }
    public Employee(Integer empId, String empName, Integer age, String sex,
                    String email) {
        this.empId = empId;
        this.empName = empName;
        this.age = age;
        this.sex = sex;
        this.email = email;
    }
    public Integer getEmpId() {
        return empId;
    }
    public void setEmpId(Integer empId) {
        this.empId = empId;
    }
    public String getEmpName() {
        return empName;
    }
    public void setEmpName(String empName) {
        this.empName = empName;
    }
    public Integer getAge() {
        return age;
    }
    public void setAge(Integer age) {
        this.age = age;
    }
    public String getSex() {
        return sex;
    }
    public void setSex(String sex) {
        this.sex = sex;
    }
    public String getEmail() {
        return email;
    }
    public void setEmail(String email) {
        this.email = email;
    }
}
```

创建控制层组件EmployeeController

```java
@Controller
public class EmployeeController {
    @Autowired
    private EmployeeService employeeService;
    @RequestMapping(value = "/employee/page/{pageNum}", method = RequestMethod.GET)
    public String getEmployeeList(Model model, @PathVariable("pageNum") Integer pageNum){
        PageInfo<Employee> page = employeeService.getEmployeeList(pageNum);
        model.addAttribute("page", page);
        return "employee_list";
    }
}
```

创建接口EmployeeService

```java
public interface EmployeeService {
    PageInfo<Employee> getEmployeeList(Integer pageNum);
}
```

创建实现类EmployeeServiceImpl

```java
@Service
@Transactional
public class EmployeeServiceImpl implements EmployeeService {

    @Autowired
    private EmployeeMapper employeeMapper;
    public List<Employee> getAllEmployee() {
        return employeeMapper.getAllEmployee();
    }

    @Override
    public PageInfo<Employee> getEmployeePage(Integer pageNum) {
        // 开启分页功能
        PageHelper.startPage(pageNum,4);
        // 查询所有的员工信息
        List<Employee> list = employeeMapper.getAllEmployee();
        // 获取分页相应数据
        PageInfo<Employee> page = new PageInfo<>(list,5);
        return page;
    }
}
```

#### 创建页面

```html
    <table>
        <tr>
            <th colspan="6">员工列表</th>
        </tr>
        <tr>
            <th>流水号</th>
            <th>员工姓名</th>
            <th>年龄</th>
            <th>性别</th>
            <th>邮箱</th>
            <th>操作</th>
        </tr>
        <tr th:each="employee,status : ${page.list}">
            <td th:text="${status.count}"></td>
            <td th:text="${employee.empName}"></td>
            <td th:text="${employee.age}"></td>
            <td th:text="${employee.gender}"></td>
            <td th:text="${employee.email}"></td>
            <td>
                <a href="">删除</a>
                <a href="">修改</a>
            </td>
        </tr>
    </table>
<div style="text-align: center;">
   <a th:if="${page.hasPreviousPage}" th:href="@{/employee/page/1}">首页</a>
   <a th:if="${page.hasPreviousPage}" th:href="@{'/employee/page/' + ${page.prePage}}">上一页</a>
    <span th:each="num : ${page.navigatepageNums}">
        <a th:if="${page.pageNum == num}" style="color:red;" th:href="@{'/employee/page/' + ${num}}" th:text="'['+ ${num}+ ']'"></a>
        <a th:if="${page.pageNum != num}" th:href="@{'/employee/page/' + ${num}}" th:text="${num}"></a>
    </span>
   <a th:if="${page.hasNextPage}" th:href="@{'/employee/page/' + ${page.nextPage}}">下一页</a>
   <a th:if="${page.hasPreviousPage}" th:href="@{'/employee/page/' + ${page.pages}}">末页</a>

</div>
```

#### 最终结果

****![最终效果](2023-01-08-00-27-19.png)
