# package
接下来我们再创建一个有包的class。

```bash
$ mkdir -p com/github/fish
# 这就是我们的包了
```

然后把我们之前的Hello.java复制到fish文件夹里面,然后添加
`package com.github.fish;`。

我们来编译运行：
``` bash
$ javac com/github/fish/Hello.java
$ java -cp . com.github.fish.Hello 
```
可以看到：
- 当我们编译一个java文件的时候，我们是通过相对或绝对路径找到这个文件的。
- 当我们尝试运行一个class文件的时候，我们是通过包名来查找的。而包名就暗示了它在磁盘中的位置。
