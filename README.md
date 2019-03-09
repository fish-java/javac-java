# Java命令行编译规则
Java程序的编译、运行是一件很头疼的事情，相信ClassNotFoundException是每个Java程序员都遇到过的事情。所以这次好好整理一下，希望后来者再也不会遇到这个问题了。


如果有读者朋友之前是写nodejs或者python这类的动态语言的，可能会对Java的编译机制很费解。nodejs它是基于文件系统进行模块管理的，程序员可以通过相对或绝对路径的来指明程序的入口文件，或者通过路径来指明依赖关系，文件和文件之间是互相交叉的网状或者树状结构。

但是其实Java的模块管理是基于包的，而且包和包之间是平行的关系。

当我们使用`javac`编译文件的时候，它其实做了这些事：
- 通过相对路径找到入口文件，尝试编译

  比如说如果我们执行`javac ./test/Hello.java`的时候，它会到`./test`目录下寻找Hello.java文件

- 如果发现Hello.java依赖了一些其他的包的class文件。javac就会尝试在它的搜索路径（后面说）里搜索这些包，确认它们是否存在

  - 如果存在

    就继续对Hello.java进行编译

  - 如果不存在相关的包以及class文件

    javac就会尝试搜索是否存在相关的.java文件

    - 如果存在

      把它们编译成class文件

    - 如果不存在

      抛出异常了

当我们使用`java`运行class文件的时候，它其实是会在classpath中寻找相关的包和class文件，完全不使用相对路径。（当然，包本生就暗含的相对路径的信息）


那么，`java`它是怎么查找.class文件的呢？

Java中的class文件有三种：

1. Bootstrap classes

  也就是JDK自带的工具包里面的class文件。

2. Extension classes

  用户下载的第三方jar包里面的class文件
  
3. 用户项目中自定义的class

第一种只要你安装JDK后没有瞎折腾，`javac` 和 `java`肯定能找到，这里就不多说了。

我们关键说后两种情况，第三方包和用户自定义的包按照下面的规则来查找

- 默认是`.`文件夹，也就是`javac`或者`java`的启动目录
- 然后`java`会查看shell的环境变量，看看CLASSPATH的值
- 通过`-cp`或者`-classpath`指定

多说无益，大家可以按照下面的顺序来阅读我给出的例子

## 文章列表
**如果没有特殊说明，命令行程序都是在README.md 文件所在的目录执行的。**

**小写的java都是指命令行程序**

- [single](./single)
- [package](./package)
- [classes](./classes)
- [multip](./multip)
- [package2](./package2)
- [output](./output)
- [jar](./jar)
