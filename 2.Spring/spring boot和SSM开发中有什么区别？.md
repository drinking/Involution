## spring boot VS spring

### What Is Spring?
**Simply put, the Spring framework provides comprehensive infrastructure support for developing Java applications**.

It's packed with some nice features like Dependency Injection, and out of the box modules like:

-   Spring JDBC
-   Spring MVC
-   Spring Security
-   Spring AOP
-   Spring ORM
-   Spring Test

These modules can drastically reduce the development time of an application.

For example, in the early days of Java web development, we needed to write a lot of boilerplate code to insert a record into a data source. By using the _JDBCTemplate_ of the Spring JDBC module, we can reduce it to a few lines of code with only a few configurations.

### What Is Spring Boot?

Spring Boot is basically an extension of the Spring framework, which eliminates the boilerplate configurations required for setting up a Spring application.

**It takes an opinionated view of the Spring platform, which paves the way for a faster and more efficient development ecosystem**.

Here are just a few of the features in Spring Boot:

-   Opinionated ‘starter' dependencies to simplify the build and application configuration
-   Embedded server to avoid complexity in application deployment
-   Metrics, Health check, and externalized configuration
-   Automatic config for Spring functionality – whenever possible

Let's get familiar with both of these frameworks step by step.


## spring boot 和 ssm比较

SSM框架和spring boot全家桶相比有哪些优缺点？  
这两者对比起来有点奇怪。因为SSM是WEB应用框架，涵盖整个应用层，而spring boot你可以看做一个启动、配置、快速开发的辅助框架，本身针对的是微服务。参考资料[1]

### 参考资料
1. [spring boot和SSM开发中有什么区别？](https://blog.csdn.net/qq_43202482/article/details/88378771)
2. https://spring.io/projects/spring-boot
3. [A Comparison Between Spring and Spring Boot](https://www.baeldung.com/spring-vs-spring-boot)
4. https://www.jianshu.com/p/ffe5ebe17c3a