#input 

什么是嵌套？嵌套就是我跟你没关系，自己可以完全独立存在，但是我就想借你的壳用一下，来隐藏一下我自己（真 TM 猥琐）。

什么是内部？内部就是我是你的一部分，我了解你，我知道你的全部，没有你就没有我。（所以内部类对象是以外部类对象存在为前提的）

[为什么Java内部类要设计成静态和非静态两种？ - 知乎 (zhihu.com)](https://www.zhihu.com/question/28197253#:~:text=%E9%9D%99%E6%80%81%E5%86%85%E9%83%A8%E7%B1%BB%E7%9A%84%E4%BD%9C%E7%94%A8,%E7%90%86%E7%B1%BB%E7%BB%93%E6%9E%84%E8%80%8C%E5%AE%9A%E4%B9%89%E3%80%82)



- 嵌套类（功能是帮助的类）使它们的包更加精简
- 增强了封装性；考虑两个顶级类 A 和 B，其中 B 需要访问 A 的成员，否则这些成员将被声明为私有。通过将类 B 隐藏在类 A 中，可以将 A 的成员声明为私有，B 可以访问它们。此外，B 本身可以隐藏在外界之外。
- 更具可读性和可维护性的代码：将小类嵌套在顶级类中会使代码更接近其使用位置。



[Nested Classes (The Java™ Tutorials > Learning the Java Language > Classes and Objects) (oracle.com)](https://docs.oracle.com/javase/tutorial/java/javaOO/nested.html)
