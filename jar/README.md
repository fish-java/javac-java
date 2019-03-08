### 如何创建自己的jar包？
复制上一阶段(output)的目录结构。

可以通过这样的命令还创建:`jar cf jar-file input-file(s)`

``` bash
$ cd dist
$ jar cf fish-bird.jar com/github/Bird.class

# 如果想反编译的话，可以
$ jar xf fish-bird.jar
```
### 编译阶段如何引用jar包？
好了，应用jar包的时候坑比较多，注意安全。
为了排除测试干扰，记得把`./dist/com/github/Bird.class` 和`com/github/Bird.java删除`。

现在我们的目录结构是这样的：
```
.
├── Main.java
├── README.md
└── dist
    └── fish-bird.jar
```

通过下面的方式编译: 
``` bash
$ javac -cp ./dist/fish-bird.jar Main.java
# success

$ javac -cp ./dist/*.jar Main.java
# success

$ javac -cp ./dist/* Main.java
# success
```

### 运行
好了，那么如何执行呢？

``` bash
$ java -cp ./dist/fish-bird.jar:. Main
hi, I am a Bird

$ java -cp ./dist/*:. Main 
no matches found: ./dist/*:.
# failed, 使用*必须加上引号
# java挺坑的，要注意了

$ java -cp "./dist/*:." Main
# success
```