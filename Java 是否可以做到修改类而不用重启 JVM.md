> Java 能不能做到修改类中的任何元素，或者增加类，而不用重启 JVM.
> 如果能，应该怎么做？
>

作者：RednaxelaFX  
链接：https://www.zhihu.com/question/28833796/answer/42310417  
来源：知乎  
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。  
  
#  修改
首先在当前JVM规范及一些相关规范（JVMTI之类）所规定要实现的功能里，题主想要的“修改类中的任何元素”这点是做不到的。增加新的类则是JVM向来都支持得很好的功能，无论新增的类是直接在内存里动态生成的，还是通过网络新下载的，都没问题。

在标准Java里，JVMTI agent与Java agent可以进行retransform（插桩） / redefine class操作，动态对已加载的类的内容进行修改而无需重启JVM。但这种方式所允许的修改非常受限——==只能修改已有方法的方法体，而不能添加新成员/删除已有成员/修改已有成员的签名（signature）==。

[JVM(TM) Tool Interface 1.2.3](https://link.zhihu.com/?target=http%3A//docs.oracle.com/javase/8/docs/platform/jvmti/jvmti.html%23RedefineClasses)

> The redefinition may change method bodies, the constant pool and attributes. **The [redefinition](https://www.zhihu.com/search?q=redefinition&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra=%7B%22sourceType%22%3A%22answer%22%2C%22sourceId%22%3A42310417%7D) must not add, remove or rename fields or methods, change the [signatures](https://www.zhihu.com/search?q=signatures&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra=%7B%22sourceType%22%3A%22answer%22%2C%22sourceId%22%3A42310417%7D) of methods, change [modifiers](https://www.zhihu.com/search?q=modifiers&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra=%7B%22sourceType%22%3A%22answer%22%2C%22sourceId%22%3A42310417%7D), or change inheritance.** These restrictions may be lifted in future versions. See the error return description below for information on error codes returned if an unsupported redefinition is attempted.

这个功能也被叫做“HotSwap”，常用于热部署或者IDE的edit-and-continue之类的功能。

## JRebel
这些工具的做法都一样：用JVMTI或Java agent的[retransform](https://www.zhihu.com/search?q=retransform&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra=%7B%22sourceType%22%3A%22answer%22%2C%22sourceId%22%3A42310417%7D)功能在用户的类被加载的时候对其进行修改，悄悄添加一个间接层到所有涉及符号链接的地方，然后如果用户想动态更新类定义的话，它就只是修改间接层的部分，所以可以绕开HotSwap的固有限制而可以运行在标准的JVM上。

但添加这个间接层对性能的影响⋯呵呵呵呵。如果在生产环境用这种解决方案而应用性能没受啥影响，或许您的应用是那种I/O密集性的或者干脆就不太需要高性能的。

# class loader 卸载在加载
[[类加载器]]