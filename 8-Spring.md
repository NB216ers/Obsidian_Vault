Spring 获取 Bean 的规则中有这样一条：尽可能保证所有 bean 初始化后调用注册的 BeanPostProcessor 的 postProcessAfterInitialization 方法进行处理。在实际开发过程中大可以针对此特性设计自己的业务逻辑。[^1]

[^1]: Spring 源码深度解析 90 页