
### 主要干的事情
1. 初始化自身,设置参数
2. 自定义init,destory,pre和post consturct回调
3. 获取自身名词,factory等属于容器的信息


### 涉及方法
1、Bean自身的方法:这个包括了Bean本身调用的方法和通过配置文件中<bean>的init-method和destroy-method指定的方法

2、Bean级生命周期接口方法:这个包括了BeanNameAware、BeanFactoryAware、InitializingBean和DiposableBean这些接口的方法

3、容器级生命周期接口方法:这个包括了InstantiationAwareBeanPostProcessor 和 BeanPostProcessor 这两个接口实现，一般称它们的实现类为“后处理器”。

4、工厂后处理器接口方法:这个包括了AspectJWeavingEnabler, ConfigurationClassPostProcessor, CustomAutowireConfigurer等等非常有用的工厂后处理器　　接口的方法。工厂后处理器也是容器级的。在应用上下文装配配置文件之后立即调用。

## 参考资料
- https://www.cnblogs.com/zrtqsk/p/3735273.html
- https://www.zhihu.com/question/38597960
- https://stackoverflow.com/questions/4460384/when-is-a-spring-beans-destroy-method-called