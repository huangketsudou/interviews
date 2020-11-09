# Spring

**面试题：**[spring面试题](https://www.w3cschool.cn/fisug/fisug-5pot2g5k.html)

[自己动手实现的 Spring IOC 和 AOP - 上篇](http://www.tianxiaobo.com/2018/01/18/自己动手实现的-Spring-IOC-和-AOP-上篇/)

## spring依赖的技术

控制反转的**依赖注入(DI)**：可以向构造函数传递参数的发生方式，或者使用setter方法。

面向方面的程序设计(**AOP**)：一个程序中跨越多个点的功能被称为横向关注点，这些横向关注点在概念上独立于应用程序的业务逻辑，例如：日志，声明性事务，安全性或者缓存。

[Spring-bean的循环依赖以及解决方式](https://blog.csdn.net/u010853261/article/details/77940767)

[多例以及单例的循环依赖解决](https://mp.weixin.qq.com/s/pQaX2-BqFsO3pzPELWIDfQ)

## spring体系

![图片](img/arch1.png)

### 核心容器

核心容器由核心，bean，上下文以及表达式语言模块组成，

1. **核心**提供了框架的基本组成部分，包括IOC和依赖注入功能
2. **Bean**提供了BeanFactory，是一个工厂模式的复杂实现
3. **上下文**模块建立在由核心以及Bean模块提供的基础上，是访问定义和配置的任何对象的媒介，ApplicationContext接口是上下文模块的重点
4. **表达式语言**在运行时提供了查询和操作一个对象图的表达式语言

### 数据访问/继承

包括JDBC，ORM，OXM和JMS和事务处理模块

- **JDBC**提供删除冗余的JDBC相关编码的JDBC抽象层
- **ORM**为流行的对象关系映射API，包括JPA，JDO，Hibernate和iBatis，提供了集成层
- **OXM**提供了抽象层，支持包括JAXB，Castor等映射实现
- java消息服务JMS模块包含生产和消费的信息的功能
- **事物模块**为实现特殊接口的类及所有的POJO支持编程式和声明式事务管理

### Web

Web层由Web，Web-MVC，Web-Socket和Web-portle组成

- Web模块提供了基本的面向Web的集成功能，
- Web-MVC包括了Spring的模式-视图-控制器，实现web应用程序
- Web-Socket模块为WebSocket-based提供了支持，而且在web应用程序中提供了客户端和服务器端之间通信的方式
- Web-Portlet提供在Portlet模式下实现MVC

### 其他

- **AOP**提供了面向方面的编程实现，允许定义方法拦截器和切入点对代码进行解耦
- **Aspect**提供了AspectJ的集成
- **Instrumentation**提供了在应用服务器中的类instrumentation的支持和类加载器的实现
- **Messaging**模块为STOMP提供了支持作为应用程序中WebSocket子协议的使用
- **测试**模块支持对具有JUnit的Spring组件的测试

### IOC容器（Inversion of control）

spring容器是spring框架的核心，容器创建对象并连接他们，管理其整个生命周期。spring容器使用依赖注入来管理组成一个应用程序的组件，这些对象被称之为spring beans。

**定义：**就是对象之间的依赖关系通过容器来创建，对象之间的关系本来由开发者,传统的应用程序时主动获取依赖对象的，而控制反转则采用容器来创建以及获取对象，其将获取对象的行为由主动转变为被动（对象的具体实现不由自己控制），采用了程序设计中的依赖反转思想

#### 依赖注入（DI）的方式：

- 基于接口：实现特定接口以供容器注入所以来类型的对象
- 基于set方法，实现特定属性的public set方法，来让外部容器调用传入锁依赖类型的对象
- 基于构造函数，实现特定参数的构造函数，在新建对象时传入所依赖类型对象
- 基于注解，例如在私有变量前加入“@Autowired”等注解

依赖注入定义：将实例变量传到一个对象中去。

除了DI之外还有DL（依赖查找），不能解决循环依赖

#### spring的BeanFactory

创建一个Bean工厂，例如xmlbean工厂，之后根据xml文件创建指定的bean对象，得到bean对象之后，就可以对bean调用可用的方法，轻量的应用中使用

#### spring的ApplicationContext（应用上下文）

是spring中的较高级容器，和beanfactory一样，可以加载配置中的bean，将所有的bean集中在一起，当有请求的时候分配bean，并实现了一些企业需要的要求。

#### Bean

##### 定义

bean是一个被实例化，组装并通过spring IOC管理的对象，这些bean是由容器提供的配置元数据（保存在xml文件中）创建的，**现在最新的bean是采用注解方式来创建bean的，因为xml配置繁琐**

##### spring配置元数据

配置文件中包含了以下的数据：如何创建一个bean，bean的生命周期的详细信息和bean的依赖关系

spring IOC容器完全由实际编写的配置元数据的格式解耦，有下面三种方法：

- 基于XML的配置文件
- 基于注解的配置
- 基于java的配置

##### Bean的作用域

spring中定义一个bean时，必须声明bean的作用域，例如希望每次需要时就产生一个新的就声明为prototype，如果希望实现单例，就声明为singleton，默认情况下，由spring容器创建的所有bean都是singleton作用域的。

##### Bean的声明周期

在一个bean被实例化时，需要执行一些初始化工作，而bean不在需要时，并且从容器中移除时，需要一些清理工作。

### springAOP

spring框架的重要组件是面向方面编程，面向方面的编程需要把程序逻辑分解成不同的部分称为关注点，跨一个应用程序的多个点的功能被称为横切关注点。

采用了proxy模式

AOP和OOP的区别

[AOP与OOP的区别](https://www.imooc.com/wenda/detail/386695)

[IOC和AOP的面试题](https://www.imooc.com/wenda/detail/386695)

**OOP定义：**面向对象编程， 业务处理过程的实体及其属性和行为进行抽象封装，以获得更加清晰高效的逻辑单元划分 

**AOP定义：**面向切面编程，基于原来的代码产生代理对象，通过代理的方法，包装原来的方法，完成对以前方法的增强

## spring MVC

[Spring MVC【入门】就这一篇！](https://www.jianshu.com/p/91a2d0a1e45a)

- **模型**封装了应用程序数据，通常由POJO构成
- **视图**主要用于呈现模型数据，并且通常它生成客户端的浏览器可以解释HTML输出
- **控制器**主要用于处理用户请求，并且构建合适的模型并将其传递到视图呈现

- **核心元素**是Dispatcher Servlet

## spring中的设计模式

[面试官:“谈谈Spring中都用到了那些设计模式?”。](https://juejin.im/post/5ce69379e51d455d877e0ca0)

