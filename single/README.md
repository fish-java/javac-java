# single
在当前目录下创建`Hello.java`。这个文件没有任何依赖关系，同时我们也没有给它指定包名，它其实就在一个匿名包中。
这可能是最简单的情况的了。

``` bash
# 编译文件
$ javac Hello.java

# 运行程序
$ java Hello
Hello Friend!
```
**编译源文件的时候需要加后缀名，运行的时候不用**。

这种情况很简单，但是如果我们想在上一级目录下编译，我们该怎么做呢？

``` bash
$ cd ..

# 可以通过相对路径指明源文件的位置
$ javac ./single/Hello.java
```

嗯，看起来不错，但是如果想运行 Hello.class怎么办呢？
``` bash
$ java ./single/Hello     
Error: Could not find or load main class ..single.Hello
Caused by: java.lang.ClassNotFoundException: //single/Hello
```

蛤，出错了。这步虽然很简单，但其实这是理解Java类查找机制的关键。

当我们尝试执行一个class文件的时候，`java`它是先确认类的搜索路径，然后再在这些路径中寻找对应的class文件！

我们之前执行`java Hello`的时候，它其实这样做了
- 创建一个列表classpath list，java将来会在这个目录下查询包和类文件
- 把JDK自带的工具包所在的目录添加到classpath list，这步不用我们管
- 把`.`文件夹添加到classpath list
- 在classpath list下搜索Hello.class
- 找到了Hello.class，执行它

而我们第二次执行的时候，出现了什么问题 ?
- 创建一个列表classpath list，java将来会在这个目录下查询包和类文件
- 把JDK自带的工具包所在的目录添加到classpath list，这步不用我们管
- 把`.`文件夹添加到classpath list
- 在classpath list下搜索Hello.class
- 找不到到Hello.class，抛出异常

错误的原因在第三步，我们的java程序是在single文件夹平级的目录执行的，而Hello.class文件在single文件夹内部，它当然找不到了。

虽然我们尝试使用 `./single/Hello.java` 来告知java我们的文件在single文件夹下，但是遗憾的是，java只会把这个字符串当做包名+类名，它并不会把它当做相对路径。

那么如果我们就是想在上级目录执行Hello.class怎么办呢？
- 我们可以手动把single文件夹添加到搜索路径

``` bash
# 在和single文件夹上级目录运行下面的程序

$ java -cp ./single Hello
Hello Friend!
```
这次执行的时候
- 创建一个列表classpath list，java将来会在这个目录下查询包和类文件
- 把JDK自带的工具包所在的目录添加到classpath list，这步不用我们管
- 把`./single`文件夹添加到classpath list
  注意这步，因为我们显示的指定了classpath，java就不会把`.`添加到classpath list
- 在classpath list下搜索Hello.class
- 找到Hello.class，运行它

好，基本情况就是这样，我们在来看一个错误示范
``` bash
# 在和single文件夹上级目录运行下面的程序

$ java single.Hello
Error: Could not find or load main class single.Hello
Caused by: java.lang.NoClassDefFoundError: Hello (wrong name: single/Hello)
```

这次执行的时候
- 创建一个列表classpath list，java将来会在这个目录下查询包和类文件
- 把JDK自带的工具包所在的目录添加到classpath list，这步不用我们管
- 把`.`文件夹添加到classpath list
- 在classpath list下搜索single.Hello.class
- 找到了Hello.class
- 但是发现Hello.class 的文件声明中并没有 `package single`，因此会抛出异常
