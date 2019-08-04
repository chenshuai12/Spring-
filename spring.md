​                         ***Spring源码解析***

#一 Spring整体架构  
![avator](../spring-framework-master/image/spring.jpg)  
##1.  SpringFrameworkRuntime  
###1.1  Data Access/Integration: JDBC ORM OXM JMS Transaction  
* JDBC模块提供了一个JDBC抽象层  
*  ORM模块提供了一个对象-关系映射API  
* OXM模块提供了一个Object/XML映射实现的抽象层  
* JMX模块主要包含了一些制造和消费消息的特性  
* Transaction模块支持编程和声明式事务管理,这些事务必须实现特定的接口,并且对所有POJO都适用  
###1.2 Web: Web Servlet Portlet  
* Web上下文模块建立在应用程序上下文模块之上,为基于Web的应用程序提供了上下文.所以Spring框架支持与Jakarta Struts的集  
成.Web模块还简化了处理多部分请求以及将请求参数绑定到域对象的工作      
* Web模块:提供了基础的面向Web的集成特性.例如,多文件上传、使用Servlet listeners初始化IoC容器以及一个面向Web的应  
用上下文.它还包含Spring远程支持中Web相关的部分  
* Web-Servlet模块web.servlet.jar:该模块包含Spring的MVC实现  
*  Web-Struts模块:该模块提供了对Struts的支持  
* Web-Porlet模块:提供了用了Porlet环境和Web-Servlet模块的MVC实现  
###1.3 AOP Aspects Instrumentation Messaging  
* Aop模块提供了面向切面编程的实现,他让你可以定义例如方法拦截器和切点,从而将逻辑代码分开,降低他们的耦合性.通过配置管  
理特性,SpringAop模块直接将面向切面的编程功能集成到了Spring框架中.SpringAOP模块为基于Spring的应用程序中的对象提供了事务管理服  
务.  
* Aspects模块提供了对AspectJ的支持    
* Instrumentation模块提供了class instrumentation支持和classloader实现,使得可以在特定的应用服务器上使用.  
###1.4 Core Container: Beans core Context SpEL  
* Core和Beans是框架的基础部分,提供Ioc(控制反转和依赖注入特性.这里的基础概念是BeanFactory,它提供对Factory模式的  
经典实现来消除对程序性单例模式的需要,并真正的允许你从程序逻辑中分离出依赖关系和配置  
* Core模块主要包含Spring框架基本的核心工具类,是其他组件的基本核心  
* Beans模块包含访问配置文件、创建和管理Bean以及进行IOC、DI相关操作  
* Context构建与Beans和Core模块之上,提供了一组类似于JNDI(是一个应用程序设计的API,为开发人员提供了查找和访问各种命名和目录服务的
通用、统一的接口)注册器的框架式的对象访问方法.Context模块继承了Beans模块的特性,为Spring核心提供了大量扩展,添加了国际化(例如资源
绑定)、时间传播、资源加载和对Context的透明创建的支持.Context模块同时也支持J2EE的一些特性,例如EJB、JMX和基础的远程处理.
ApplicationContext接口是Context模块的关键.  
* Expression Language模块提供了一个强大的表达式语言  
###1.5 Test  
* Test模块支持使用JUnit和TestNG对Spring组件进行测试  
#二 容器的基本实现   
    1、功能分析  
        1.1 读取配置文件  
        1.2 根据配置文件中的配置找到对应类的配置,并实例化  
        1.3 调用实例化的实例  
    2、至少需要的几个类  
        2.1 ConfigReader:用于读取以及验证配置文件  
        2.2 ReflectionUtil:用于根据配置文件中的配置进行反射实例化  
        2.3 App:用于完成整个逻辑的串联  

