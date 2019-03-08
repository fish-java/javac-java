接下来我们看一下有依赖关系的情况

在当前文件夹创建👇的文件
``` bash
$ ls
Dog.java Main.java  README.md
```

我们的Main.java 依赖了Dog.java
```
$ javac Main.java
$ ls
Dog.class  Dog.java   Main.class Main.java  README.md
```
我们可以看到，javac在处理依赖关系的时候，自动的帮我们把依赖的文件给编译了。

运行:
``` bash
$ java Main
Bob is marking
```
很简单。
