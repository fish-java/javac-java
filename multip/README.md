创建下面的文件结构
``` bash
$ tree
.
├── Main.java
├── OTHER
│   └── com
│       └── github
│           └── Bird.java
├── README.md
└── xyz
    └── bitfish
        └── Fish.java
```
我们的Main.java 依赖的两个包，而且它们不再同一个目录。那么我们在编译时就要指定多个路径
像这样：
```
$ javac -cp ./OTHER:. Main.java
```
**windows 下请将分隔符 : 换成 ;**
通过cp指明所有依赖的classpath，记得不要忘了当前文件夹，因为指明cp会覆盖默认设置

执行时引用多个
```
$ java -cp ./OTHER:. Main
hello world
hi, I am a Bird
```
