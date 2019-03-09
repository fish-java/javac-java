# package
这次我们创建如目录所示的目录结构
``` bash
$ javac -cp ./OTHER:. com/github/fish/Hello.java
$ java -cp ./OTHER:. com.github.fish.Hello 
Hello Friend!
Hi, I am a monky!
```
Monky.sayHi是在同一个包内才能访问的方法，而程序可以正常运行

说明即使Hello.java 和 Monky.java 虽然不在同一个文件夹，但是它们的包名相同，它们就是在运行时就算在同一个包里面
