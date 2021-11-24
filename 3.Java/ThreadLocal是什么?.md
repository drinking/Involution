The _TheadLocal_ construct allows us to store data that will be **accessible only** by **a specific thread**.

**ThreadLocal**的**作用**是提供线程内的局部变量，这种变量在线程的生命周期内起**作用**。 **作用**：提供一个线程内公共变量（比如本次请求的用户信息），减少同一个线程内多个函数或者组件之间一些公共变量的传递的复杂度，或者为线程提供一个私有的变量副本，这样每一个线程都可以随意修改自己的变量副本，而不会对其他线程产生影响。

### 参考资料
- https://www.baeldung.com/java-threadlocal